# Class

- 1.类的定义

```swift
class Person : NSObject {
    var age : Int = 0

    // override : 重写, 如果写的某一个方法是对父类的方法进行的重写,那么必须在该方法前加上override
    override func setValue(value: AnyObject?, forUndefinedKey key: String) {}
}
```

- 2.创建类对应的对象

```swift
let p = Person()
```

- 3.给类的属性赋值
    - 直接赋值
    - 通过KVC赋值

```swift
//p.age = 20

p.setValuesForKeysWithDictionary(["age" : 18, "name" : "why"])
```

- 4.可以重写`setValue(value: AnyObject?, forUndefinedKey key: String`,那么字典中没有的字段可以在类中没有对应的属性

- `override` : 重写, 如果写的某一个方法是对父类的方法进行的重写,那么必须在该方法前加上`override`






