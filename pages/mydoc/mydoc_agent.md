---
title: 浏览器渲染过程
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

![URL TO DOM](./images/ulr_to_dom.png "URL TO DOM")  


{% include links.html %}
