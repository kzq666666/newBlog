+++
title = "CSSDemo"
date = 2019-05-23T16:11:03+08:00
draft = false

tags = ['CSS','demo']
+++

### 水波效果

 <style>
        .waterWaves{
            position: relative;
            width: 200px;
            height: 200px;
            border: 1px solid #999;
            border-radius: 50%;
            text-align: center;
            line-height: 100px;
            margin: 100px auto;
            animation: wave linear infinite;
            overflow:hidden;
        }
        .wave1{
            position: absolute;
            width: 200%;
            height: 200%;
            background:skyblue;
            opacity: 0.4;
            left: -50%;
            top: 50%;
            border-radius: 180px;
            animation: inherit;
            animation-duration: 7s;
        }
        .wave2{
            position: absolute;
            width: 200%;
            height: 200%;
            background:skyblue;
            opacity: 0.6;
            left: -30%;
            top: 60%;
            border-radius: 45%;
            animation: inherit;
            animation-duration: 10s;
        }
        .wave3{
            position: absolute;
            width: 200%;
            height: 200%;
            background:skyblue;
            opacity: 0.8;
            left: -50%;
            top: 55%;
            border-radius: 45%;
            animation: inherit;
            animation-duration: 7s;
        }
        @keyframes wave{
            0%{
                transform: rotate(0deg);
            }
            100%{
                transform: rotate(360deg);
            }
        }
    </style>
<div class="waterWaves" >
  <div class="wave1" ></div>
  <div class="wave2"></div>
  <div class="wave3"></div>
  WaterWave
</div>
主要利用子元素的旋转实现，具体代码如下
```html
<div class="waterWaves">
  <div class="wave1"></div>
  <div class="wave2"></div>
  <div class="wave3"></div>
  WaterWave
</div>
```

```css
.waterWaves {
  position: relative;
  width: 200px;
  height: 200px;
  border: 1px solid #999;
  border-radius: 50%;
  text-align: center;
  line-height: 100px;
  margin: 100px auto;
  animation: wave linear infinite;
  overflow: hidden;
}
.wave1 {
  position: absolute;
  width: 200%;
  height: 200%;
  background: skyblue;
  opacity: 0.4;
  left: -50%;
  top: 50%;
  border-radius: 180px;
  animation: inherit;
  animation-duration: 7s;
}
.wave2 {
  position: absolute;
  width: 200%;
  height: 200%;
  background: skyblue;
  opacity: 0.6;
  left: -30%;
  top: 60%;
  border-radius: 45%;
  animation: inherit;
  animation-duration: 10s;
}
.wave3 {
  position: absolute;
  width: 200%;
  height: 200%;
  background: skyblue;
  opacity: 0.8;
  left: -50%;
  top: 55%;
  border-radius: 45%;
  animation: inherit;
  animation-duration: 13s;
}
@keyframes wave {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
```
