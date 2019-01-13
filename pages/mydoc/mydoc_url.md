---
title: URL
sidebar: mydoc_sidebar
permalink: mydoc_url.html
folder: mydoc
---

### URI

对，你没有看错是URI不是URL，URI（Uniform Resource Identifier URI）统一资源标识。他就想你的某宝邮寄地址一样。主要用来定位的。我们在互联网上可以访问的所有资源都有对应的URI。
但是我们的URI会分为两种，URL与URN。URL是通过描述资源的位置来标识资源的。URN则是通过名字来识别资源的，它与当前所处位置无关（虽然HTTP协议将URI作为资源标识，但实际HTTP服务器是处理了URL这个子集）以后这两个东西不要傻傻的分不清了。

### URL
 URL 统一资源定位符。URL一般由以下9个组件：
 ```
 <schemem>://<user>:<password>@<host>:<port>/<path>;<params>?<query>#<frag>
 ```
 其中主要的就是”方案（scheme）“，”主机（host）“，”路径（path）“这三部分了（面试一般能说上着3个就够了）。下表是各个部分的详细说明。

组件|描述|默认值
-- |--  |--
scheme|说明使用什么协议|无
user|用户|匿名
password|用户对应的密码|无
host|资源服务器的地址，客户是域名或者IP|无
port|端口，如你的Tomcat默认的8080|不同的方案有不同的默认端口
path|服务器上资源的本地名，想一下现在流行的RESTful|无
params|参数有键值对组成，相互之间以及与其余部分可以用分号（;）分隔。|无
query|查询组件内容没有通用的格式，用字符？将它与其他部分分隔。|无
frag|它用来表示一个片段，这部分是在客户端使用的，通过#将其余其他部分分隔。**这部分是不会发送给服务器的。**|无







{% include links.html %}
