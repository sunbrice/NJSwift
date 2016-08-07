# SwiftFoundation

- swift中定义标识符:必须制定该标识符是一个常量还是一个变量
    - var(变量)/let(常量) 标识符的名称 : 标识符的类型 = 初始化值

```swift
var a : Int = 10;
let b : Double = 3.14;
a = 29;
// b = 3.11 错误写法

```

- 1.在开发中优先使用常量,只有在需要修改时,在修改成var
- 2.常量本质:保存的内存地址不可以修改,但是可以通过内存地址拿到对象,之后修改对象内部的属性

```swift
let view : UIView = UIView()
//  view = UIView() 错误写法
view.backgroundColor = UIColor.redColor()

```

## 类型推导
- 可以通过:option + 鼠标左键,查看一个标识符的类型

```swift

// 类型推导
// 可以通过:option + 鼠标左键,查看一个标识符的类型
// var a : Int = 30
var a = 30

```
## 基本运算

- Swift中没有隐式转化,不会将整形自动转成浮点型

```swift
// 将整型转成浮点型
let result = Double(m) + n
// 将浮点型转成整型
let result1 = m + Int(n)

```

##逻辑分支

- `if-else if -else`
- 1> if后面的()可以省略
- 2> 判断句不再有非0即真.必须有明确的Bool值:true/false

```swift

let a = 10

if a != 0 {
    print("a不等于0")
} else {
    print("a等于0")
}

```

## **guard 判断 else{}**
- guard必须用在函数
- 如果条件成立,者会执行后面的代码块
- 如果条件不成立,则会执行{}中的语句,并且{}中必须跟上

```swift

func online(age : Int) {
    guard age >= 18 else {
        print("未成年不能上网")
        return
    }

    guard 带了身份证 else {
        print("不可以上网,回家拿身份证")
        return
    }

    guard 带了钱 else {
        print("回家拿钱")
        return
    }

    print("留下来上网")
}

```













































