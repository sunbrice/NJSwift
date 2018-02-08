# Array

- 不可变数组(let)和可变数组(var)

- 1>不可变数组

```swift
let array = ["why", "lmj", "lnj", "yz"]
```
- 2>可变数组的2中不同的方式

```swift
var arrayM1 = Array<String>()
var arrayM = [String]()
```

- 3>对可变数组的操作(增删改查)

```swift
// 2.1.添加元素
arrayM.append("why")
arrayM.append("yz")
arrayM.append("lmj")
arrayM.append("lnj")

// 2.2.删除元素
arrayM.removeAtIndex(0)

// 2.3.修改元素
arrayM[1] = "why"

```

- 4 遍历数组的4中方式, 注意第四种方式

```swift
for i in 0..<arrayM.count {
    print(arrayM[i])
}

for name in arrayM {
    print(name)
}

// 不常见
for i in 0..<2 {
    print(arrayM[i])
}

for name in arrayM[0..<2] {
    print(name)
}

```

- 5 数组的合并
    - swift中如果两个数组类型是完全一致的,可以相加进行合并

```swift
let resultM = arrayM + array
```














