---
title: "Tween.js"
date: 2018-11-18T11:22:48+08:00
showDate: true
draft: false
tags: ["tween.js","tween","动画"]
---
#### tween.js - http://github.com/sole/tween.js
JavaScript tweening engine for easy animations, incorporating optimised Robert Penner's equations.
<br>JavaScript补间引擎，可轻松制作动画，并采用优化的Robert Penner方程。
### 1.基本用法(Usage)
```js
// 开始位置
var InitPosition = {x:100,y:0};

// 目标位置
var targetPosition = {x:200,y:0};

// 创建一个开始位置的tween
var tween = new TWEEN.Tween(Initposition);

// 告诉tween需要变换到的位置和时间
tween.to({targetPositon},time);

// 开始这个动画
tween.start();

// 为了使动画尽可能平滑,可以在每次循环的时候更新tween
animate();
function animate() {
    requestAnimationFrame(animate);
    //...
    TWEEN.update();
    //...
}

// 整个变换过程中是不能看到位置的变换的,如果需要可以执行以下代码
tween.onUpdate(function() {
    console.log(this)    
})
```