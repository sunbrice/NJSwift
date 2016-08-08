# SecondDay

### 一, 异常处理

- 如果在调用系统某一个方法时,该方法最后有一个throws.说明该方法会抛出异常.
- 如果一个方法会抛出异常,那么需要对该异常进行处理
- 在swift中提供三种处理异常的方式

- 方式一:try方式 程序员手动捕捉异常

```swift
        do {
          let regex = try NSRegularExpression(pattern: pattern, options: .CaseInsensitive)
        } catch {
            print(error)
        }
```

-  方式二:try?方式(常用方式) 系统帮助我们处理异常,如果该方法出现了异常,则该方法返回nil.
-  如果没有异常,则返回对应的对象

```swift
        guard let regex0 = try? NSRegularExpression(pattern: pattern, options: .CaseInsensitive) else {
            return
        }
```

- 方式三:try!方法(不建议,非常危险) 直接告诉系统,该方法没有异常.
- 注意:如果该方法出现了异常,那么程序会报错(崩溃)

```swift
let regex1 = try! NSRegularExpression(pattern: pattern, options: .CaseInsensitive)
```

### 二, 根据字符串创建类对象

```swift
        // 0.获取命名空间
        guard let nameSpace = NSBundle.mainBundle().infoDictionary!["CFBundleExecutable"]
                                as? String else {
            print("没有获取命名空间")
            return
        }

        // 1.根据字符串获取对应的Class
        guard let anyClass = NSClassFromString(nameSpace + "." + childVcName) else {
            print("没有获取到字符串对应的Class")
            return
        }

        // 2.将对应的AnyClass转成控制器的类型
        guard let childVcType = anyClass as? UIViewController.Type else {
            print("没有获取对应控制器的类型")
            return
        }

        // 3.创建对应的控制器对象
        let childVc = childVcType.init()
```

### 三, 类方法
- swift中类方法是以class开头的方法.类似于OC中+开头的方法

```swift
    class func createButton(imageName : String, bgImageName : String) -> UIButton {
        // 1.创建btn
        let btn = UIButton()

        // 2.设置btn的属性
        btn.setImage(UIImage(named: imageName), forState: .Normal)

        btn.sizeToFit()

        return btn
    }

// 外边怎么用
    private lazy var composeBtn : UIButton = UIButton.createButton("tabbar_compose_icon_add", bgImageName: "tabbar_compose_button")
```


### swift中的SEL
###访客视图中的icon的缩放问题
###animation
###initWithFame的注意点
###modal的背后控制





