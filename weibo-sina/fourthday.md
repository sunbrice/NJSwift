# FourthDay

### 自定义归档解挡
```swift
    // MARK:- 归档&解档
    /// 解档的方法
    required init?(coder aDecoder: NSCoder) {
        access_token = aDecoder.decodeObjectForKey("access_token") as? String
        uid = aDecoder.decodeObjectForKey("uid") as? String
    }

    /// 归档方法
    func encodeWithCoder(aCoder: NSCoder) {
        aCoder.encodeObject(access_token, forKey: "access_token")
        aCoder.encodeObject(uid, forKey: "uid")
    }

    // 4.2.保存对象
    NSKeyedArchiver.archiveRootObject(account, toFile: accountPath)

    // 1.2.读取信息
    let account = NSKeyedUnarchiver.unarchiveObjectWithFile(accountPath) as? UserAccount

```

###??

-  ?? : 如果??前面的可选类型有值,那么将前面的可选类型进行解包并且赋值
    -  如果??前面的可选类型为nil,那么直接使用??后面的值


