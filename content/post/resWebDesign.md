+++
title = "ResWebDesign"
date = 2019-04-02T16:26:09+08:00
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
- 媒体查询
### meta标签
针对视口的标签，告诉浏览器该如何渲染当前页面，是网页和移动浏览器的接口
```html
<!--
viewport:视口 
width为设备宽度 
初始化页面大小为实际大小的1.0倍 
禁止用户缩放
-->
<meta name="viewport" content="width=device-width,initial-scale=1.0,user-scalable=no"/>
```
### 弹性布局与响应式图片
#### Flexbox
- 方向
  - flex-direction
    - row:水平方向（起点是最左端）
    - row-reverse:水平反方向（起点是最右端）
    - column:垂直方向（起点是最上方）
    - column-reverse:垂直反方向（起点是最下方）
- 主轴和交叉轴
  - FlexBox方向是row，主轴就是横轴，交叉轴就是与之垂直的纵轴
  - FlexBox方向是column，主轴就是纵轴，交叉轴就是横轴
- 对齐
  - align-item:交叉轴对齐方式
    - flex-start:从flexbox父元素起始边对齐
    - flex-end:从flexbox父元素末尾对齐
    - center:从flexbox父元素居中对齐
    - baseline:沿基线对齐
    - stretch:所有项拉伸至父元素一样大（默认）
  - justify-content:主轴对齐方式
    - flex-start(默认)
    - flex-end
    - center
    - space-between:每个子元素的之间空白间距一样
    - space-around:每个子元素的两端空白间距都一样
- flex(flex-grow flex-shrink flex-basis)
  - flex-grow:伸
  - flex-shrink
  - flex-basis
- 弹性