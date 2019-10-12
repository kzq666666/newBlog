+++
title = "前端常用知识点复习"
date = 2019-10-12T15:43:28+08:00
draft = false
+++

## HTML
#### html5特性
- 增加了canvus画布
- 增加了用于视频播放的video和音频的audio，可以直接在页面播放视频和音频而不需要任何的插件
- 增加了许多语义化的标签，header、article、footer等等
- 增加了用于本地离线存储的localStorage和sessionStorage
## CSS
#### 盒模型
- 标准盒模型(content-box):height = content
- IE合模型(border-box):height = content +  padding + border
#### 水平居中和垂直居中一些方式
- (水平)行内元素：text-align：center;line-height:父元素高度
- (水平)块级元素：margin：0 auto; 
- (垂直)：display:table-cell;vertical-align:middle;
- (水平垂直)已知高度：position:absolute;left:50%;top:50%;margin-left:自身宽度的一半;margin-top:-50%;
- (水平垂直)未知高度：position:absolute;left:50%;top:50%;transform:translate(-50%,-50%)
- (水平垂直)未知高度position:absolute;left:0;right:0;top:0;bottom:0;margin:auto;
- (水平垂直)未知高度display:flex;justify:center(水平居中);align-items:center;(垂直居中)

#### 什么是BFC？怎么理解
- BFC(Block Formatting Context):块级格式上下文；它规定块级元素内部如何布局
- 内部定位方案： 
  - 内部的盒子按垂直方向一个接一个


## JS
## VUE

## 网络
#### TCP和UDP的区别和优缺点
- TCP和UPD都是传输层的TCP/IP网络协议的，作用都是用来传输和接受数据
- TCP面向连接的，通讯之前必须保证双方连接上，三次握手。UDP面向无连接的，通讯之前不需要连接
- TCP能保证数据可靠和顺序性。UDP则不能保证，传输过程会出现丢包现象
- TCP复杂些，报文字节数多。UPD简单快速，报文字节少

## 浏览器
- Chrome：webkit/blink
- Safari: webkit
- IE：Trident
- FireFox：Gecko
- Opera：Presto

