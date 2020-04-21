- 一种无状态的、应用层的、以请求/应答方式运行的协议，他使用可扩展的语义和自描述消息格式，与基于网络的超文本信息系统灵活的互动。

- 超文本传输协议（英文：HyperText Transfer Protocol，缩写：HTTP）是一种用于分布式、协作式和超媒体信息系统的应用层协议。HTTP是万维网的数据通信的基础。

#### 请求和响应格式
> 请求行
> 请求头
> 请求体

#### HTTP之状态码：
- 1xx：指示信息--表示请求已接收，继续处理

- 2xx：成功--表示请求已被成功接收、理解、接受

- 3xx：重定向--要完成请求必须进行更进一步的操作

- 4xx：客户端错误--请求有语法错误或请求无法实现

- 5xx：服务器端错误--服务器未能实现合法的请求

#### 常见状态码：
- 200 OK                        //客服端请求成功
- 400 Bad Request               //客户端请求有语法错误，不能被服务器所理解
- 401 Unauthorized              //请求未经授权，这状态代码必须和WWW-Authenticate报头域一起使用
- 403 Forbidden                 //服务器搜到请求，但是拒绝提供服务
- 404 Not Found                 //请求资源不存在，eg:输入了错误的url
- 500 Internal Server ErroRequest//服务器发生了不可预测的错误
- 503 Server Unavailable        //服务器当前不能处理客户端的请求，一段时间后可能恢复正常

#### HTTP请求方法
HTTP1.0 定义了三种请求方法： GET, POST 和 HEAD方法。

HTTP1.1 新增了五种请求方法：OPTIONS、PUT、PATCH、DELETE、TRACE 和 CONNECT 方法。

| 序号 | 方法   | 描述 |
| ----- | --------- | ----------- |
| 1 | GET |请求指定的页面信息，并返回实体主体。             |
| 2  |  HEAD     | 类似于 GET 请求，只不过返回的响应中没有具体的内容，用于获取报头,监控平台是否还是正常连接    |
| 3  |  POST     |向指定资源提交数据进行处理请求（例如提交表单或者上传文件）。数据被包含在请求体中。POST 请求可能会导致新的资源的建立和/或已有资源的修改。   |
| 4  |  PUT     |从客户端向服务器传送的数据取代指定的文档的内容。   |
| 5  |  DELETE     |请求服务器删除指定的页面。   |
| 6  |  CONNECT     |从HTTP/1.1 协议中预留给能够将连接改为管道方式的代理服务器。   |
| 7  |  OPTIONS     |允许客户端查看服务器的性能。   |
| 8  |  TRACE     |回显服务器收到的请求，主要用于测试或诊断。   |
| 9  |  PATCH     |是对 PUT 方法的补充，用来对已知资源进行局部更新 。   |


​	    		    	


#### HTTP响应头信息
| 应答头 | 说明   |
| ----- | --------- |
| Allow | 服务器支持哪些请求方法（如GET、POST等）。 |
| Content-Encoding | 文档的编码（Encode）方法。只有在解码之后才可以得到Content-Type头指定的内容类型。利用gzip压缩文档能够显著地减少HTML文档的下载时间。 |
| Content-Length | 表示内容长度。 |
| Content-Type | **表示后面的文档属于什么MIME类型。**Servlet默认为text/plain，但通常需要显式地指定为text/html。 |
| Date | 当前的GMT时间。 |
| Expires | 应该在什么时候认为文档已经过期，从而不再缓存它？ |
| Last-Modified | **文档的最后改动时间。**客户可以通过If-Modified-Since请求头提供一个日期，该请求将被视为一个条件GET，只有改动时间迟于指定时间的文档才会返回，否则返回一个304（Not Modified）状态。 |
| Location | **表示客户应当到哪里去提取文档。**Location通常不是直接设置的，而是通过HttpServletResponse的sendRedirect方法，该方法同时设置状态代码为302。 |
| Refresh |  表示浏览器应该在多少时间之后刷新文档，以秒计。注意Refresh头不属于HTTP 1.1正式规范的一部分，而是一个扩展，但Netscape和IE都支持它。 |
| Server | 服务器名字。Servlet一般不设置这个值，而是由Web服务器自己设置。 |
| Set-Cookie | 设置和页面关联的Cookie。 |
| WWW-Authenticate | 客户应该在Authorization头中提供什么类型的授权信息？在包含401（Unauthorized）状态行的应答中这个头是必需的。 |

#### Cookie功能特点：
- 存储于浏览器头部/传输于HTTP头部
- 写时带属性，读时无属性
- HTTP头中Cookie: user=bob; cart=books;
- 属性 name/value/expire/domain/path/httponly/secure/…
- 由三元组[name,domain,path]唯一确定cookie




评估web架构的关键属性
1. 性能Performance：影响高可用的关键因素
2. 可伸缩性Scalability：支持部署可以交互的大量组件
3. 简单性： 易理解、易实现、易验证
4. 可见性：对两个组件间的交互进行监视或者仲裁的能力。如缓存、分层设计等
5. 可移植性性：在不同的环境下运行的能力
6. 可靠性：出现部分故障时，对整体影响的程度
7. 可修改性：对系统做出修改的难易程度，由可进化性、可定制性、可扩展性、可配置性、可重构性构成。



性能：

- 网络性能：network 
  - 吞吐量
  - 开销
- 用户感知到的性能：user-perceived
  - 延迟
  - 完成时间
- 网络效率：network 
  - 重用缓存、减少交互次数、cod


#### 5种架构风格
数据流风格 Data-flow Styles
-  优点：简单性、可进化性、可扩展性、可配置性、可重用性


客服端:
<方法> <请求URL> <版本> 
<请求首部>

服务端:
<版本> <状态码> <原因短句> 
<响应首部>


#### Http协议首部字段

a、通用首部字段（请求报文与响应报文都会使用的首部字段）
Date：创建报文时间
Connection：连接的管理
Cache-Control：缓存的控制
Transfer-Encoding：报文主体的传输编码方式
b、请求首部字段（请求报文会使用的首部字段）
Host：请求资源所在服务器
Accept：可处理的媒体类型
Accept-Charset：可接收的字符集
Accept-Encoding：可接受的内容编码
Accept-Language：可接受的自然语言
c、响应首部字段（响应报文会使用的首部字段）
Accept-Ranges：可接受的字节范围
Location：令客户端重新定向到的URI
Server：HTTP服务器的安装信息
d、实体首部字段（请求报文与响应报文的的实体部分使用的首部字段）
Allow：资源可支持的HTTP方法
Content-Type：实体主类的类型
Content-Encoding：实体主体适用的编码方式
Content-Language：实体主体的自然语言
Content-Length：实体主体的的字节数
Content-Range：实体主体的位置范围，一般用于发出部分请求时使用


#### 链接
[HTTP协议详解](https://blog.csdn.net/weixin_34268169/article/details/91437431)
