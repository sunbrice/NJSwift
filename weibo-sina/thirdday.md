# ThirdDay

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
