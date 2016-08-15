# SixDay

###collection的内容的内边距

```swift
        // 设置collectionView的内边距
        contentInset = UIEdgeInsets(top: edgeMargin, left: edgeMargin, bottom: 0, right: edgeMargin)
```

###collectionView重写init来设置流水布局
```swift
    init()
    {
        let layout = UICollectionViewFlowLayout()

        let itemWH = (LMJScreenWidth - 4 * LMJ_StatusEdgeMargin) / 3

        layout.itemSize = CGSize(width: itemWH, height: itemWH)

        layout.minimumInteritemSpacing = 1
        layout.minimumLineSpacing = LMJ_StatusEdgeMargin

        layout.sectionInset = UIEdgeInsets(top: LMJ_StatusEdgeMargin, left: LMJ_StatusEdgeMargin, bottom: 0, right: LMJ_StatusEdgeMargin)
        layout.scrollDirection = .Vertical
        super.init(collectionViewLayout: layout)
    }
```


###弹出相册控制器, 并且拿到照片
- 还要设置图片选中框的样式
- 遵守`UIImagePickerControllerDelegate, UINavigationControllerDelegate`协议里边有字典能拿到选中的照片

```swift
    override func collectionView(collectionView: UICollectionView, didSelectItemAtIndexPath indexPath: NSIndexPath) {
//        collectionView.deselectItemAtIndexPath(indexPath, animated: true)
        ///判断是否能展示图片框
        if !UIImagePickerController.isSourceTypeAvailable(.PhotoLibrary)
        {
            return
        }

        ///创建图片控制器
        let ipc = UIImagePickerController()
        ///设置代理, 监听选中的图片
        ipc.delegate = self
        //设置弹出的图片的选择控制器的样式
        ipc.sourceType = .PhotoLibrary
        ///弹出控制器
        self.presentViewController(ipc, animated: true, completion: nil)
    }
// MARK: - 照片选择器的代理
extension LMJPickPhotoCollectionViewController: UIImagePickerControllerDelegate, UINavigationControllerDelegate
{

    func imagePickerController(picker: UIImagePickerController, didFinishPickingImage image: UIImage, editingInfo: [String : AnyObject]?) {
}
```

###注意cell的循环利用, 虽然最后一个cell没有图片, 但是再返回cell的时候要给设置最右一个cell的默认图片

###VFL
- 取消需要布局控件的`translatesAutoresizingMaskIntoConstraints`属性
- 设置字典告诉系统控件对应的key
- 用vfl布局控件
- 左右对齐是竖直方向的约束

```swift
        collectionView.translatesAutoresizingMaskIntoConstraints = false
        toolBar.translatesAutoresizingMaskIntoConstraints = false

        let views = ["tBar" : toolBar, "cView" : collectionView]

var cons = NSLayoutConstraint.constraintsWithVisualFormat("H:|-0-[tBar]-0-|", options: [], metrics: nil, views: views)
cons += NSLayoutConstraint.constraintsWithVisualFormat("V:|-0-[cView]-0-[tBar]-0-|", options: [.AlignAllLeft, .AlignAllRight], metrics: nil, views: views)
        view.addConstraints(cons)
```


###系统的约束使用addconstaints

```swift
                view.addConstraint(NSLayoutConstraint(item: toolBar, attribute: .Right, relatedBy: .Equal, toItem: view, attribute: .Right, multiplier: 1, constant: 0))

                view.addConstraint(NSLayoutConstraint(item: toolBar, attribute: .Left, relatedBy: .Equal, toItem: view, attribute: .Left, multiplier: 1, constant: 0))
                view.addConstraint(NSLayoutConstraint(item: toolBar, attribute: .Bottom, relatedBy: .Equal, toItem: view, attribute: .Bottom, multiplier: 1, constant: 0))

```

###当资源在自定义的`Emoticons.bundle`里边的时候, 需要和系统的mainbundle路径进行拼接

```swift
        ///id = com.apple.emoji
        // 2.根据id拼接info.plist的路径
        let plistPath = NSBundle.mainBundle().pathForResource("\(id)/info.plist",
        ofType: nil, inDirectory: "Emoticons.bundle")!

        // 3.根据plist文件的路径读取数据 [[String : String]]
        let array = NSArray(contentsOfFile: plistPath)! as! [[String : String]]
```

###重写descrption

```swift
    override var description : String {
        return dictionaryWithValuesForKeys(["code", "png", "chs"]).description
    }
```

###获取plist中图片名字有需要进行拼接
- 第一步先和文件夹名字拼接
- 第二部和自定义bundle拼接

```swift
        // 4.遍历数组
        for var dict in array {
            if let png = dict["png"] {
                dict["png"] = id + "/" + png
            }

            emoticons.append(Emoticon(dict: dict))
        }

            var png : String? {      // 普通表情对应的图片名称
        didSet {
            guard let png = png else {
                return
            }

            pngPath = NSBundle.mainBundle().bundlePath + "/Emoticons.bundle/" + png
        }
    }
```

###emoji表情code的转化

```swift
           // 1.创建扫描器
            let scanner = NSScanner(string: code)

            // 2.调用方法,扫描出code中的值
            var value : UInt32 = 0
            scanner.scanHexInt(&value)

            // 3.将value转成字符
            let c = Character(UnicodeScalar(value))

            // 4.将字符转成字符串
            emojiCode = String(c)
```










