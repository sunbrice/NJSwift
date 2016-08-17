# 7thDay

###textview
- 1删除

```swift
 ///删除
        if emoticon.isRemove
        {
            self.deleteBackward()
            return
        }
```
- 2插入普通的文字

```swift
        ///插入emoji
        if emoticon.emojiCode != nil
        {
            ///获取光标所在的位置
//  let range = self.textView.selectedTextRange
            ///替换所在位置
//  self.textView.replaceRange(<#T##range: UITextRange##UITextRange#>, withText: <#T##String#>)

            ///直接插入
            self.insertText(emoticon.emojiCode!)

            return
        }
```

- 3 图文混排`NSTextAttachment`和`NSAttributedString(attachment: attachment)`


```swift

        // 4.普通表情:图文混排
        // 4.1.根据图片路径创建属性字符串
        let attachment = NSTextAttachment()
        attachment.image = UIImage(contentsOfFile: emoticon.pngPath!)

        ///保存字体解决bug
        let font = textView.font!
        attachment.bounds = CGRect(x: 0, y: -4, width: font.lineHeight, height: font.lineHeight)
        let attrImageStr = NSAttributedString(attachment: attachment)

        // 4.2.创建可变的属性字符串
        let attrMStr = NSMutableAttributedString(attributedString: textView.attributedText)

        // 4.3.将图片属性字符串,替换到可变属性字符串的某一个位置
        // 4.3.1.获取光标所在的位置
        let range = textView.selectedRange

        // 4.3.2.替换属性字符串
        attrMStr.replaceCharactersInRange(range, withAttributedString: attrImageStr)

        // 显示属性字符串
        textView.attributedText = attrMStr

        // 将文字的大小重置
        textView.font = font

        // 将光标设置回原来位置 + 1
        textView.selectedRange = NSRange(location: range.location + 1, length: 0)
```

###图文混排后如何获得文中普通图片对应的字符串?

- 自定义NSTextAttachment, 增加属性保存图片的文字

```swift
        // 4.普通表情:图文混排
        // 4.1.根据图片路径创建属性字符串
        let attachment = EmoticonAttachment()
        attachment.chs = emoticon.chs
        attachment.image = UIImage(contentsOfFile: emoticon.pngPath!)
        let font = textView.font!
        attachment.bounds = CGRect(x: 0, y: -4, width: font.lineHeight, height: font.lineHeight)
        let attrImageStr = NSAttributedString(attachment: attachment)
```

- 遍历富文本字符串获得attachment
- 把里边的对应的文职替换成文字

```swift
        // 1.获取属性字符串
        let attrMStr = NSMutableAttributedString(attributedString: textView.attributedText)

        // 2.遍历属性字符串
        let range = NSRange(location: 0, length: attrMStr.length)
        attrMStr.enumerateAttributesInRange(range, options: []) { (dict, range, _) -> Void in
            if let attachment = dict["NSAttachment"] as? EmoticonAttachment {
                attrMStr.replaceCharactersInRange(range, withString: attachment.chs!)
            }
        }

        // 3.获取字符串
        print(attrMStr.string)
    }
```

###怎么切换键盘
- 先取消第一响应者
- 更换inputview
- 成为第一响应者

```swift
        emoticonKeyboardVc.mjTextView.resignFirstResponder()

        emoticonKeyboardVc.mjTextView.inputView = (emoticonKeyboardVc.mjTextView.inputView != nil ? nil : emoticonKeyboardVc.keyboard)

        emoticonKeyboardVc.mjTextView.becomeFirstResponder()
```

###frame和bounds的区别

- 修改frame的时候, 比如修改宽度, 那x不会变
- 而用bounds修改宽度的时候, 是从控件的中间开始增大, x会变

### 把图片写入相册

```swift
         UIImageWriteToSavedPhotosAlbum(image, self, "image:didFinishSavingWithError:contextInfo:", nil)

    }

    @objc private func image(image : UIImage, didFinishSavingWithError error : NSError?, contextInfo : AnyObject) {

        if error != nil
        {
            SVProgressHUD.showErrorWithStatus("图片保存失败")
        }else
        {
            SVProgressHUD.showSuccessWithStatus("图片保存成功")
        }

    }
```
