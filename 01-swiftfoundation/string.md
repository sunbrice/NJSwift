# String

- 1.定义字符串
- 2.遍历字符串中字符

```swift
let str = "hello world"

for c in str.characters {
    print(c)
}
```

### 3.字符串的拼接
- 3.1.字符串之间的拼接

```swift
let str1 = "NJHu"
let str2 = "Alan"
let result = str1 + str2
```

- 3.2.字符串和其他标识符之间的拼接

```swift
let age = 18
let name = "why"
let height = 1.88

// 拼接其他标识符的格式: \(标识符的名称)
let info = "my name is \(name), age is \(age), height is \(height)"
```

- 3.3.字符串的格式化: 音乐播放器

```swift
let min = 3
let second = 04
//let timeStr = "0\(min):0\(second)"
let timeStr = String(format: "%02d:%02d", arguments: [min, second])
```

- 4.字符串的截取
    - 将String类型转成NSString类型 string as NSString

```swift
let urlString = "www.520it.com"

// 将String类型转成NSString类型 string as NSString
let header = (urlString as NSString).substringToIndex(3)
let middle = (urlString as NSString).substringWithRange(NSRange(location: 4, length: 5))
let footer = (urlString as NSString).substringFromIndex(10)
```


