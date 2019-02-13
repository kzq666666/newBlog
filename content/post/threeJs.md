---
title: "Three.js"
date: 2018-11-16T23:43:52+08:00
showDate: true
draft: false
tags: ["THREE","three","three.js","3D"]
---
### 1.scene 场景
scene就是一个可以放置物体、灯光的3D空间，和现实中的一个空间相似，可大可小
```js
//创建一个场景
var scene = new THREE.Scene();
```
### 2.camera 相机
camera决定看一个物体的方式和位置，和现实中的相机行为相似，有很多种类的相机。

* PerspectiveCamera 透视相机

```js
// 透视相机更加接近于现实中我们看物体的视角，远小近大
// 创建一个透视相机
var camera = new THREE.PerspectiveCamera(fov可视角度,aspect纵横比,near近端距离,far远端距离)
// 设置camera的位置
camera.set(x,y,z)
```
<img src="/PCamera.jpg">
### 3.渲染器
* WebGLRenderer

```js
var renderer = new THREE.WebGLRenderer()
```


### 4.几何形状
* 立方体(CubeGeometry)

```js
CubeGeometry(width, height, depth, widthSegments, heightSegments, depthSegments)
// width,height,depth是分别在x,y,z方向上的长度,后面三个参数是对应的分段数,如果不需要分段可以不设置。几何中心在原点
```
* 平面(PlaneGeometry)

长方形平面,并非是无限延伸的平面  

```js
PlaneGeometry(width, height, widthSegments, heightSegments)
// width,height分别是x,y方向上的长度,后面两个参数是对应的分段数
```
* 球体(SphereGeometry)

```js
SphereGeometry(radius, segmentsWidth, segmentHeight, phiStart, phiLength, thetaStart, thetaLength)
// radius:半径,segmentWidth:纬度上切片数,segmentHeight:经度上的切片数,phiStart:经度开始的弧度,phiLength:经度跨过的弧度,thetaStart:纬度开始的弧度,thetaLength:纬度跨过的弧度
```
* 文字形状
  
使用额外的文字形状需要下载和引用额外的字体库,下载对应的json文件放在目录下,用下面的方法引用
<br>传送门:https://github.com/mrdoob/three.js/tree/master/examples/fonts
```js
var loader = new THREE.FontLoader();
loader.load('../gentilis_regular.typeface.json', function(font) {
    var text = new THREE.Mesh(
        new THREE.TextGeometry('KZQ',{
            font:font,
            size:1,
            height:1
        }),
        new THREE.MeshNormalMaterial();
        scene.add(text);
        renderer.render(scene, camera);
    )
})
```
### 4.物体

* Mesh 构造器

```js
// 基于以三角形为polygon mesh多边形网格的物体的类
Mesh(geometry:Geometry,material:Material)
```

* Object3D()

Object3D是大部分物体的基类，大部分的物体都可以通过Object3D构建
```js
var object = new Object3D();
```

### 5，加载器
* ImageLoader

```js
// 初始化一个加载器
var loader = new THREE.ImageLoader();
// 加载一个图片资源
loader.load(
    // 资源URL
    './image/1.jpg',
    // onLoad回调
    function(image){ 
        var canvas = document.createElement('canvas');
        var context = canvas.getContext('2d');
        context.drawImage(image,100,100)
    }
)
```

### 6.控制器
* OrbitControls
  
```js
// 构造器(Constructor)
var controls = new THREE.OrbitControls(object:camera,domElement:HTMLDOMElement);

// 属性(Properties)
1 .maxDistance
滚轮能放大的最大距离
2 .minDistance
滚轮能缩小的最小距离

// 方法(methods)
1 .update()
更新控件,一般用在手动更新camera变换后调用,或者在更新循环中调用

var controls = new THREE.OrbitControls(camera,renderer.domElement);
camera.position.set(0,0,5000);
controls.update()

function animate(){
    requestAnimationFrame(animate);
    controls.update()
}
```
* TrackballControls

球形控制器，以物体为中心，鼠标左键控制旋转，右键平移
```js
// 构造器(Constructor)
var controls = new THREE.TrackballControls(camera, renderer.domElement)
```

### 8.其他
* Vector3 3D矢量

```js
var vector = new THREE.Vector3(x,y,z);
// 如果没有参数，则是指向一个(0,0,0)的矢量;
```











```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>使用three.js创建一个球</title>
    </head>
    <body>
        <script type="text/javascript" src="three.js"></script>
        <script type="text/javascript" src="OrbitControls.js"></script>
        <script type="text/javascript">
            // 创建一个场景
            var scene = new THREE.Scene();
            // 创建一个透视视图相机
            var camera = new THREE.PerspectiveCamera(45,window.innerWidth/innerHeight,1,1000);
            // 设置相机的位置(x,y,z)
            camera.position.set(0,0,5);
            // 创建一个渲染器
            var renderer = new THREE.WebGLRenderer();
            // 设置渲染器的大小
            renderer.setSize(window.innerWidth,window.innerHeight);
            // 设置背景颜色
            renderer.setClearColor(0xfff6e6)
            // 插入到页面当中
            document.body.appendChild(renderer.domElement);

            // 开始渲染(表演开始....)
            // 创建一个球使用SphereGeometry()
            var geomery = new THREE.SphereGeometry(1,22,22);
            // 选择材料
            var material = new THREE.MeshNormalMaterial({wireframe:true});
            // 创建网格对象
            var sphere = new THREE.Mesh(geomery, material);
            // 加入到场景(舞台)当中
            scene.add(sphere);
            // 创建一个控制器
            var controls = new THREE.OrbitControls(camera,renderer.domElement);
            controls.addEventListener('change',function(){
                renderer.render(scene,camera)
            })
            // 渲染
            renderer.render(scene,camera)
            // var animation = function(){
            //     requestAnimationFrame(animation);
            //     sphere.rotation.x += 0.01;
            //     sphere.rotation.y += 0.01;
            //     renderer.render(scene,camera)
            // }
            // animation()
        </script>
    </body>
</html>
```
