---
title: "Typeof"
date: 2018-11-01T17:52:19+08:00
draft: false
showDate : true
tags: ["JS"]
---
typeof返回一个字符串,表示为经计算的操作数的类型
<br>typeof(操作数)/typeof 操作数  ()是可以省略的
返回有五种基本类型:string,number,boolean,undefined,function,object
还有ES6的Symbol
```js
// 1.string:
typeof('你好')
typeof('123')
typeof('')   // 空字符串也是String类型
typeof(typeof('a'))

// 2.number:
typeof(123);
typeof(NaN);

// 3.boolean:
typeof(true);
typeof(false);
typeof(NaN===NaN) // 强制类型转换

// 4.undefined:
typeof(a)  // 未经使用的变量的数据类型

// 5.object:
typeof(null) // js底层所有值的前三位表示数据类型,object是000,而null的32位全是0,因此也是object
typeof([])
typeof({})

// 6.function:
typeof(function(){})
typeof(new Function())
typeof(class A{})
typeof(Symbol)

// 7.symbol:
typeof(Symbol())
```
#### 暂时性死区
在ES6中let和const出现之前,typeof都是一个完全安全的操作,即不会报错,但有了ES6中let和const的出现所带来的暂时性死区特性,使得typeof也有可能报错

如果在一个块级作用域下存在let或const命令,则它所声明的变量就绑定在这个区域,不再受外部的影响.在声明之前使用这些变量就会报错.使用let命令声明变量之前是不可用的,这在语法上称为`暂时性死区`
```js
typeof(a);   //ReferenceError
let a;
```
