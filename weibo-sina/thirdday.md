# ThirdDay

### 如何改变modal出来控制器view的frame

- 自定义弹出的控制器的view, 是放在一个系统的presentVc里边的containerView里边
- 所以要自定义`UIPresentationController`
- 但是如何使用这个自定义的控制器?
- 1, 需要设置弹出控制器的转场代理

```swift
        // 2.创建弹出的控制器
        let popoverVc = PopoverViewController()

        // 3.设置控制器的modal样式
        popoverVc.modalPresentationStyle = .Custom

        // 4.设置转场的代理
        popoverVc.transitioningDelegate = self

        // 弹出控制器
        presentViewController(popoverVc, animated: true, completion: nil)
```

- 2代理遵守`UIViewControllerTransitioningDelegate`协议, 并实现协议中的方法
- 3在协议中返回自定义控制器`UIPresentationController`

```swift
    ///实现代理方法
    func presentationControllerForPresentedViewController(presented: UIViewController, presentingViewController presenting: UIViewController, sourceViewController source: UIViewController) -> UIPresentationController? {

        return XMGPresentationController(presentedViewController: presented, presentingViewController: presenting)
    }
```

- 4在自定义的`UIPresentationController`里边的`containerViewWillLayoutSubviews`里边改变presentedView的frame

```swift
    // MARK:- 系统回调函数
    override func containerViewWillLayoutSubviews() {
        super.containerViewWillLayoutSubviews()

        // 1.设置弹出View的尺寸
        presentedView()?.frame = CGRect(x: 100, y: 55, width: 180, height: 250)

        // 2.添加蒙版
        setupCoverView()
    }
```
- 5, 如何自定义modal动画?
- 实现`UIViewControllerTransitioningDelegate`中的2个方法, 一个是展示控制器, 还有一个就是dismiss
- 在返回的对象里边要遵守`UIViewControllerAnimatedTransitioning`协议
```swift
// MARK:- 自定义转场代理的方法
extension HomeViewController : UIViewControllerTransitioningDelegate {
    // 目的:改变弹出View的尺寸
    func presentationControllerForPresentedViewController(presented: UIViewController, presentingViewController presenting: UIViewController, sourceViewController source: UIViewController) -> UIPresentationController? {
        return XMGPresentationController(presentedViewController: presented, presentingViewController: presenting)
    }

    // 目的:自定义弹出的动画
    func animationControllerForPresentedController(presented: UIViewController, presentingController presenting: UIViewController, sourceController source: UIViewController) -> UIViewControllerAnimatedTransitioning? {
        isPresented = true
        return self
    }

    // 目的:自定义消失的动画
    func animationControllerForDismissedController(dismissed: UIViewController) -> UIViewControllerAnimatedTransitioning? {
        isPresented = false
        return self
    }
}
```

- 6, 然后遵守`UIViewControllerAnimatedTransitioning`并实现里边的方法
    - 一个是动画的持续时间
    - 二是自定义动画
        - 在自定义动画方法里边需要手动添加到containerview,并且告诉动画上下文的动画执行完毕

```swift
// MARK:- 弹出和消失动画代理的方法
extension HomeViewController : UIViewControllerAnimatedTransitioning {
    /// 动画执行的时间
    func transitionDuration(transitionContext: UIViewControllerContextTransitioning?) -> NSTimeInterval {
        return 0.5
    }

    /// 获取`转场的上下文`:可以通过转场上下文获取弹出的View和消失的View
    // UITransitionContextFromViewKey : 获取消失的View
    // UITransitionContextToViewKey : 获取弹出的View
    func animateTransition(transitionContext: UIViewControllerContextTransitioning) {

        isPresented ? animationForPresentedView(transitionContext) : animationForDismissedView(transitionContext)
    }

    /// 自定义弹出动画
    private func animationForPresentedView(transitionContext: UIViewControllerContextTransitioning) {
        // 1.获取弹出的View
        let presentedView = transitionContext.viewForKey(UITransitionContextToViewKey)!

        // 2.将弹出的View添加到containerView中
        transitionContext.containerView()?.addSubview(presentedView)

        // 3.执行动画
        presentedView.transform = CGAffineTransformMakeScale(1.0, 0.0)
        presentedView.layer.anchorPoint = CGPointMake(0.5, 0)
        UIView.animateWithDuration(transitionDuration(transitionContext), animations: { () -> Void in
            presentedView.transform = CGAffineTransformIdentity
            }) { (_) -> Void in
                // 必须告诉转场上下文你已经完成动画
                transitionContext.completeTransition(true)
        }
    }

    /// 自定义消失动画
    private func animationForDismissedView(transitionContext: UIViewControllerContextTransitioning) {
        // 1.获取消失的View
        let dismissView = transitionContext.viewForKey(UITransitionContextFromViewKey)

        // 2.执行动画
        UIView.animateWithDuration(transitionDuration(transitionContext), animations: { () -> Void in
            dismissView?.transform = CGAffineTransformMakeScale(1.0, 0.00001)
            }) { (_) -> Void in
                dismissView?.removeFromSuperview()

                // 必须告诉转场上下文你已经完成动画
                transitionContext.completeTransition(true)
        }
    }
}
```

###封装AFNetworking

- 单例
- 闭包的灵活应用

```swift
// 定义枚举类型
enum RequestType : String {
    case GET = "GET"
    case POST = "POST"
}

class NetworkTools: AFHTTPSessionManager {
    // let是线程安全的
    static let shareInstance : NetworkTools = {
        let tools = NetworkTools()
        tools.responseSerializer.acceptableContentTypes?.insert("text/html")

        return tools
    }()
}

// MARK:- 封装请求方法
extension NetworkTools {
    func request(methodType : RequestType, urlString : String, parameters : [String : AnyObject], finished : (result : AnyObject?, error : NSError?) -> ()) {

        // 1.定义成功的回调闭包
        let successCallBack = { (task : NSURLSessionDataTask, result : AnyObject?) -> Void in
            finished(result: result, error: nil)
        }

        // 2.定义失败的回调闭包
        let failureCallBack = { (task : NSURLSessionDataTask?, error : NSError) -> Void in
            finished(result: nil, error: error)
        }

        // 3.发送网络请求
        if methodType == .GET {
            GET(urlString, parameters: parameters, progress: nil, success: successCallBack, failure: failureCallBack)
        } else {
            POST(urlString, parameters: parameters, progress: nil, success: successCallBack, failure: failureCallBack)
        }

    }
}
```

###OAuth授权

- 开发者创建应用后会获得2个参数
- App Key：`3377518170`
- App Secret：`c66ad551a940e0bee79f44a98bb0387f`
- 授权回调页：`http://www.itcast.cn`
- 取消授权回调页：`https://www.baidu.com`

- 根据文档的url发送请求`https://api.weibo.com/oauth2/authorize`
- `client_id` true string 申请应用时分配的AppKey。
- `redirect_uri` true string 授权回调地址，站外应用需与设置的回调地址一致，站内应用需填写canvas page的地址。
- 拼接 `https://api.weibo.com/oauth2/authorize?client_id=3377518170&redirect_uri=http://www.itcast.cn`
- 进入制定的登陆界面

- 用户在指定的登陆界面登陆后, 新浪服务器会回调指定网页并在网页网址后边添加code
`http://www.itcast.cn/?code=69752d88dcc3eaff9f0689cfcf5334c1`

- `code=69752d88dcc3eaff9f0689cfcf5334c1`

- 根据code对应的接口去获得accesstoken



### 自动填充js

```swift
        // 1.书写js代码 : javascript / java --> 雷锋和雷峰塔
        let jsCode = "document.getElementById('userId').value='1606020376@qq.com';document.getElementById('passwd').value='haomage';"
```

### 封装网络工具类的接口

```swift
// MARK:- 请求AccessToken
extension NetworkTools {
    func loadAccessToken(code : String, finished : (result : [String : AnyObject]?, error : NSError?) -> ()) {
        // 1.获取请求的URLString
        let urlString = "https://api.weibo.com/oauth2/access_token"

        // 2.获取请求的参数
        let parameters = ["client_id" : app_key, "client_secret" : app_secret, "grant_type" : "authorization_code", "redirect_uri" : redirect_uri, "code" : code]

        // 3.发送网络请求
        request(.POST, urlString: urlString, parameters: parameters) { (result, error) -> () in
            finished(result: result as? [String : AnyObject], error: error)
        }
    }
}
```
### 重写对象的description

```swift
    // MARK:- 重写description属性
    override var description : String {
        return dictionaryWithValuesForKeys(["access_token", "expires_in", "uid"]).description
    }
```

### 将对象转成字典

```swift
    NSDictionary *dict = @{@"name" : @"why", @"age" : @18, @"height" : @1.88};

    Person *p = [[Person alloc] init];
    [p setValuesForKeysWithDictionary:dict];

    NSDictionary *dict1 = [person dictionaryWithValuesForKeys:@[@"name", @"age", @"height"]];
    NSLog(@"%@", dict1);

```





















