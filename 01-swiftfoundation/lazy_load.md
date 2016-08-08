# Lazy Load

- 格式 `lazy var 变量: 类型 = { 创建变量代码 }()`, 后边跟上一个函数调用小括号

- 懒加载的本质是,在第一次使用的时候执行闭包,将闭包的返回值赋值给属性

- lazy的作用是只会赋值一次

```swift
    lazy var array : [String] = {
        () -> [String] in
        return ["why", "lmj", "lnj"]
    }()
```

```swift

private lazy var imageNames = ["tabbar_home", "tabbar_message_center"]

private lazy var composeBtn : UIButton = UIButton()

private lazy var composeBtn : UIButton = UIButton(imageName: "tabbar_compose_icon_add", bgImageName: "tabbar_compose_button")

```
