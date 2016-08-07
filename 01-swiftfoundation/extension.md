# Extension

- 段落注释`// MARK:- 懒加载的属性`

- 属性注释`/// tableView的属性`

- extension类似OC的category,也是只能扩充方法,不能扩充属性

```swift
extension ViewController : UITableViewDataSource, UITableViewDelegate
{
    func tableView(tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        return 20
    }
}
```
