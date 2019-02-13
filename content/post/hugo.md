---
title: "Hugo"
date: 2018-10-30T09:11:33+08:00
showDate: true
draft: false
tags: ["tool"]
---

#### [Hugo](http://www.gohugo.org/)是由Go语言实现的静态网站生成器。简单、易用、高效、易扩展、快速部署。我的博客网站就是通过Hugo来进行部署的,感谢Hugo,让我不需要重复造轮子.
官网:http://www.gohugo.org/
<br>
### 1.下载
直接下载安装包 https://github.com/gohugoio/hugo/releases

### 2.安装
windows10:解压安装包,会生成一个exe文件,在windows系统变量中添加当前路径到path.这样就算是安装成功了,之后都是在终端直接运行

### 3.创建一个站点
```
hugo new site path/siteName 
在path路径下生成一个叫siteName的站点
```
站点目录结构:
```
sitname
├── archetypes
│   └── default.md
├── config.toml     配置文件
├── content         存放主要内容的目录
├── data            
├── layouts
├── static
└── themes          主题目录
```
### 4.创建一篇文章
```
hugo new  posts/blog.md 
在content目录下生成posts/blog.md  
```
### 5.下载主题和配置
url : https://themes.gohugo.io/
###### (1)下载<br>这些主题都托管在GitHub上,可以直接用git的下载方式下载
```
cd themes/  进入themes目录
. git clone + 对应主题的地址
  在readme.md中,作者会有对应git命令操作
  
. 直接在release最新发布版本中下载包 
``` 
###### (2)配置
可以直接将下载的主题目录里面的 exampleSite/config.toml复制到站点根目录下覆盖初始化的config.toml文件
<br>( tip:注意config.toml文件中启用的主题名字是否和主题目录名一样,sam主题就是不一样的,不然就会加载主题失败 )
<br>sam主题 ( https://themes.gohugo.io/hugo-theme-sam/ ) , 一个简约舒适的主题
### 6.启动项目及部署
```
(1)启动本地服务
▶ hugo server (--theme=<themeName>如果有多个主题可以进行选择)
一般在本地的1313端口运行 
localhost:1313 or 127.0.0.1:1313

(2)部署到服务器中
▶ hugo 
会生成一个public的文件,如果要部署到服务器只要将该目录放到服务器之中
(类似于vue-cli的npm run build会生成一个dist目录的静态文件)
```










