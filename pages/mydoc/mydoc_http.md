---
title: HTTP
sidebar: mydoc_sidebar
permalink: mydoc_http.html
folder: mydoc
---

### HTTP

URL是一种在网络上资源的一个标识。HTTP，是获取资源的协议。全名就是 超文本传输协议（HyperText Transfer Protocol).
下图是访问http://tv.cctv.com的网络抓包。我们主要从TCP层看看到底发生了一些什么。  
图1：  
!["所有抓包"](./images/1-2-kl-all-protocol-m1.png)  
图2：  
!["所有抓包"](./images/1-2-kl-http-all-m1.png)  

从图2可以清晰的看到，HTTP协议是基于TCP的，每次HTTP请求都要先建立TCP连接，然后在进行HTTP协议的传输。  

1. 事务
2. 报文
3. 方法
4. 状态码
5. keep-alive
6. cookie
7. session
8. Web缓存

#### 事务
图2其实是完成一个完整的HTTP请求的全过程。我们把这个过程在HTTP协议叫做一个事务。这个图中的每一条连线就是一个报文，前三个为TCP层的三次握手，在TCP层建立连接后，客户代理发起了一次GET请求，然后服务器端通过两个报文来将数据传输到客户代理，最后发起关闭请求。服务器关闭TCP连接。网络层次如图1右边部分。

 协议 | OSI |
:--:|:--:|
HTTP|应用层
TCP |传输层
IP  |网络层
链路接口|数据链路层
物理网络硬件|物理层

#### 报文
![HTTP报文](./images/baowen_02.png "HTTP报文")  
图3  
![HTTP报文](./images/baowen_response_03.png "HTTP报文")  
图4  
此截图为TCP层的截图，看中间部分，他就是一个HTTP协议的报文。所有的HTTP的报文可以分为两类：请求报文和响应报文。  
请求报文：向Web服务器请求一个动作。  
响应报文：将请求的结果返回给客户端。  
图3为请求报文。图4为响应报文。
```
请求报文格式：
<method> <request-URL> <version>
<headers>

<entity-body>
```

```
响应报文格式：
<version> <status> <reason-phrase>
<headers>

<entity-body>
```
+ method:方法;
+ request-URL:请求URL；
+ version：版本；
+ status：状态码；
+ reason-phrase：原因短语；
+ header：首部；
+ entity-body：实部主题；
实体部分不是所有的都有。
#### 方法
 HTTP报文的起始行就是方法。方法是用来告知服务器要做些什么。如图3中的”GET /afarmer/arichive/2011/08/29/2158860.html HTTP/1.1“中，就是GET方法。下表为HTTP规范中定义的一些常用的方法：  

方法名|说明|是否包含主体
:--|:--|:--:
GET|从服务器获取文档|否
POST|向服务器发送需要处理的数据|是
HEAD|只从服务器获取文档的首部|否
PUT|将请求的主体部分存储到服务器上|是
TRACE|对可能经过代理服务器传送到服务器上去的报文进行跟踪|否
OPTIONS|决定可以在服务器上执行那些方法|否
DELETE|从服务器上删除衣服文档|否

#### 状态码
方法是用来告诉服务器要干什么，状态码则是告诉代理发生了什么情况。如图4 HTTP/1.1 200 OK中，200就是状态码。下面是HTTP规范对状态码的一个分类，由三位数字来表达。  


整体范围|已定义范围|分类
:--|:--|:--
100~199|100~101|信息提示
200~299|200~206|成功
300~399|300~305|重定向
400~499|400~415|客户端错误
500~599|500~505|服务器错误


关于HTTP的状态码的具体分类，可以参考《HTTP权威指南》.这里简要说明几个比较常见的状态码。 


状态码|原因短语|含义
:--:|:--:|:--
200|OK|请求没有问题，实体的主体部分包含了所有的请求资源。
301|Moved Permanently|在请求的URL已移除，响应的Location首部中应该包含资源现在所处的URL。
304|Not Modified|客户端可以通过所包含的请求首部，使其请求变成有条件的。如客户端发起了一个GET请求。而最近资源未被修改的话，就可以用这个状态码来说明资源未被修改。带有这个状态码的响应不应该包含实体的主体部分。
400|Bad Request|用于告知客户端它发送了一个错误的请求
401|Unauthorized|客户端未获取对资源的访问权。
404|Not Found|用于说明服务器服务找到请求的URL。通常会包含一个实体，以便客户端应用程序显示给用户看。
405|Mehod Not Allowed|发起的请求中带有所请求的URL不支持的方法时，使用此状态码。
500|Inernal Server Error|服务器遇到一个妨碍它为请求提供服务的错误时，使用此状态码。
501|Not Implemented|客户端发起的请求超出了服务器的能力范围时使用此状态码。如使用了服务器不支持的方法。  

#### keep-alive
由于HTTP是在TCP层的，每次请求HTTP都需要进行TCP层的三次握手。而在一般的HTTP中，这个耗时就会话费50%以上的时间。再次由于TCP层具有慢启动的特性(TCP连接会随着时间进行自我”调谐“，期初会限制连接的最大速度，用于防止因特网的突然过载和拥塞)，一般一个网页会有多次的HTTP请求，如果每次都重新建立TCP，然后再传输的话，很明显性能会有问题，再次，由于操作系统的2MSL问题。会导致服务器端的连接率不会高于500次/秒。所以为了解决这些问题，HTTP协议规定，可以在HTTP请求都Connection中增加Keep-alive使用一个TCP来接来完成多个HTTP事务。 
![KEEP-ALIVE](./images/http_304_get_request_01.png "KEEP-ALIVE") 图5  
同一个TCP连接上，完成5次HTTP事务。 

#### cookie
Cookie技术是用来识别客户端的一种技术。我们知道HTTP的无状态的。即HTTP访问结束后，会关闭掉当前连接。这样服务器就没有办法知道具体客户端是谁了。为了解决这个问题。网景公司开发Cookie技术。后来被大多浏览器使用。  
Cookie主要分为两类：会话Cookie和持久Cookie。会话Cookie是一种临时Cookie，浏览器退出时，会话Cookie就会别删除了。持久Cookie的生存时间更长一些。他存储在硬盘上，浏览器退出，计算器重启它任然存在。  
Cookie会在HTTP请求是，在HTTP头部携带Cookie。如果是第一次访问，服务器会在返回的HTTP中设置Set-Cookie的头，后面是Cookie值。这样服务器就知道这次来访问的就是谁了。

#### session
虽然Cookie中可以存储一些信息，但是有些敏感信息存储在客户端是不安全的。这样就有了对应的Session机制。一般Cookie中有一ID值。通过这个ID值可以找到服务器端对应的Session。这样服务器端程序就可以把一些敏感的信息存储在服务器端。

#### Web缓存
Web缓存是可以自动保存常见文档副本的HTTP设备。当Web请求到达缓存时，如果本地有“已缓存的”副本。就可以从本地存储设备而不是原始服务器去取文档。
HTTP协议中，可以通过GET请求的If-Modified-Since来请求验证服务器当前资源是否在指定的时间之前修改了，如果没有修改，则返回304 Not Modified。如果发生了修改，则返回一条普通的200 OK的响应。如果资源以及被删除，则返回404 Not Found响应。


{% include links.html %}
