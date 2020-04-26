### Object基础知识摘要

1.  Object.create(null) 创建的对象`[[Protottype]]`属性为null，这导致对象没有valueOf,toString,constructor方法。英雌无法静心去哪告知类型的转换，但是可以当做Map来使用。
2.  +(-)运算符的医院形式是显示的类型转换。如 var c="3.14"; var d = 5 + +c;//8.14
3. JavaScript中，如果构造函数没有参数，可以不用带()，于是会看到 var timesamp= + new Date;这只对构造函数使用。不适用函数调用。
4.  在JavaScript中 ~可以当做 -(x + 1);此时，只有 x = -1 时，值为0；如果在数组中的indexOf中，我们可以使用 ~arr.indexOf("x")；来当做判断条件。
5. `==`和`===` 都会检测操作数的类型。区别在于操作数的类型不同时他们的处理方式不同。扩展规则:  
    - 1). 如果Type(x)是数字，Type(y)是字符串，这放回 x === ToNumber(y); 
    - 2). 如果Type(x)是字符串。Type(y)是数字，则返回 ToNumber(x) == y. 
    - 3). 如果Type(x)是布尔类型，则返回 ToNumber(x) == y;
    - 4). 如果Type(y)是布尔类型，则返回 x == ToNumber(y);
    - 5). 如果Type(x)是字符串或者数字，Type(y)是对象，这返回 x === ToPrimitive(y)的结果。
    - 6). 如果Type(x)是对象，Type(y)是字符串或则数字，则返回 ToPrimitive(x) == y的结果。
6. 在JavaScript中，关系比较满意严格关系比较，如果有 `a<=b`则会处理为`b < a`，然后取反。