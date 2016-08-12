# 5thDay

```swift
// MARK: - 缓存所有的图片, 拿到所有的图片的尺寸
extension LMJStatusListViewModel
{
    /// 缓存所有的图片, 拿到所有的图片的尺寸
    private func cachePicturesToGetImageSize(completion: () -> ())
    {
        let group = dispatch_group_create()

        for statusViewModel in statusViewModels
        {
            for picURL in statusViewModel.picURLs_lmj
            {
                /// 进入组
                dispatch_group_enter(group)

                SDWebImageManager.sharedManager().downloadImageWithURL(picURL, options: [], progress: nil, completed: { (_, _, _, _, _) -> Void in
                    /// 离开组
                    dispatch_group_leave(group)
                })
            }
        }

        dispatch_group_notify(group, dispatch_get_main_queue()) { () -> Void in

            LMJLog("线程组内下载图片完成")
            ///执行完成
            completion()
        }
    }
}
```
