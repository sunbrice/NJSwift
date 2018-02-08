# dateHandle

```swift

 //  判断时间是否是今年
                //  判断是否是今天
                    //  判断是否是1分钟之内
                        //  - 刚刚
                    //  判断是否是1小时之内
                        //  - xx分钟前
                    //  其它
                        //  - xx小时前
                //  判断是否是昨天
                    //  - 昨天 10:10
                //  其他
                    08-14 08:41
        //  不是今年
            //  2015-10-20 20:10


extension NSDate {
    //  通过时间字符串转成时间对象
    class func sinaDate(createDateStr: String) -> NSDate {
        //  代码执行到此,表示发微博时间不为nil,表示没有问题
        let dt = NSDateFormatter()
        //  指定格式化方式
        dt.dateFormat = "EEE MMM dd HH:mm:ss z yyyy"
        //  指定本地化信息
        dt.locale = NSLocale(localeIdentifier: "en_US")
        //  通过格式化方式转成成时间对象
        //  当前时间加上多少秒
        //  NSDate().dateByAddingTimeInterval(-3600-1000)
        let createDate = dt.dateFromString(createDateStr)!

        return createDate
    }
    //  微博时间字符串
    var sinaDateString: String {

        let dt = NSDateFormatter()
        //  指定本地化信息
        dt.locale = NSLocale(localeIdentifier: "en_US")

        if isThisYear(self) {
            //  是今年
            //  日历对象
            let calendar = NSCalendar.currentCalendar()


            if calendar.isDateInToday(self) {
                //  是今天
                //                createDate.timeIntervalSinceDate(<#T##anotherDate: NSDate##NSDate#>)
                //  获取发微博时间距离当前时间差多少秒
                let timeInterVal = abs(self.timeIntervalSinceNow)

                if timeInterVal < 60 {
                    return "刚刚"
                } else if timeInterVal < 3600 {

                    let result = timeInterVal / 60

                    return "\(Int(result))分钟前"

                } else {
                    let result = timeInterVal / 3600
                    return "\(Int(result))小时前"
                }

            } else if calendar.isDateInYesterday(self) {
                //  昨天
                dt.dateFormat = "昨天 HH:mm"
            } else {
                //  其它
                dt.dateFormat = "MM-dd HH:mm"
            }



        } else {
            //  不是今年 2015-10-20 20:10
            dt.dateFormat = "yyyy-MM-dd HH:mm"
        }

        return dt.stringFromDate(self)

    }



    //  根据时间判断是否是今年
    private func isThisYear(createDate: NSDate) -> Bool {

        let dt = NSDateFormatter()
        //  指定格式化方式
        dt.dateFormat = "yyyy"
        //  指定本地化信息
        dt.locale = NSLocale(localeIdentifier: "en_US")
        //  获取发微博时间的年份
        let createDateYear = dt.stringFromDate(createDate)
        //  获取当前时间的年份
        let currentDateYear = dt.stringFromDate(NSDate())
        //  对比年份是否相同
        return createDateYear == currentDateYear



    }


}

```
