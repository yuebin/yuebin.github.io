---
title: 实现一个简易MVVM
tags: [MVVM]
keywords: MVVM
sidebar: mydoc_sidebar
permalink: tow_way_binging_ts.html
folder: mydoc
---
在将MVVM之前，我们先说说Web的简单历史。

在早期的网站开发中，其实是没有前端这么明确的一个岗位的，大部分都是有开发人员来直接完成的，而在Java横行的网络时代，其以[Struts2](https://struts.apache.org/)最为著名，其Struts2采用MVC的设计模式，大致如下图：
![URL TO DOM](./images/struts2.png "URL TO DOM")  


struts2最明显的一点及时将业务逻辑与ServletAPI直接分离。简单理解就是在Servlet收到请求后，将对应的请求在ActionMapper中匹配，好到对应的Action后，执行其Action，然后将返回一个Result,Result通过Template处理后，通过Response返回到用户。MVC大致如下：  

![URL TO DOM](./images/mvc.png "URL TO DOM") 


但是这种开发模式一直持续到2010年左右，前端涌现出了一些比较纯粹的MVC框架，但是很多人对这些框架并不满足，其中有Misko Hevery 和 Facebook分别为代表的AngularJS与React最为影响大，其中React在13年5月左右才开源，而AngularJS在Google收购后，已经在内部部分项目中得到了很好的实践。这些框架将模板功能，数据模板等全部放在前端，后台只需要通过Ajax来完成数据的提交与查询即可。从而使在开发Web移动影响时将大幅度的减少由于CURD操作来带来的大量重复代码。

这些框架最明显的一个就是通过`\/{\/{expression/\}\/}`来实现数据模板的展示绑定，通过`x-model`方式来实现对输入的绑定。

在下面的例子中，我将用最少的代码，最简易的方式来实现以下上面的两个功能。

```

class Parse {

    parse(template, dataSet) {
        let regExp = /\{\{\w+\}\}/g;
        if (template) {
            return template.replace(regExp, function (match, index, template) {
                if (match) {
                    let variable = match.replace(/\{\{/, "").replace(/\}\}/, "");
                    if (dataSet && dataSet.hasOwnProperty(variable)) {
                        return dataSet[variable];
                    } else {
                        return "";
                    }
                }
            });
        } else {
            return "";
        }
    }
}

let pageData = {
    message: "Hello world!"
};
let parse = new Parse();

window.addEventListener('load',function(){
    //1,查找模板
    //2,替换模板值
    let template = document.getElementById("messageTemplate");
    let html = parse.parse(template.innerHTML, pageData);
    document.querySelector("#app").innerHTML = html;
});

document.addEventListener("input",function(event){
    let newValue = event.target.value;
    let target = event.target;
    let moduleTemplate = target.getAttribute("u-model");
    pageData[moduleTemplate] = target.value;

    let template = document.getElementById("messageTemplate");
    let html = parse.parse(template.innerHTML, pageData);
    document.querySelector("#app").innerHTML = html;
    
});

var getValue = function(parent,key){
    if(parent && parent.hasOwnProperty(key)){
        return parent[key];
    }else{
        return "";
    }
}
```

HTML代码
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Two-way binding stage 4</title>
</head>
<body>
    <h3>stage 4</h3>
    <div id="app">
        
    </div>

    <script src="./index.js"></script>
    <script type="template/text" id="messageTemplate">
        <div>
            <div>模板数据展示: {{message}}</div>
            <div>
                <input type="text" value="" name="message" u-model="message"/>
            </div>
        </div>
    </script>
</body>
</html>
```
#### 实现思路
1. 在html通过 `<script type='template/text' id='templateId'>`定义一个模板。
2. 添加load事件，在load万成后，先将template获取到，然后通过Pares将模板解析，替换里面的对应绑定的值。
3. 解析完成后，将解析完的代码通过`innerHTML`替换到界面。
4. 浏览器添加了`input`事件，如果有`input`事件触发。检测input事件触发的元素是否有`u-model`属性，如果有，需要取值，更新数据状态。
5. 数据发生变化后，重新渲染界面。

#### 问题 
  通过上上面步骤可以完成一个简易的MVVM的样子。但是这个里面涉及到了几个比较重要的问题，我们可以思考一下。
1. 页面数组状态`pageData`是全局的。
2. 每次数据更新都要替换整个页面。
3. 模板替换使用`innerHTML`，替换后，光标状态丢失。
4. 事件监听使用`input`是否合适，是否可以输入拼音。

git地址 [https://github.com/yuebin/TwoWayBinding](https://github.com/yuebin/TwoWayBinding)

{% include links.html %}