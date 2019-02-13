---
title: "ES6"
date: 2019-01-04T11:03:38+08:00
showDate: true
draft: false
tags: ["ES6"]
---

### let 和 const

ES6 新加了两种声明变量的方式，一个是 let，一个是 const。

- let 和 const 声明变量有自己的块级作用域（在 for 循环中用 let 声明的变量不会泄露到外部）
- let 和 const 声明变量在预编译的过程都不会进行变量提升
- let 和 const 声明的变量不能再次声明，而 const 声明变量的时候必须同时赋值，并且不能再次赋值

```js
{
    console.log(a); // ReferenceError:a is not undefined
    let a;
}
{
    let a = 1;
    let a = 2; // SyntaxError: Identifier 'a' has already been declared
}
{
    const a; // SyntaxError:Missing initializer in const declaration
}

{
    const a = 1;
    a = 2 // TypeError:Assignment to constant variable
}
```

### 模板字面量

- 创建字符串不必再拼接了~

```js
let a = {
  str: "模板字面量"
};
console.log("ES6" + a.str);
// ES6
console.log(`ES6${a.str}`);
```

- 换行直接按下键盘的 Enter 就可以了

```js
console.log("ES6\n模板字面量");
// ES6
console.log(`ES6
模板字面量`);
```

### 默认参数

```js
function defalutPerson(person = "kzq") {
  console.log(`The person is ${person}`);
}
defalutPerson();
defalutPerson("HH");
```

### 箭头函数

- ES6 的箭头函数简化了函数的语法

```js
var plus = function(a, b) {
  return a + b;
};
// ES6箭头函数
var plus = (a, b) => {
  return a + b;
};
// 或者这样
var plus = (a, b) => a + b;
```

- 箭头函数的 this 指向是固定的，即在箭头函数声明的时候就定义好了，继承来自外部最近的 this 指向

```js
var x = 7;
var obj = {
  x: 77,
  print: function() {
    console.log(this.x);
  }
};
obj.print(); // obj调用的，则this指向obj，77

var obj = {
  x: 77,
  print: () => {
    console.log(this.x);
  }
};
obj.print(); // print是箭头函数，在声明的时候this就指向obj内部的this指向window，7

function test() {
  this.x = 7777;
  let print = function() {
    console.log(this);
  };
  print();
}
test(); // 全局调用this指向window，7

function test() {
  this.x = 7777;
  let print = () => {
    console.log(this);
  };
  print();
}
test(); // 箭头函数print，print在定义的时候this就指向test，7777
```

### 解构赋值

```js
var info = {
  name: "kzq",
  age: 20,
  sex: "male"
};
var { name, age } = info;
console.log(name, age);

var [, , lastNum] = [1, 2, 3];
```

### 扩展运算符(...)

```js
// 合并数组
var person1 = ["kzq", "lzj", "hmy", "dcb"];
var person2 = ["hh", "hqy", "xxbb", "xx"];
var person = [...person1, ...person2]; // person2.push(...person)

// 复制
var a = [1, 2, 3];
var oppA = [...a].reverse();

// 解构赋值
let { name1, name2, ...remainName } = { name1: "kzq", name2: "hh", name3: "wq", name4: "xx" };
console.log(name1); // "kzq"
console.log(name2); // "hh"
console.log(remainName); // {name3:"wq", name4:"xx"}
```

### Object.assign 实现浅复制

```js
var newObj = Object.assign(targetObj, sourceObj); // 把sourceObj复制给targetObj并返回targetObj
```
