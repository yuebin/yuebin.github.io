---
title: 浏览器渲染
tags: [浏览器渲染过程]
keywords: 解析，HTMP Parse
sidebar: mydoc_sidebar
permalink: mydoc_agent.html
folder: mydoc
---
```
 这里我们以WebKit为主进行分析，其他浏览器内核基本与此相同
```
#### 浏览器
浏览器我们都知道，就是在输入一个[URL](./mydoc_url.html)后，将URL变化成一个可视化，可操作的页面。在这个过程中，浏览器到底都有哪些模块，怎样完成这样一个效果的呢？  
我们按照浏览器数据流的流向，可以将上述这个过程分成三个阶段。  
1. 从网页的URL到构建完DOM树。
2. 从DOM树到构建完绘制上下文。
3. 第三个阶段是从绘制上下文到生成最终的图像。


#### 从网页的URL到构建完DOM树
![URL TO DOM](./images/ulr_to_dom.png "URL TO DOM")  

1. 用户输入URL后，调用资源类加载器加载改URL对应的网页。
2. 加载器依赖网络模块建立连接，发送请求并接受应答。
3. 接受到各种网页或者资源数据，这些资源有可能是同步的，又有可能是异步的。
4. 网页被交给HTML解析器变成一系列的词语（Token）
5. 解析器根据词语构建节点，形成DOM树。
6. 如果节点是JavaScript代码，调用JavaScript引擎并执行。
7. JavaScriptdiam可能会修改DOM树的结构。
8. 如果节点需要依赖其他资源，如图片，CSS，视频等，调用资源加载器来加载它们。但是它们是异步的。不会阻塞当前DOM树的继续创建；如果是JavaScript资源URL(没有标记 async活defer)。则需要停止当前DOM树的创建，直到JavaScript的资源加载并被JavaScript引擎执行后才继续DOM树的创建。

在上面这个过程中，有个非常重要的一点就是DOMConent事件和DOM的“onload"事件。这两事件分布发生在DOM树构建完之后，以及DOM树构建完，并且网页所依赖的资源都加载完之后才发生。完成上的系列操作后，接下来就是利用CSS和DOM树构架RenderObject树再到绘制上下文。

#### 从DOM树到构建完绘制上下文
![DOMTree to RenderObject](./images/css_dom_render_object.png "DOMTree to RenderObject") 

1. CSS文件被CSS解释器解释成内部表示结构
2. CSS解释器工作完成之后，在DOM树上附加解释后的样式信息，这既是RenderObject树。
3. RenderObject节点在创建的同时，WebKit会根据网页的层次构建RenderLayer树，同时构建一个虚拟的绘图上下文。


#### 从绘制上下文到生成最终的图像
构建为绘制上线文后，接下来就是根据绘制上下文生成最终图像了。这个主要依赖2D和3D图形库。如下图：  
![RenderObject to view](./images/render_content_view.png "RenderObject to viewqsz")  

上面就是浏览器渲染的三个组要阶段。通过上面的分析，我们可以知道在DOM构建的过程中需要执行JavaScriptdiam，所以需要特别注意在DOM未构建完成是，不能访问DOM，对DOM进行操作。


{% include links.html %}
