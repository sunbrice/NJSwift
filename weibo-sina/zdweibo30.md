# ZDWeibo30

###@IBInspectable
```swift
//  提供外界设置占位文字的属性
    //  @IBInspectable 给xib/sb添加可以设置的属性
    @IBInspectable var placeHolder: String? {
        didSet {
            placeHolderLabel.text = placeHolder

        }
    }
```


###UIStackView

```swift
//  自定义发微博toolbar
//  UIStackView 是容器, 不具备渲染功能,颜色根据子控件显示
class CZComposeToolBar: UIStackView {


    //  添加控件设置布局方式
    private func setupUI() {
        //  水平方向布局
        axis = .Horizontal
        //  子控件等比填充
        distribution = .FillEqually
```


###访问相册
```swift
        let picCtr = UIImagePickerController()
        picCtr.delegate = self

        if UIImagePickerController.isSourceTypeAvailable(.Camera) {
            //  设置来源类型
            picCtr.sourceType = .Camera

        } else {
            //  设置图库
            picCtr.sourceType = .PhotoLibrary
        }

        //  判断前置摄像头是否可用
        if UIImagePickerController.isCameraDeviceAvailable(.Front) {

            print("前置摄像头可用")
        } else if UIImagePickerController.isCameraDeviceAvailable(.Rear) {
            print("后者摄像头可用")
        } else {
            print("没有摄像头")
        }

        //  是否允许编辑
        //picCtr.allowsEditing = true

        presentViewController(picCtr, animated: true, completion: nil)
```

###url的参数获得

```swift
 if let query = url.query where query.hasPrefix("code=") {
            //  获取code
            print(query)
            let code = query.substringFromIndex("code=".endIndex)
            print(code)
}
```

###记录约束卸载约束
```swift
            retweetViewBottomConstraint?.uninstall()



                self.snp_updateConstraints(closure: { (make) -> Void in
                   self.retweetViewBottomConstraint =  make.bottom.equalTo(pictureView).offset(StatusTableViewCellMargin).constraint
                })
```

###枚举
```swift
//  通过原始值获取枚举
        let type = CZComposeToolBarButtonType(rawValue: button.tag)!
             //  根据枚举的原始值最为tag
        button.tag = type.rawValue
```

###enumerate
```swift
            //  绑定表情数据
            for (i, value) in ets.enumerate() {
                //  获取表情按钮的控件
                let emoticonButton = emoticonButtonArray[i]

                }
```

###filter

```swift
        //  扩展

        //  $0表示闭包中的第一个参数, $1表示第二个参数....
        //  如果只有一行代码还可以省略return  ,以上代码需要看懂
        if let defaultEmoticon = defaultEmoticonArray.filter({ $0.chs == chs}).first {
            return defaultEmoticon
        }
        if let lxhEmoticon = lxhEmoticonArray.filter({ $0.chs == chs}).first {
            return lxhEmoticon
        }

        let defaultEmoticon = defaultEmoticonArray.filter { (emoticon) -> Bool in
            return emoticon.chs == chs
        }.first
```


###数组翻转
```swift

 //  reverse 数组翻转
        for value in matchResultArray.reverse() {

            //  查找本地的表情模型
            if let emoticon = CZEmoticonTools.sharedTools.searchEmoticonWithChs(value.matchString) {
                print(status)
                //  把表情模型转成表情富文本
                //  取到表情模型里面的图片路径, 创建UIImage对象,然后让其转成富文本
                //  通过表情模型和字体对象创建表情富文本
                let attributedStr = NSAttributedString.attributedStringWithEmoticon(emoticon, font: UIFont.systemFontOfSize(StatusFontSize))
                //  通过匹配的表情描述的范围替换指定表情富文本
                result.replaceCharactersInRange(value.matchRange, withAttributedString: attributedStr)

            }

 ```

