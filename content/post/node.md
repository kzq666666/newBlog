---
title: "Node"
date: 2018-11-27T17:04:59+08:00
showDate: true
draft: false
tags: ["Node"]
---
开此篇记录下学习node的过程和一些笔记
### Node.js的一些特性
* 基于Chrome的V8引擎
* 事件驱动、非堵塞、单线程
* Node.js是一个非阻塞的系统，当调用一些需要阻塞的等待或者事件，node会采用回调函数替代闲置等待，即事件驱动。就像我们在学校经常吃饭点餐的情况，点完餐之后店家会给个小票，上面有这此点餐的号码，到时候菜做好了就会叫号，这个号码相当于回调号码，这样就提高了效率，继续为下一个客人服务。
* 串行IO和并行IO，类似于同步和异步，前者的运行顺序是固定的，后者任何一个IO操作返回时间都是不确定的，如果IO操作有关联的话就要使用串行IO。按顺序的串行请求，无序的并行的请求

### 模块加载
- require导入
- exports导出

### 核心模块
#### files
```js
// ---------files---------
// Node.js利用流的方式来处理文件
// 引入模块
var fs = require('fs');

// 1.写文件，当前路径下没有就创建一个，如果存在就覆盖
fs.writeFile('./test.txt', '异步写入一些数据', 'utf8', function(err){
    if(err){
        console.log('写入失败')
        throw err
    }else{
        console.log('写入成功')
    }
})

fs.writeFileSync('./test.txt','同步写入一些数据','utf8')

// 2.读文件，如果不加编码类型，则data返回的就是一个buffer缓冲区，里面存有二进制数据
fs.readFile('./test.txt','utf8',function(err, data){
    console.log(data)
})

// 3.追加文件，如果没有则创建一个
fs.appendFileSync('./log.txt', '同步追加，写入时间：'+new Date().toLocaleString()+'\n')

fs.appendFile('./log.txt','异步追加，写入时间：'+new Date().toLocaleString()+'\n',function(err){
    if(err){
        console.log('添加失败')
    }else{
        console.log('添加成功')
    }
})

// 4.监听文件，文件只要修改了就会执行回调函数
fs.watchFile('./log.txt', function(cuur,prev) {
    console.log(prev);
})

// 5.判断文件是否存在，存在返回true，不存在返回false
var res = fs.existsSync('/a');
console.log(res);

fs.exists('./a',function(res){
    if(res){
        console.log('文件存在')
    }else{
        console.log('文件不存在')
    }
})
```
#### http
```js
// --------------http-----------------
var http = require('http');
var fs = require('fs')

// 创建服务
var myServer = http.createServer(function(req, res){
    var reqUrl = req.url=='/'?'./html/index.html':'./html'+req.url;
    if(fs.existsSync(reqUrl)){
        var html = fs.readFileSync(reqUrl);
        res.write(html);
    }else{
        var errPage = fs.readFileSync('./html/404.html');
        res.write(errPage);
    }
    res.end();
})

// 监听
myServer.listen('1313', function(err){
    if (err){
        console.log('监听失败')
        throw err
    }else{
        console.log('服务器已经开启，端口号为：1313')
    }
})
```

#### path
```js
// --------path------------
var path = require('path');

// 当前文件夹路径
console.log(__dirname)

// 当前文件路径
console.log(__filename)

// 路径的字符串拼接
var url = path.join('html', 'index.html');
console.log(url)
```
#### url
- url.parse(urlStr)：返回一个url对象
- url.format(urlObj)：传入一个url对象，返回一个完整的url地址
- url.resolve(from,to)：拼接两个对象或者是字符串url

#### dns
- dns.resolve()：将一个域名解析为指定类型的数组
- dns.lookup()：返回第一个被发现的IPv4或者IPv6的地址
- dns.reverse()

#### Express框架
```js
// --------express框架----------
var express = require('express');
var path = require('path');

// 实例化对象
var app = express();



// 路由传参
app.get('/student/:id', function(req,res){
    var id = req.params.id;
    console.log(id);
})

// 客户端所有请求
app.all('/all', function(req, res){
    res.send('所有的请求都接受了');
})
// 客户端get请求
app.get('/account', function(req, res){
    res.status(200).json({
        code:0,
        data:{
            name:'kzq',
            age:20 
        },
        message:'ok'
        
    })
})
// 设置访问页面(默认index.html)
app.use(express.static(path.join(__dirname,'html')))
app.use('/hello', function(req, res){
    res.status(200).sendFile(path.join(__dirname, 'html', 'hello.html'))
})
app.use('*', function(req, res){
    res.status(404).sendFile(path.join(__dirname, 'html', '404.html'))
})
// 监听端口
app.listen(3000, function(err){
    if(err){
        console.log('监听失败');
        throw err;
    }else{
        console.log('express搭建的服务器已开启，端口号是3000')
    }
})
```
### 文件系统

### 优点与缺点
* 优点/应用场景：数据密集型实时（比如聊天系统、微博之类的）
* 不适合压缩/解压缩，加/解密，模板渲染


