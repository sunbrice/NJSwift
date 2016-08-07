# Func

```swift
func 函数名(参数列表) -> 返回值类型 {
    代码块
    return 返回值
}
```

- 1.没有参数没有返回值

```swift
func about() -> Void {
    print("iPhone7s Plus")
}

func about1() {
    print("iPhone7s")
}

func about2() -> (){

    print("iphone")
}
about2()
about()
```

- 2.有参数没有返回值

```swift
func callPhone(phoneNum : String) {
    print("打电话给\(phoneNum)")
}

callPhone("+86 110")
```

- 3.没有参数有返回值

```swift
func readMessage() -> String {
    return "吃饭了吗?"
}
```


- 4.有参数有返回值

```swift
func sum(num1 : Int, num2 : Int) -> Int {
    return num1 + num2
}

sum(20, num2: 30)
```

