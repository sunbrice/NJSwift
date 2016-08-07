# SwiftFoundation

- swift中定义标识符:必须制定该标识符是一个常量还是一个变量
    - var(变量)/let(常量) 标识符的名称 : 标识符的类型 = 初始化值

```objc
var a : Int = 10;
let b : Double = 3.14;
a = 29;
// b = 3.11 错误写法

```

- 1.在开发中优先使用常量,只有在需要修改时,在修改成var
- 2.常量本质:保存的内存地址不可以修改,但是可以通过内存地址拿到对象,之后修改对象内部的属性

```objc
let view : UIView = UIView()
//  view = UIView() 错误写法
view.backgroundColor = UIColor.redColor()

```

## 类型推导
- 可以通过:option + 鼠标左键,查看一个标识符的类型

```objc

// 类型推导
// 可以通过:option + 鼠标左键,查看一个标识符的类型
// var a : Int = 30
var a = 30

```




















