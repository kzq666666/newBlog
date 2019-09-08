+++
title = "坑"
date = 2019-05-31T16:02:38+08:00
draft = false
+++

### 解决jupyter notebook 运行之后为空页面
1.打开cmd  = >register
<br>
2.找到HKEY_LOCAL_MACHINE\SOFTWARE\Classes\.js
<br>
3.把content Type : text/plain => application/javascript

### electron-builder打包过程的错误
![报错截图](/img/electron-builder-error.png)
在可以科学上网的情况还是出现了该bug，只能选择手动下载对应的包了
，这里报错是要下载winCodeSign-2.4.0，之后也会报错相应的包，就手动去下载对应的包
<br>[下载传送门](https://github.com/electron-userland/electron-builder-binaries/releases)
<br>之后解压到 => C:\Users\KZQ\AppData\Local\electron-builder\Cache
<br><div style="color:red">切记，一定要在上面路径下先创建一个叫做winCodeSign的路径，然后将winCodeSign-2.4.0解压到winCodeSign路径。其他的包也是如此</div>
![解压对应包路径图](/img/electron-builder-path.png)