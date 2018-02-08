# Notice-Func

- 注意一:内部参数和外部参数
    - 内部参数: 在函数内部可以看到的参数就是内部参数, 默认情况下所有的参数都是内部参数
    - 外部参数: 在函数外部可以看到的参数名称就是外部参数, 默认情况从第二个参数开始既是内部参数也是外部参数
    - 如果希望第一个参数也是外部参数,可以在标识符前给该参数添加一个别名
    - 注意下边代码的`num1`

```swift
func sum(num1 num1 : Int, num2 : Int, num3 : Int) -> Int {
    return num1 + num2 + num3
}

sum(num1: 20, num2: 30, num3: 30)
```

- 注意二:swift中的默认参数

```swift
func makeCoffee(coffeeName : String = "雀巢") -> String {
    return "制作了一杯\(coffeeName)咖啡"
}

makeCoffee("拿铁")

makeCoffee()
```


- 注意三:可变参数
    - 只需要在参数的类型后边加`...`
    - 默认多个同种类型的参数

```swift
func sum(num : Int...) -> Int {
    var result = 0
    for n in num {
        result += n
    }
    return result
}

sum(18, 20, 30, 40, 50, 50)
```
- 注意四:指针类型

```swift
var m = 20
var n = 30

func swapNum(inout m : Int, inout n : Int) {
    let temp = m
    m = n
    n = temp
}

swapNum(&m, n: &n)
```

- 注意五:函数的嵌套使用(了解)

```swift
func test() {

    func demo() {
        print("demo")
    }

    print("test")

    demo()
}

test()

// 输出结果
//test
//demo
```

### swift支持方法的重载

- 方法的重载:方法名称相同,但是参数不同.
    - 1.参数的类型不同
    - 2.参数的个数不同
    - `private`在当前文件中可以访问,但是其他文件不能访问

```swift

private func addChildViewController(childVc: UIViewController, title : String, imageName : String) {

    }

```









