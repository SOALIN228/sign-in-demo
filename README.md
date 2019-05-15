# sign-in-demo
学习Cookie

## Cookie特点

1. 服务器通过 Set-Cookie 响应头设置 Cookie
2. 浏览器得到 Cookie 之后，每次请求都要带上 Cookie
3. 服务器读取 Cookie 就知道登录用户的信息
4. Cookie 存在有效期，默认20分钟左右，看浏览器
5. Cookie 不安全，可以手动改



## 登录流程

1. 用户打开sign_up注册，发送post请求到后台
2. 后台将接收数据写入数据库，返回注册成功给前端
3. 用户打开sign_in登录，发送post请求到后台
4. 后台验证通过，将cookie写入浏览器
5. 用户在访问首页时，就会带上cookie
6. 后台读取首页请求时接收到cookie，将数据库对应的信息写入页面，响应给用户

