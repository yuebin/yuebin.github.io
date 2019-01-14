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
3. 状态码
4. 隧道
5. keep-alive
6. 方法
7. cookie
8. session
9. 缓存

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
图1  
![HTTP报文](./images/baowen_response_03.png "HTTP报文")  
图2  
此截图为TCP层的截图，看中间部分，他就是一个HTTP协议的报文。所有的HTTP的报文可以分为两类：请求报文和响应报文。  
请求报文：向Web服务器请求一个动作。  
响应报文：将请求的结果返回给客户端。  
图1为请求报文。图2为响应报文。
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


#### 状态码
HTTP的状态码

#### 隧道

#### keep-live

#### 方法

#### cookie

#### session

#### 缓存



{% include links.html %}
