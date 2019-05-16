# sign-in-demo
学习登录一套的流程

## Cookie 4k

1. 服务器通过 Set-Cookie 响应头设置 Cookie
2. 客户端得到 Cookie 之后，每次请求都要带上 Cookie
3. 服务器读取 Cookie 就知道登录用户的信息
4. Cookie 存在有效期，默认20分钟左右，看浏览器
5. Cookie 不安全，可以手动改



## Session

1. 将 SessionID (随机数) 通过 Cookie 发给客户端
2. 客户端访问服务器，服务器读取 SessionID 
3. 服务器有一块内存(哈希表) 保存了所有 session
4. 通过 SessionID 我们可以得到对应用户的隐私信息，如id、email
5. 这块内存 (哈希表) 就是我们服务器上的所以 session



## LocalStorage

1. LocalStorage 和 HTTP **无关**
2. HTTP **不会带上** LocalStorage 的值
3. **相同域名**的页面可以**互相读取** LocalStorage
4. 每个域名 LocalStorage 的最大存储量为 5MB左右
5. 常用场景：**记录**是否提示过用户信息等**不敏感的信息**
6. LocalStorage 永久有效，通过清理缓存来清除



## SessionStorage

1. 同上
2. 同上
3. **相同域名**的页面**不可以**互相读取 SessionStorage
4. 每个域名 SessionStorage的最大存储量为 10MB左右
5. SessionStorage 关闭浏览器后清除




## Cache-Control

后台接口添加下面这句代码，就可以将数据缓存下来

```javascript
response.setHeader('Cache-Control', 'max-age=30000000')
```

在接下来的 30000000 s内**浏览器不会再发起请求**来请求这份资源 ，而是从缓存中读取

当想要更新资源的时候给资源添加一个版本号或随机数即可更新缓存

一般只缓存 CSS 和 JS 不要缓存 HTML,因为HTML是访问的接口，不能缓存



## 登录流程

1. 用户打开sign_up注册，发送post请求到后台
2. 后台将接收数据写入数据库，返回注册成功给前端
3. 用户打开sign_in登录，发送post请求到后台
4. 后台验证通过，将 sessionId 存入后台并将 sessionId 以 cookie 发给浏览器
5. 用户在访问首页时，浏览器就会带上cookie
6. 后台读取首页请求时接收到 cookie 中的 sessionId ，然后进行数据比对将对应的信息写入页面，响应给用户



## 总结

1. Session 依赖于 Cookie 实现

2. Cookie 和 LocalStorage 区别

   LocalStorage 不会被 HTTP 带过去

3. LocalStorage 和 SessionStorage 的区别

   - 存储容量不同
   - 存储时间不同
   - 访问权限不同