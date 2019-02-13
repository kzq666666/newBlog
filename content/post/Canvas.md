---
title: "CSS3 Canvas"
date: 2018-10-31T18:52:17+08:00
showDate: true
draft: false
tags: ["CSS","Canvas"]
---

Canvas 是 HTML5 新增加的一个元素,它又称为"画布",主要有以下四种功能

- 绘制图形
- 绘制图表
- 动画效果
- 游戏开发

在 chrome 浏览器中,canvas 的默认宽高是 300px 和 150px,写宽高的样式的时候最好写在 HTML 页面的属性值里面

```html
<canvas width="150" height="100" style="border: 1px black dashed"></canvas>
```

一般的操作
<br>1.获取 canvas 对象
<br>2.获取上下文环境对象 context

```js
cxt = canvas.getContext("2d");
```

3.开始绘制图形

### 1.直线

```js
cxt.moveTo(x1,y1)   画笔移到(x1,y1)处
cxt.LineTo(x2,y2)   画笔从起点(x1,y1)开始画线,一直到终点(x2,y2)处
cxt.strokeStyle = "red"     设置线的颜色
cxt.stroke()        用笔划线
(tip:cxt.strokeStyle要在cxt.stroke()之前执行,否则是看不到效果的,和画画是一样的,在动笔之前把要画的东西,颜色,样式确定好
```

### 2.描边矩形 填充矩形 清空矩形

* 描边矩形

```js
cxt.strokeRect(x1,y1,x2,y2)     (x1,y1)为矩形左上角坐标,(x2,y2)为矩形右下角坐标
等价于==>
cxt.rect(x1,y1,x2,y2);
cxt.stroke();
```

* 填充矩形

```js
cxt.fillStyle = "属性值"
cxt.fillRect(x1,y1,width,height) (x1,y1)是矩形左上角坐标,width是矩形的宽度,height是矩形的高度
等价于==>
cxt.rect(x1,y1,x2,y2);
cxt.fill()
```

* 清空矩形

```js
cxt.clearRect(x1, y1, x2, y2);
```

* 绘制一个正 n 多边形

```html
  <canvas width="100" height="50" style="border: 1px black dashed"></canvas>
    <script>
        var canvas = document.getElementsByTagName('canvas')[0]
        var cxt = canvas.getContext('2d');      //获取上下文环境对象
        var cvs_width = parseFloat(getComputedStyle(canvas, null).width);   //获取画布的宽
        var cvs_height = parseFloat(getComputedStyle(canvas, null).height); //获取画布的高
        var distanceR = distanceD = 0 
        function createPolygon(n) {
            var r = Math.min(cvs_width, cvs_height)/2;  //正多边形外接圆半径
            if(Math.min(cvs_width,cvs_height)==cvs_height){
                distanceR = (cvs_width/2) - r
            }else{
                distanceD = (cvs_height/2) - r
            }
            var degree = (2 * Math.PI) / n;     //每个角的度数
            cxt.moveTo(0+distanceR, r+distanceD);   //初始化起点
            for (let i = 1; i < n; i++) {
                cxt.lineTo(r - r * Math.cos(i * degree)+distanceR, r + r * Math.sin(i * degree)+distanceD);
            }
            cxt.closePath();
            cxt.fillStyle = "#f40";
            cxt.fill()
        }
    </script>
```
### 2.曲线
* 圆形

```js
cxt.beginPath() 开始一个路径
cxt.arc(x,y,半径,开始角度,结束角度,anticlockwise)
// (x,y)时圆心的坐标,开始角度和结束角度都是弧度制,anticlockwise(逆时针地)为true时,逆时针绘制图形,为false时,顺时针绘制图形
cxt.closePath() 结束一个路径
// 描边
cxt.strokeStyle = "颜色值" 
cxt.stroke()  画线
// 或者填充
cxt.fillStyle()
cxt.fill()
```
* 弧形

``` js
1.arc() 
// 和画圆基本语法一样,就是把cxt.closePath()去掉就好了
2.arcTo(cx,cy,x2,y2,radius)
// 控制点坐标(cx,cy) 终点坐标(x2,y2) radius是圆弧半径 起点坐标(x1,y1)由一般由moveTo()或lineTo()提供
``` 
* 二次贝塞尔曲线

```js
cxt.quadraticCurveTo(cx,cy,x2,y2)
// (cx,cy)控制点坐标,(x2,y2)终点坐标,起点坐标由moveTo()或lineTo()提供
```
* 三次贝塞尔曲线

```js
cxt.bezierCurveTo(cx1,cy1,cx2,cy2,x,y)
//(cx1,cy1)控制点1的坐标,(cx2,cy2)控制点2的坐标,(x,y)表示结束点坐标,起点坐标由moveTo()或lineTo()提供
```
### 3.线条操作
```js
lineWidth   
//线条宽度(px)
lineCap     
//线帽样式 Butt默认值无键帽,Round圆形键帽,Square正方形键帽
lineJoin    
//线条交接处样式 miter默认值尖角,round圆角,bevel斜角
```






### canvas应用实例
#### （1）星光闪闪
先上效果
<img src="/starBG.png" style="box-shadow:1px 1px 15px grey">
```html
  <canvas id="myCanvas"></canvas>
  <script>
    // 获取画布
    var myCanvas = document.getElementById('myCanvas');
    // 画笔
    var ctx = myCanvas.getContext('2d');
    // 创建一个列表存放位置信息
    var list = [];
    // 初始化画布
    function init(){
      myCanvas.width = window.innerWidth;
      myCanvas.height = window.innerHeight;
    }
    init();
    // 每当窗口大小变化的时候重新初始化
    window.onresize = init;
    // 初始化位置
    for(let i=0; i<777; i++){
      // 圆点的位置
      var x = Math.random() * myCanvas.width;
      var y = Math.random() * myCanvas.height;
      // 圆的半径
      var r = Math.random() * 5;
      // 圆的偏移量,发散的移动，以中间为界限，左上的向左上角移动，右上的向右上角移动，左下向左下角移动，右下向右下角移动
      var disX = x - myCanvas.width / 2;
      var disY = y - myCanvas.height / 2;
      list.push({
        x:x,
        y:y,
        r:r,
        disX:disX,
        disY:disY
      });
    }
    // 绘制函数
   function render(){
     // 每次都把画布更新
     ctx.clearRect(0,0,myCanvas.width,myCanvas.height);
     for(var i=0;i<list.length;i++){
       var item = list[i];
       // 圆点移动
       item.x += item.disX / 50;
       item.y += item.disY / 50
       // 判断小圆点消失
       if(item.x < 0 || item.y<0 ||item.x>myCanvas.width || item.y > myCanvas.height){
         // 每次消失重新生成圆点
         item.x = Math.random() * myCanvas.width;
         item.y = Math.random() * myCanvas.height;
         item.disX = item.x - myCanvas.width/2;
         item.disY = item.y - myCanvas.height/2;
       }
       // 开始绘制
       ctx.beginPath();
       // 填充颜色
       ctx.fillStyle = "rgb("+random(0,255)+','+random(0,255)+','+random(0,255)+')';
       // 绘制圆
       ctx.arc(item.x,item.y,item.r,0,Math.PI*2,false);
       ctx.fill();
     }
     // 每40毫秒重新绘制
     setTimeout(render,40);
   }
   render();
   function random(left,right){
     return Math.random() * (right-left+1) + left
   }
  </script>
```
