# Monitor-Property

- 属性监听器, `newValue/oldValue`
    - `willSet`
    - `didSet`


```swift

class Person: NSObject {
    // 属性监听器
        // 可以给newValue自定义名称
        willSet (new){ // 属性即将改变,还未改变时会调用的方法
            // 在该方法中有一个默认的系统属性newValue,用于存储新值
            print(name)
            print(new)
        }
        // 可以给oldValue自定义名称
        didSet (old) { // 属性值已经改变了,会调用的方法
            // 在该方法中有一个默认的系统属性oldValue,用于存储旧值
            print(name)
            print(old)
        }
    }
}

let p = Person()
p.name = "why"
p.name = "yz"

// 输出结果
/*
nil
Optional("why")
Optional("why")
nil
Optional("why")
Optional("yz")
Optional("yz")
Optional("why")

*/
```





