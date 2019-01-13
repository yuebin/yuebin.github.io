---
title: HTTP
sidebar: mydoc_sidebar
permalink: mydoc_http.html
folder: mydoc
---

### HTTP

知道URL的同学都知道，URL是一种在网络上资源的一个标识。HTTP，是获取资源的协议。全名就是 超文本传输协议（HyperText Transfer Protocol).
下图是访问http://tv.cctv.com的网络抓包。我们主要从TCP层看看到底发生了一些什么。  
图1：  
!["所有抓包"](./images/1-2-kl-all-protocol-m1.png)  
图2：  
!["所有抓包"](./images/1-2-kl-http-all-m1.png)  

从图2可以清晰的看到，HTTP协议是基于TCP的，每次HTTP请求都要先建立TCP连接，然后在进行HTTP协议的传输。  

1. 事务
2. 方法
3. 状态码
4. 隧道
5. keep-alive
6. 报文
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

#### 方法
HTTP方法

#### 状态码
HTTP的状态码

#### 隧道



{% include links.html %}
