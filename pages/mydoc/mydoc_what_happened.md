---
title: 发生了什么
sidebar: mydoc_sidebar
permalink: mydoc_what_happened.html
folder: mydoc
---

## 发生了什么

其实现在互联网是无处不在，例如当我们在浏览器输入http://tv.cctv.com (本来想使用百度或者某宝，但是现在全站换成https了，所有就用cctv来举例，关于[https](./mydoc_https.html)，我在后面写到HTTP的隧道的时候会详解)时，具体发生了一些什么呢！如图1-1：
![what_happened](./images/1-1.png "what_happened")
---
1. 用户输入[URL](./mydoc_url.html)后，从[DNS](https://baike.baidu.com/item/%E5%9F%9F%E5%90%8D%E7%B3%BB%E7%BB%9F/2251573)获取了tv.cctv.com域名对应的IP地址。
2. 获取IP地址后，从http://tv.cctv.com获取协议为[HTTP](./mydoc_http.html)。
3. 由于tv.cctv.com后面没有带端口号，故使用80端口进行访问。
4. 访问目标服务并建立[TCP](mydoc_tcp.html)通讯。
5. 客户代理给Web服务器发送一条HTTP的GET请求。
6. 服务器获取请求后，将对应的数据输出。
7. HTTP的一次事务完成，断开网络连接。
8. 代理根据HTTP返回的报文信息[解析处理数据](mydoc_agent.html)。
9. 代理最终显示Web服务器返回的数据。



{% include links.html %}
