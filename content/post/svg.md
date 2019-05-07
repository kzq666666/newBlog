+++
title = "SVG"
date = 2019-04-11T15:38:47+08:00
draft = false

# Tags and categories
# For example, use `tags = []` for no tags, or the form `tags = ["A Tag", "Another Tag"]` for one or more tags.
tags = []
categories = []

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder. 
[image]
  # Caption (optional)
  caption = ""

  # Focal point (optional)
  # Options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
  focal_point = ""
+++
### SVG(Scalable Vector Graphics 可伸缩矢量图)
### 历史
2001年推出第一版，一直在发展，但直到高分辨率设备出现才得到广泛的关注和使用
### 定义
SVG是XML中用于描述二维图形的语言，SVG支持三种图形对象`矢量图形形状`、`图像`、`文本`
### 代码实例
#### 五角星
<svg width="198px" height="188px" viewBox="0 0 198 188" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:sketch="http://www.bohemiancoding.com/sketch/ns">
    <!-- Generator: Sketch 3.2.2 (9983) - http://www.bohemiancoding.com/sketch -->
    <title>Star 1</title>
    <desc>Created with Sketch.</desc>
    <defs></defs>
    <g id="Page-1" stroke="none" stroke-width="1" fill="none" fill-rule="evenodd" sketch:type="MSPage">
        <polygon id="Star-1" stroke="#979797" stroke-width="3" fill="#F8E81C" sketch:type="MSShapeGroup" points="99 154 40.2214748 184.901699 51.4471742 119.45085 3.89434837 73.0983006 69.6107374 63.5491503 99 4 128.389263 63.5491503 194.105652 73.0983006 146.552826 119.45085 157.778525 184.901699 "></polygon>
    </g>
</svg>

```html
<!--
  0 0 198 198
  min-x min-y 宽度 高度
-->
<svg width="198px" height="188px" viewBox="0 0 198 188" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:sketch="http://www.bohemiancoding.com/sketch/ns">
    <!--title和desc是在图片没有加载出来时候的展现出来的信息 -->
    <title>Star 1</title>
    <desc>Created with Sketch.</desc>
    <!--defs用于存储所有可以复用的元素定义的地方，如梯度、符号、路径-->
    <defs></defs>
    <!--g标签是group的缩写，可以把其他元素捆绑在一起使用-->
    <g id="Page-1" stroke="none" stroke-width="1" fill="none" fill-rule="evenodd" sketch:type="MSPage">
        <!--多边形节点（polygon），内置还有path、rect、circle、ellipse、-->
        <polygon id="Star-1" stroke="#979797" stroke-width="3" fill="#F8E81C" sketch:type="MSShapeGroup" points="99 154 40.2214748 184.901699 51.4471742 119.45085 3.89434837 73.0983006 69.6107374 63.5491503 99 4 128.389263 63.5491503 194.105652 73.0983006 146.552826 119.45085 157.778525 184.901699 "></polygon>
    </g>
</svg>
```
### 在页面上插入SVG
- img
```html
<img src="1.svg" alt="a svg"/>
```
- object
```html
<object type="image/svg+xml" data="1.svg">
  <span>your browser donot support svg</span>
</object
```
- 背景图片插入
- 内联

