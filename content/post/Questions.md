---
title: "Q && A"
date: 2018-11-16T10:01:19+08:00
showDate: true
draft: false
tags: ["Question"]
---

 
### 1. return !1 和 return false 以及 return 0! 和 return true写法有什么区别
```js
tween.min.js的源码
update: function(c) {
        if (0 === a.length) return !1;
        for (
          var b = 0, d = a.length, c = void 0 !== c ? c : Date.now();
          b < d;

        )
          a[b].update(c) ? b++ : (a.splice(b, 1), d--);
        return !0;
      }
```

### 2. void 和 undefined 有什么区别(详细请看[这里](https://segmentfault.com/a/1190000000474941))
A : void是一种操作符,无论void后的表达式是什么，void操作符都会返回undefined.但undefined不是[`保留字`](https://baike.baidu.com/item/%E4%BF%9D%E7%95%99%E5%AD%97),undefined可以作为变量使用,所以在使用undefined作为变量名的时候容易出错,因此使用void可以确保取到undefined值
```js
function x() {
   var undefined = 'hello world',
       f = {},
       window = {
           'undefined': 'joke'
       };
   console.log(undefined);// hello world
   console.log(window.undefined); //joke
   console.log(f.a === undefined); //false
   console.log(f.a === void 0); //true
}
```
* void还有一个经常使用到的作用,就是在a标签的href中使用,填充href,使它不跳转而是进行一些交互,比如在许多网站中的收藏,快转功能.

``` html
<a href="javascript:void(0)">
```

* 生成一个空的src的img标签的最好的方式似乎是使用`src="javascript:void(0)"`
<br>详情请看[What's the valid way to include an image with no src?](https://stackoverflow.com/questions/5775469/whats-the-valid-way-to-include-an-image-with-no-src)

<br> Tip : 关于此问题更加详细请看[这里](https://segmentfault.com/a/1190000000474941)

### 3.null!=a 和 a!=null的区别
### 4.常见的获取元素宽高的方式及其区别
* dom.style.width/height 
  <br>这种方式只能获取dom元素`内联样式`的宽高，而style标签的样式和外联样式使获取不到的。修改样式用这个还是可以的
* dom.currentStyle.width/height 
  <br>无论哪种样式都可以获得，不过只有IE浏览器支持(我亲测了chrome和firefox都是不兼容的)。只读
* window.getComputedStyle(element,[preudoElt]).width/height
  <br>首先getComputedStyle(element,[preudoElt])返回的是一个实时的css属性对象preudoElt是伪元素(可选),对于普通元素就是设置为null即可。兼容性更好(IE、firefox、chrome都可以)。只读
* dom.offsetWidth/offsetHeight 
  <br>兼容性很好，常用，且返回值是数字，不带单位。只读
* dom.getBoundingClientRect().width/height
  <br>getBoundingClientRect()返回的是一个元素的绝对位置的DomRect对象，里面有top、bottom、left、right、width、height,IE不兼容getBoundingClientRect(),IE兼容getClientRects(),其他浏览器都兼容，返回值是数值，不带单位。只读

<br>以上，个人觉得offsetWidth比较方便一些
### 5.window.onload和$(document).ready()方法的区别
A：window.onload事件会在页面所有元素加载完成后立即发生。而$(document).ready()是在DOM树加载完毕之后对其进行操作

### 6.v-if和v-else使用应该注意什么？
* 他们必须是兄弟节点！！！
* v-else上一个节点必须是v-if！！！
  
### 7. 常见的水平居中的方法？
* text-align:center;  (具有文本特性的元素水平居中,display为inline或者为inline-block)
* margin:0 auto (块级元素，且自身要有宽度)
* position:left;left:50%;margin-left:-元素高度/2;     (元素高度已知)
* position:left;left:50%;transform:translateX(-50%); (元素高度未知)
* display:flex;justify-content:center;         

### 8. 常见的垂直居中的方法？
### 9. 常见的水平垂直居中的方法？
### 10. calc使用注意事项
运算符前后必须要有空格，如calc(100% - 20px);
### 11. background-size中cover和contain有什么区别
两者都是等比例缩放。
<br>cover：如果容器的宽高比和照片的宽高比不同，那么图片就会等比例缩放到塞满整个容器，图片多余的部分就会被裁剪
<br>contain：图片等比列缩放至全部都展示出来，所以可能会有留白
### 12. js中关系运算符中大于和小于是怎么比较的？
* 字符串和字符串比较，比较第一个不同的字符的ASCII码
* 数字和纯数字字符串比较，将纯数字字符串转换为数字比较
* 数字和非纯数字字符串比较，返回false
* 特殊字符 null 和 undefined 进行比较的时候，null == undefined，undefined和除了null的其他所有值进行比较都是false

```js
// 关系运算符 和 相等运算符 并不是一个类别的.
// 关系运算符,在设计上,总是需要运算元尝试转为一个number . 而相等运算符在设计上,则没有这方面的考虑.
// 最重要的一点, 不要把 拿 a > b , a == b 的结果 想当然的去和 a >= b 建立联系. 正确的符合最初设计思想的关系是 a > b 与 a >= b是一组 . a == b 和其他相等运算符才是一组. 比如 a === b , a != b, a !== b .
null > 0 // null尝试转型为number，则为0，所以结果是false
null >=0 // null尝试转型为number，则为0，所以结果是true
null == 0 // null在设计上不尝试转型，所以结果是false
```
关于null的问题，参考了关于这个问题的回答=>[传送门](https://www.jb51.net/article/106370.htm)

### 13.JS引擎中对变量的查询方式LHS和RHS有什么区别？
LHS和RHS是JS引擎的两种查找方式，赋值操作的左侧和右侧
<br>LHS：找到目标，对其赋值，赋值操作的目标
<br>RHS：找到源头，得到ta的原值，赋值操作的源头
<br>不同的查找方式结果不一样，如果查找到最顶层的全局作用域下也没有找到变量的话，RHS查找就会抛出异常，而LHS查找方式在非严格模式会在全局作用域隐式的创建该变量，而严格模式则一样会抛出ReferenceError（ES5推出的严格模式不允许自动或者隐式的创建变量）
<br>简单的说就是，如果查找的目的是对变量进行赋值，那么就会使用LHS查询，如果目的是获取变量的值，就会使用RHS查询。

### 14.什么是闭包？
当函数可以记住并访问所在的词法作用域，即使函数是在当前词法作用域之外执行，这时就产生了闭包。函数的执行期上下文没有被销毁

### 15.Object.create(null)和{}创建空对象的方式有什么区别？
Object.create(null)创建的对象比{}更‘空’，因为前者是没有创建Object.prototype原型的，而{}则会创建这个原型。

### 16.如何判断this指向？
1.由new调用？绑定到新创建的对象
2.由call或者apply或者bind调用？绑定到指定的对象
3.由上下文对象调用？绑定到那个上下文对象
4.默认：在严格模式下绑定到undefined，非严格模式绑定到全局对象

### 17.什么是事件冒泡和捕获？一个事件的执行顺序是怎样的？
事件冒泡和捕获都是事件的执行顺序，事件捕获是从上到下依次执行，而事件冒泡是从下到上执行。DOM事件流分三个阶段：捕获阶段=> 目标阶段（真正的目标节点正在处理事件的阶段） => 冒泡阶段，就好比猛地将一个瓶子扔到水里，它会下沉一段距离，然后再浮上来。

### 18.什么是事件委托？有什么用？
事件委托是利用事件冒泡的原理，避免过多的操作DOM元素，利用其父级元素完成相应的事件操作。优化页面。

### 19.addEventListener 和 onclick一类 绑定事件有什么区别？
* addEventListener可以给一个事件绑定不同的监听器，而onclick一类只能一个事件只能绑定一个，同时绑定多个会覆盖。
* addEventListener更加灵活，可以选择事件执行顺序是冒泡（第三个参数为false）还是捕获（第三个参数为true）

### 20. __proto__ 和 prototype有什么区别？
### 21. instanceof的用法？
### 22. 常见js迭代器？
* forEach
* some
* every
* for...in
遍历索引
* for...of
遍历元素

### 23.LF 和 CRLF 换行符有什么不同?
#### 一些题目
1 关于this指向
```js
// this指向的是调用它的对象，如果没有直接调用对象，会指向undefined或者window，一般都会指向window，在严格模式下才会指向undefined
function a(xx){
  this.x = xx;
  return this;
};
var x = a(5);  // window.x = 5 , return this,  x = window
var y = a(6);  // window.x = 6 , return this,  y = window
console.log(x.x); // x = 6 , x.x => undefined
console.log(y.x); // y = window , widow.x = 6

// -----------------分割线-----------------------
var name = '222';
var a = {
  name:'111',
  say:function(){
    console.log(this.name);  //谁调用this就指向谁
  }
}
var fun = a.say;   
fun();   // this指向window, this.name = '222'
a.say(); // this指向a, this.name = '111'
var b = {
  name:'333',
  say:function(fun){
    fun();
  }
}
b.say(a.say);  
// say:function(fun){
//    this;这里的this指向b
//    fun();  fun里面的this是在预编译过程中指向window的
//}
// 所以这里的this.name = '222'
fun()   // this指向window, this.name = '222'
b.say = a.say;  
b.say();   // this.name = '333'

// -------------------分割线--------------------
function Point(x, y){
  this.x = x;
  this.y = y;
  this.moveTo = function(x, y){
    this.x = x;
    this.y = y;
    console.log(this.x + "," + this.y);
  }
}
var p1 = new Point(0,0);
var p2 = {x:0,y:0};
p1.moveTo(1,1); // 1,1
p1.moveTo.apply(p2,[10,10]); // 10,10

// -------------------分割线---------------
var num = 10;
var obj = {
  num:0,
  inner:{
    num:6,
    print:function(){
      console.log(this.num);
    }
  }
}
num = 88; // 全局num变为88
obj.inner.print() // 6
var fn = obj.inner.print;
fn(); // 88
(obj.inner.print)(); // 6
(obj.inner.print = obj.inner.print)(); // 0
```