# property-total


```swift

= 存储属性
    /// 授权AccessToken
    var access_token : String?
    /// 过期时间-->秒
    var expires_in : NSTimeInterval = 0.0

= 单利
    // let是线程安全的
    static let shareInstance : NetworkTools = {
        let tools = NetworkTools()
        tools.responseSerializer.acceptableContentTypes?.insert("text/html")
        return tools
    }()

    // MARK:- 将类设计成单例
    static let shareIntance : UserAccountViewModel = UserAccountViewModel()

= MARK:- 自定义构造函数
    init(dict : [String : AnyObject]) {
        super.init()

= didSet的监听
    /// 过期时间-->秒
    var expires_in : NSTimeInterval = 0.0 {
        didSet {
            expires_date = NSDate(timeIntervalSinceNow: expires_in)
        }
    }
    /// 过期日期
    var expires_date : NSDate?

= 懒加载属性
    // MARK:- 懒加载属性
    lazy var visitorView : VisitorView = VisitorView.visitorView()
    // MARK:- 懒加载属性
    private lazy var titleBtn : TitleButton = TitleButton()

    lazy var iconImageView: UIImageView = {

        let imageView = UIImageView(image: UIImage(named: "avatar_default"))
        imageView.layer.cornerRadius = (imageView.image?.size.width)! * 0.5


        return imageView
    }()
= MARK:- 计算属性
    var accountPath : String {
        let accountPath = NSSearchPathForDirectoriesInDomains(.DocumentDirectory, .UserDomainMask, true).first!
        return (accountPath as NSString).stringByAppendingPathComponent("accout.plist")
    }
    var isLogin : Bool {
        if account == nil {
            return false
        }
    }

   var defaultViewController : UIViewController? {
        let isLogin = UserAccountViewModel.shareIntance.isLogin
        return isLogin ? WelcomeViewController() : UIStoryboard(name: "Main", bundle: nil).instantiateInitialViewController()
    }

= MARK:- 重写init()函数
    init () {
        // 1.从沙盒中读取中归档的信息
        account = NSKeyedUnarchiver.unarchiveObjectWithFile(accountPath) as? UserAccount
    }

= 闭包属性
var callBack : ((presented : Bool) -> ())?


= 自定义构造函数
    // 注意:如果自定义了一个构造函数,但是没有对默认构造函数init()进行重写,
    那么自定义的构造函数会覆盖默认的init()构造函数
    init(callBack : (presented : Bool) -> ()) {
        self.callBack = callBack
    }


= 注意:在闭包中如果使用当前对象的属性或者调用方法,也需要加self
    // 两个地方需要使用self : 1> 如果在一个函数中出现歧义 2> 在闭包中使用当前对象的属性和方法也需要加self
    private lazy var popoverAnimator : PopoverAnimator = PopoverAnimator {[weak self] (presented) -> () in
        self?.titleBtn.selected = presented

    }
```
