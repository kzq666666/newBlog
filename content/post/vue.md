---
title: "Vue"
date: 2018-12-04T18:21:14+08:00
showDate: true
draft: false
tags: ["vue"]
---

### 坑
在使用axios拦截器的时候，在vue-router的钩子函数created是不会触发的

### scroll
在写websocket网页版聊天时，有个需求时每次发消息，scroll都要定位在最下面，刚开始我是监听一个data里message数据的变化，每次有消息的时候，元素的scrollTop=元素的scrollHeight，但每次都是滚动条都定位在最底下的上一条消息上，因为每有一个消息，我就push到message的数组里面，然后页面自动渲染，也就是在最后一条消息渲染完成前就完成了滚动条的移动，所以导致每次都差一条消息的位置。解决办法就是监听dom的变化，
使用this.$nextTick()，dom变化后再进行滚动条的移动

### 只能点击一次事件
v-click.once="clickOnce"

