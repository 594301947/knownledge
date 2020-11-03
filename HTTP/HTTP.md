### HTTP

超文本传输协议，用于在web浏览器传输文本

- 为什么HTTP使用TCP不使用UDP？
  - HTTP要求很高，不能随便出错，使用TCP能保证可靠传输，与此同时TCP能提供流量/拥塞控制

- Chrome浏览器，采用多线程/多进程？
  - 多进程。因为如果采用多线程，一个浏览器页面挂掉，所有的页面都有挂掉的风险，采用多线程，不能保证不出意外

#### HTTP请求报文

- 请求方法 请求URL HTTP协议以及版本号，如：POST /chapter17/user.html HTTP/1.1

- 报文头

- 报文体

#### HTTP响应报文

- HTTP协议以及版本号 状态码 状态码描述，如：HTTP/1.1 200 OK
- 响应头
- 响应体

##### 请求方法

GET：获取URI资源（返回所有信息，包括报文首部、报文体）

HEAD：只获取报文首部，不获取报文体（用于确认URI的有效性、资源更新的日期）

POST：传输报文主体，一般用于更新

PUT：传输文件，保存到URI指定的位置

DELETE：删除文件，与PUT方法相反

TRACE：追踪路径，查询发送出去的请求的中转路径

CONNECT：要求与代理服务器通信时，建立隧道，实现用隧道协议进行TCP通信（主要使用SSL/TLS）

OPTIONS：查看该URI支持哪些请求方法



#### HTTP特点

- 无连接：一请求，一连接。即：每次请求都会建立连接，请求完成后，就断开连接
- 无状态：不保存上次请求的状态信息

HTTP上面的2个特点，会带来缺点，即：每次请求不会保持上一次的状态，比如，在购物网站中，如果用户登录了信息，在点击下一个网页后，连接将会断开，需要重新再次输入账号/密码登录，这样十分麻烦。因此引入了HTTP-keepalive保持连接，Cookie、Session保存状态

- keepalive
  - 持久连接：减少连接/断开的次数，降低消耗
  - 只要某一端没有明确提出断开连接，就会保持TCP连接状态

- Cookie
  - 保存在客户端
  - 客户端向服务端发起请求后，服务端会生成Cookie返回给客户端；客户端之后将会保存Cookie；当再次访问时，将会把Cookie放在报文头中传给服务端；服务端收到Cookie后，解析Cookie，发现这个请求是客户端A发来的，就直接可以向客户端A回复响应
- Session
  - 会话，保存在服务端
  - 比如：XShell，在第一次登录时，会生成Session，保存起来，它是保存在服务端的内存中

#### 状态码

- 1XX 信息状态码，接收的请求正在被处理中
- 2XX 成功状态码，请求处理成功
  - 200 处理成功
  - 204 处理成功，返回内容不包含主体，No content
  - 206 处理成功，返回部分主体，partial content
- 3XX 重定向状态码
  - 301 永久重定向，旧的URL地址资源被永久移除了，转移到新的URL地址
  - 302 临时重定向，旧的URL地址仍然存在，该重定向临时跳转到新的URL地址
  - 307 临时重定向（暂时性转移），如果请求不是GET/HEAD，浏览器禁止自动重定向
  - 304 Not Modify（缓存），客户端连续多次请求相同的URL资源，后请求的将会直接从缓存中获取
- 4XX 客户端发来错误的请求
  - 400 请求保存存在语法问题
  - 401 发送的请求需要HTTP认证
  - 403 没有权限，拒绝访问
  - 404 没有资源
- 5XX 服务端出问题，不能处理请求
  - 500 Internal Server Error，服务器处理请求时，发生错误
  - 503 Service Unavailable，服务不可达，可能是因为服务器负载过高or正在停机维护



---

### HTTPS

HTTPS = HTTP + 加密 + 认证 + 完整性校验，HTTPS是身披SSL外壳的HTTP。采用SSL后，HTTP就拥有了加密、证书、完整性校验的特性

#### HTTP、HTTPS的区别

- 是否明文传输：SSL/TLS建立安全通信线路
- 是否验证对方身份：SSL证书
- 是否验证报文完整性：MD5/RSA/数字签名

关于加密的应用场景举例：一般在下载软件的时候，经常会提供一个MD5检验值。当下载完软件后，可以计算该软件包MD5值，判断是否相等来判断该软件包是否正确。

#### 公钥加密/私钥加密

- 共享公钥加密（对称加密）
  - 双方采用相同的密钥对数据加密
  - 缺点：公钥要在网络中传播，存在被盗的危险
- 公开密钥加密（非对称加密）
  - 公钥是公开的，所有人都可以拿到公钥。
  - 私钥只有主人持有
  - 其他人将数据采用公钥进行加密，发送给持有私钥的主人，主人通过私钥解密

非对称加密也是有一个小的风险，就是：公钥是否是正确的，是否是货真价实的？如果公钥是假的，那么，用假公钥加密后的数据将会泄漏。因此，引出了“CA数字证书认证机构”，它会颁发证书，证明公钥的权威性。



---

### HTTP2.0

