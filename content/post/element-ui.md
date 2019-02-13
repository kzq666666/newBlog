---
title: "Element Ui"
date: 2018-12-04T21:47:47+08:00
showDate: true
draft: false
tags: ["element-ui","轮子库"]
---

之所以用别人造好的轮子，就是觉得自己的设计水平很差，脑子也没有很多的样式储备，写出来的样式有点丑，于是乎就想用一用类似BootStrap、uiket等轮子库，借鉴一下。这里就先学习了一下element-ui，，看！别人的轮子又大圆~
### 基本介绍
Element，一套为开发者、设计师和产品经理准备的基于 Vue 2.0 的桌面端组件库
现在是vue3.0，估计一段时间之后就会变成3.0了，相应的改动也会更新

### Vue-cli@3.0使用element-ui
作为一个插件添加到vue-cli中
```bash
vue create el
cd el
vue add element
```
安装element插件过程中会有交互，是全部导入，还是按需求导入，我是选择按需求导入，这样比较方便，也比较轻。
<br>成功之后就可以看到你的vue-cli初始页面就会有一个element-button


```vue
element.js
import Vue from 'vue'
import { Button } from 'element-ui'
import 'element-ui/lib/theme-chalk/index.css'
Vue.use(Button)
```
<div style="color:red;font-size:16px">tip：一定要导入对应你需要的css样式，这样才有用,index.css是theme-chalk下所有的css入口文件，如果只想单独使用某个css，找到那个css导入就好了</div>

### 选择你需要的轮子
[官网](http://element.eleme.io/#/zh-CN/component/installation)有很详细的介绍和样式预览，选择需要的，然后使用就好了，对于很好的样式可以看一看具体css怎么实现的，增加一些自己写css的能力

### FAQ
* vue使用element-ui的el-input监听不了回车事件解决
<br>在后面加个native
<br>@keydown.enter.native

