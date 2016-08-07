# Optional-nil

- 类中所有的属性在对象初始化的时候, 必须有初始化值

```swift
class Person : NSObject {
    var name : String?
    var view : UIView?
}
```

- 1.定义可选类型
    - 1>普通定义可选类型的方式`var name : Optional<String>`
    - 2>语法糖`var name : String?`

- 2.给可选类型赋值`name = "why"`

- 3.从可选类型中取值

```swift
print(name)
// 输出结果
"Optional("why")\n"
```
- 从可选类型中取值:可选类型!-->强制解包

```swift
print(name!)
// 输出结果
"why\n"
```

- 4.注意:如果可选类型中没有值,那么强制解包程序会崩溃
 - 强制解包是非常危险的操作:建议在解包前先判断可选类型中是否有值

```swift
if name != nil {
    print(name!)
}
```

- 5.可选绑定
    - 1> 判断name是否有值,如果没有值,则不执行{}
    - 2> 如果有值,则对可选类型进行解包,并且将解包后的值赋值给前面的常量

```swift
//if let tempName = name {
//    print(tempName)
//}

if let name = name {
    print(name)
}
```

###NSURL

```swift
// 通过该方法创建的URL,可能有值,也可能没有值.
// 错误写法:如果返回值是nil时,就不能接收了
// 如果字符串中有中文,则返回值为nil,因此该方法的返回值就是一个可选类型,而使用一个NSURL类型接收是错误的
let url : NSURL = NSURL(string: "www.520it.com")

// 正确写法:使用可选类型来接收
let url : NSURL? = NSURL(string: "www.520it.com")
// 该方式利用类型推导
let url = NSURL(string: "www.520it.com")

// 通过url来创建request对象:在使用可选类型前要先进行判断是否有值
// 该语法成为可选绑定(如果url有值就解包赋值给tempURL,并且执行{})
if let tempUrl = url {
    let request = NSURLRequest(URL: tempUrl)
}

// 可选绑定的简洁写法
if let url = NSURL(string: urlString) {
    let request = NSURLRequest(URL: url)
}
```






