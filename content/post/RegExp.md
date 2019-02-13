---
title: "RegExp"
date: 2019-01-23T17:51:53+08:00
showDate: true
draft: false
tags: ["正则表达式"]
---
Regular Expression

### 正则表达式：匹配特殊字符或有特殊搭配原则的字符的最佳选择
### 创建方式
* 直接量
* new RegExp();

```js
// 直接量
var reg = /abc/ ;
// new RegExp();
var reg = new RegExp(pattern. attribute);
var reg = new RegExp("abc","i")
var reg = new RegExp(/abc/i);
```

### 修饰符
/i  ignoreCase 忽视大小写
<br>
/g  global   全局匹配
<br>
/m  multiline   多行匹配  
### 常用方法
```js
str.match(reg)  // 返回匹配成功的结果数组
str.search(reg) // 返回匹配到的位置，匹配不到返回-1
str.split(reg)
str.replace(reg, newStr/function(){})
reg.test(str)   // 匹配返回true，不匹配则返回false
reg.exec()      // 
```
### 常用规则

```js
\w ==> [0-9A-z_]
\W ==> [^\w]
\d ==> [0-9]
\D ==> [^\d]
\s ==> [\n\f\r\t\v] 空白字符
\S ==> [^\s]
\b ==> 单词边界     /\bc/  以c开头的单词
\B ==> 非单词边界
.  ==> [^\r\n]
+  ==> 匹配一次到无数次 {1, infinity}
*  ==> 匹配0次到无数次  {0, infinity}
?  ==> 匹配0到1次   {0,1}
^  ==> 开头
$  ==> 结尾
|  ==> 或
() ==> 子表达式
\1 ==> 反向引用第一个子表达式一次
()\1 ==> 反向引用第一个子表达式一次
()\1\1\1 ==> 反向引用第一个子表达式两次
```
### 匹配原则：贪婪匹配原则（能匹配最多的）
如果要打破贪婪匹配就在量词后面加上？，则是非贪婪匹配
### 正则表达式的属性
reg.global      ==> 是否全局匹配
<br>
reg.ignoreCase  ==> 是否忽略大小写
<br>
reg.multiline   ==> 是否有换行匹配
<br>
reg.source      ==> 返回正则表达式的文本
<br>
reg.lastIndex ==> 返回游标位置
### 正向预查 正向断言
?=/!=   ==>断言表达式
<br>
```js
var reg = /a(?=b)/g      // 选择后面是b的a
```
### Practice
#### 1. 检验一个字符串首尾是否含有数字
```js
var reg = /^\d | \d$/;
```
#### 2. 将一个字符转换成小驼峰式写法
```js
var str = "the-first-name";
var reg = /-(\w)/g;
str.replace(reg,function($,$1){
    return $1.toUpperCase();
})
```
#### 3. 字符串去重
```js
var str = "aaaaaaaaaabbbbbbbbbbbbcccccccccc"
var reg = /(\w)\1*/g;
str.replace(reg,"$1");
```
