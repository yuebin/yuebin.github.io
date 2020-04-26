---
title: 类型转换
tags: [MVVM]
keywords: JavaScript基础
sidebar: mydoc_sidebar
permalink: type_conversion.html
folder: mydoc
---
#### 类型转换

  &emsp;&emsp;JavaScript是若类型的，这个我们都知道，那在这种代码中`var a = 3, b= '43'; a == b`的判断中，将会将会发生类型转换，但是类型转换的具体规则是什么呢。他们是通过什么来完成的。
  &emsp;&emsp;在JavaScript中，有一类操作，我们称之为"抽象值操作"（即“仅供内部使用的操作”）。这儿主要介绍ToString，ToNumber，ToBoolean，[ToPrimitive](https://www.w3.org/html/ig/zh/wiki/ES5/%E7%B1%BB%E5%9E%8B%E8%BD%AC%E6%8D%A2%E4%B8%8E%E6%B5%8B%E8%AF%95#ToPrimitive)。

### 1. ToString `String(x)`
- ToString在将非字符串到字符串的转换的时候用到。对于普通对象来说，除非自己定义了，否则toString返回调用的是Object.prototyp.toString方法。
```
var o1 = Object.create(null); //没有Object.prototype
o1.a = "abc";
var o2 = {a:"abc"};
String(o2);//正常显示： [object Object]
String(o1);// TypeError
```
- JSON字符串工具 JSON.stringify 首先调用`toJSON()`（他返回正常的Object）.如果没有重写，则在JSON.stringify在遇到 undefined,function,symbol时会自动忽略。
- 在`a + ''`计算中，根据`ToPrimitive`抽象操作规则，先会调用a的`valueOf`方法，然后通过ToString抽象操作返回的值作为字符串，而String(a）则直接调用了ToString();
```
var obj = {
    valueOf:function(){
        return 43;
    },
    toString:function(){
        return "34"
    }
};
console.log(obj + 1);// 44;
console.log(`${obj}`);// 34
String(obj);//34
```


### 2. ToNumber `Number(x)`
先给出一段代码;
```
var a = "a";
a + 1;// "a1"
true + 1;// 2
true - 1;//0
false + 1;//1
false - 1;// -1
undefined -1;// NaN
null - 1; // -1
null + 1;// 1
```
- 从运行结果可以看出  true转换后为 1， false转换后为0，undefined转换为NaN， null转换为0.
- ToNumber对字符串的处理基本遵循数字常量相关的规则/语法。处理识别，返回NaN.
- 对于对象，首先会别转换为对应的基本类型，如果返回的是非数字的基本类型值，则再遵循上面的规则将其强制转换为数字。将对象转换为基本类型，抽象操作ToPrimitive首先检查该值是否有valueOf方法，如果有并且返回了基本类型值，就使用该值进行类型转换。如果没有就是用toString()返回的值来镜像类型转换。如果`valueOf()`与`toString()`都没有返回基本类型，则TypeError。
### ToBoolean `Boolean(x)` 

在ES5规范中列举下面为假值：

- undefined
- null
- false
- +0,-0,NaN
- `""`

除了在假值以外的都为真正，但是`document.all`在IE上除外。
在此需要注意一下boolean的在逻辑比较中的规则：
- `==`和`===` 都会检测操作数的类型。区别在于操作数的类型不同时他们的处理方式不同。扩展规则:  
    - 1). 如果Type(x)是数字，Type(y)是字符串，这放回 x === ToNumber(y); 
    - 2). 如果Type(x)是字符串。Type(y)是数字，则返回 ToNumber(x) == y. 
    - 3). 如果Type(x)是布尔类型，则返回 ToNumber(x) == y;
    - 4). 如果Type(y)是布尔类型，则返回 x == ToNumber(y);
    - 5). 如果Type(x)是字符串或者数字，Type(y)是对象，这返回 x === ToPrimitive(y)的结果。
    - 6). 如果Type(x)是对象，Type(y)是字符串或则数字，则返回 ToPrimitive(x) == y的结果。
- 在JavaScript中，关系比较满意严格关系比较，如果有 `a<=b`则会处理为`b < a`，然后取反。
 ```
  var a = {b:42};
  var b = {b:43};
   a < b;//false
   a == b;//false
   a > b; //false

   a <=b; //true
   a >= b; //true
 ```



   



{% include links.html %}