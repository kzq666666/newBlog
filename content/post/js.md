+++
title = "JS"
date = 2019-04-27T09:14:09+08:00
draft = false
+++

### Console
console.time和console.timeEnd统计一段代码运行时间
```js
console.time('total time');
for(let i = 0;i<1000;i++){};
console.timeEnd('total time')
// total time: 0.072ms
```
