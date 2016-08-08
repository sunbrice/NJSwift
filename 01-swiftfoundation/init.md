# init()

- 重写系统的构造函数`init()`
    - 在构造函数中,如果没有明确super.init(),那么系统会帮助调用super.init()

```swift
    override init() {
        // 在构造函数中,如果没有明确super.init(),那么系统会帮助调用super.init()
        print("------")
        // super.init()
    }
```

- 自定义构造函数
    - 注意:如果自定义了构造函数,会覆盖init()方法.即不在有默认的构造函数

```swift
    init(name : String, age : Int) {
        self.name = name
        self.age = age
        // super.init()
    }
```

- **从字典中取出的value是一个Anyobject?, 需要转成String?和Int**
- as? 最终转成的类型是一个可选类型

```swift
        if let name = dict["name"] as? String
        {
        // self.name是String?
            self.name = name
        }

        if let age = dict["age"] as? Int
        {
            self.age = age
        }
```
- as! 最终转成的类型是一个确定的类型

```swift
        if dict["name"] != nil
        {
            self.name = (dict["name"] as? String)!
//            self.name = dict["name"] as? String
        }

        if dict["age"] != nil
        {
            self.age = dict["age"] as! Int
//            self.age = (dict["age"] as? Int)!
        }
```

- 在自定义构造方法中用到了字典

```swift
    init(dict0 : [String : AnyObject]) {
        super.init()

        setValuesForKeysWithDictionary(dict0)
    }

    override func setValue(value: AnyObject?, forUndefinedKey key: String) {}
```

- `convenience` : 便利,使用convenience修饰的构造函数叫做便利构造函数
    - 遍历构造函数通常用在对系统的类进行构造函数的扩充时使用
- 遍历构造函数的特点
    - 1.遍历构造函数通常都是写在extension里面
    - 2.遍历构造函数init前面需要加载convenience
    - 3.在遍历构造函数中需要明确的调用self.init()

```swift
    convenience init (imageName : String, bgImageName : String) {
        self.init()

        setImage(UIImage(named: imageName), forState: .Normal)
        sizeToFit()
    }
```






