# Dictionary

- 注意:在swift中无论是数组还是字典都是使用[],但是如果[]中存放的是元素,编译器会认为是一个数组.如果[]中存放的是键值对,编译器会认为是一个字典

- 1>不可变字典(let)

```swift
let dict = ["name" : "why", "age" : 18, "height" : 1.88]
```

- 2>可变字典(var)
    - 创建方式之一, 类型限定`Dictionary<String, AnyObject>()`
    - 创建方式之二, 指定元素`[String : AnyObject]()`
```swift
var dictM0 = Dictionary<String, AnyObject>()
var dictM = [String : AnyObject]()
```

- 2.1.添加元素

```swift
dictM["name"] = "why"
dictM["age"] = 18
dictM["heihgt"] = 1.88
dictM["weight"] = 75
```

- 2.2.删除元素

```swift
dictM.removeValueForKey("name")
```

- 2.3.修改元素
    - 注意:如果有对应的key,则修改对应的value,如果没有对应的key,则添加对应的键值对

```swift
dictM["age"] = 30
```
- 2.4.获取元素


- 3 遍历字典

```swift
// 3.1.遍历所有的key
for key in dictM.keys {
    print(key)
}

// 3.2.遍历所有的value
for value in dictM.values {
    print(value)
}

// 3.3.遍历所有的key/value
for (key, value) in dictM {
    print(key)
    print(value)
}

```

- 4 合并字典
    - 注意:字典即使类型一直也不可以先加合并
    - 是遍历出另一个字典的所有键值对添加到新的字典中
```swift
let tempDict : [String : AnyObject] = ["phoneNum" : "+86 110", "sex" : "男"]

for (key, value) in tempDict {
    dictM[key] = value
}
```

