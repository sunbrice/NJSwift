# Closure(闭包)

- 闭包的类型: (参数列表) -> (返回值类型)
- 闭包的写法:

```swift

    类型:(形参列表)->(返回值)
    技巧:初学者定义闭包类型,直接写()->().再填充参数和返回值

    值:
    {
        (形参) -> 返回值类型 in
        // 执行代码
    }
```

### 循环引用

- 解决循环引用的方式三:`[weak self]`用的时候`self?.view`

```swift
        tools.loadData {[weak self] (jsonData) -> () in
             print("在ViewController拿到数据:\(jsonData)")
            self?.view.backgroundColor = UIColor.redColor()
        }
```

- 解决循环引用的方式二:`unowned`用的时候`self.view`

```swift
        tools.loadData {[unowned self] (jsonData) -> () in
            // print("在ViewController拿到数据:\(jsonData)")
            self.view.backgroundColor = UIColor.redColor()
        }
```

- 解决循环引用的方式一:`weak var weakself = self`用的时候`weakself?.`

 ```swift
        // 0x0 --> nil
        weak var weakself = self
        tools.loadData { (jsonData) -> () in
            // print("在ViewController拿到数据:\(jsonData)")
            weakself?.view.backgroundColor = UIColor.redColor()
        }
 ```


 ### 尾随闭包

 - 尾随闭包:如果闭包作为方法的最后一个参数,那么闭包可以将()省略掉
    - 也可以写到最前边

```swift
        // 普通写法
        tools.loadData ({[weak self] (jsonData) -> () in
            // print("在ViewController拿到数据:\(jsonData)")
            self?.view.backgroundColor = UIColor.redColor()
        })

        // 尾随闭包的写法一:
        tools.loadData() {[weak self] (jsonData) -> () in
            // print("在ViewController拿到数据:\(jsonData)")
            self?.view.backgroundColor = UIColor.redColor()
        }

        // 尾随闭包的写法二:
        tools.loadData {[weak self] (jsonData) -> () in
            // print("在ViewController拿到数据:\(jsonData)")
            self?.view.backgroundColor = UIColor.redColor()
        }

```

### `deinit`相当OC中的dealloc方法,当对象销毁时会调用该函数

```swift
    deinit {
        print("ViewController -- deinit")
    }
```
