---
title: "VScode配置C环境"
date: 2018-11-27T18:39:26+08:00
showDate: true
draft: false
tags: ["vscode","C环境"]
---
需要写一些关于C的实验报告，老师给的VC++6.0感觉很难用(字体小而且难看)，于是乎就想用我经常用的vscode编辑器来写C，上网百度了一些教程，搞了半天都没怎么搞懂里面的配置，于是自己就捣鼓了一哈。

* 在vscode下载C/C++(Microsoft)扩展
* 下载编译器[tdm-gcc](http://tdm-gcc.tdragon.net/download)(windows),其他编译器具体请看对应的官网，我觉得这个比较容易装就装了这个。
安装成功会自动到将tdm-gcc的bin路径加入到windows的path变量中，如果没有则自己手动添加一下

基本上做完上面两步就可以了
直接在终端输入gcc file.c -o file.exe就编译好了。
<br>
<br>还有一种简单的方法就是在VScode中安装一个扩展插件--Code Runner,这是一个可以运行C，C++，java，JS，PHP，Python的一个插件,安装好了重新加载一下就会看到在VScode右边出现一个运行的按钮,不过默认是在输出下运行，不过输出是一个只读编辑器,所以如果有scanf需要输入的话就不能做了。这时候改下Code Runner的配置，使它运行在Terminal。
<br>
<br>文件-->首选项-->设置-->用户设置-->扩展-->Code Runner Configuation-->勾选✔Run in Terminal
<br>
<br>还有一个问题就是运行C的时候中文在Terminal中使会乱码的，这是因为cmd自身编码的问题,
解决办法是终端或者在CMD.exe中进入到当前文件目录下输入`chcp`(CHCP是一个计算机指令，能够显示或设置活动代码页编号),
默认应该是936简体中文，所以需要改为utf-8，utf-8代码页编号是65001，输入`chcp 65001`就好了

