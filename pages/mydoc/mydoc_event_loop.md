---
title: 事件循环
tags: [事件循环]
keywords: 事件循环
sidebar: mydoc_sidebar
permalink: mydoc_event_loop.html
folder: mydoc
---
```
 事件循环，这部分内容主要在HTMLStandard中有描述，似乎不属于JavaScript的部分，但是了解这部分对于写出更加优秀的代码以及处理问题非常有帮助。
```


#### 事件循环
  为了协调事件，用户的交互，脚步的执行，浏览器渲染，网络请求等，浏览器使用了事件循环这个特性来处理这些任务。事件循环有两种，浏览器上下文与worker。
  一般情况下，我们理解的是一个iframe为一个运行时，里面至少包含一个事件循环。不同的的event loop可以通过 postMessage来完成通讯。
#### 
关于动画的优化网络上有很多示例，这里只记录关键信息。另外附一个CSS的样式[触发器](https://csstriggers.com/)表用来查询样式修改会引起那些动作。


{% include links.html %}
