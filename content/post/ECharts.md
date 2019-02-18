+++
title = "ECharts"
date = 2019-02-14T09:42:36+08:00
draft = false

# Tags and categories
# For example, use `tags = []` for no tags, or the form `tags = ["A Tag", "Another Tag"]` for one or more tags.
tags = ["Echarts","图表","数据"]
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
[官网](https://echarts.baidu.com)&nbsp;&nbsp;
[教程](https://echarts.baidu.com/tutorial.html)&nbsp;&nbsp;
[API](https://echarts.baidu.com/api.html)


<br>
<script src="/src/echarts.min.js"></script>
<div style="width:100%;height:15em;margin: 0 auto" id="bar"></div>
<p></p>
<p></p>
<div style="width:100%;height:15em;margin: 0 auto" id="pie"></div>
<p></p>
<p></p>
<div style="width:100%;height:15em;margin: 0 auto" id="line"></div>

<!-- <div style="width:100%;height:15em;margin: 0 auto" id="pie"></div> -->
<script>
    echarts.init(document.getElementById('bar')).setOption({
            title:{
              text:'柱状图'
            },
            tooltip:{},
            legend:{
              data:['销量']
            },
            xAxis:{
              data:["衬衫","羊毛衫","雪纺衫","裤子","高跟鞋","袜子"]
            },
            yAxis:{},
            series: [{
                type: 'bar',
                name: '销量',
                data: [5, 20, 36, 10, 10, 20]
            }]
    });
   echarts.init(document.getElementById('pie')).setOption({
            title:{
              text:'饼状图'
            },
            series: {
                name: '访问来源',
                type: 'pie',
                radius:'60%',
                data: [
                    {value:235, name:'视频广告'},
                    {value:274, name:'联盟广告'},
                    {value:310, name:'邮件营销'},
                    {value:335, name:'直接访问'},
                    {value:400, name:'搜索引擎'}
                ]
            }
    });
    echarts.init(document.getElementById('line')).setOption({
    title: {text: '直线图'},
    tooltip: {},
    toolbox: {
        // feature: {
        //     dataView: {},
        //     saveAsImage: {
        //         pixelRatio: 2
        //     },
        //     restore: {}
        // }
    },
    xAxis: {},
    yAxis: {},
    series: [{
        type: 'line',
        smooth: true,
        data: [[12, 5], [24, 20], [36, 36], [48, 10], [60, 10], [72, 20]]
    }]
});
</script>


```js
// 柱状图
echarts.init(document.getElementById('bar')).setOption({
        title:{
          text:'柱状图'
        },
        tooltip:{},
        legend:{
          data:['销量']
        },
        xAxis:{
          data:["衬衫","羊毛衫","雪纺衫","裤子","高跟鞋","袜子"]
        },
        yAxis:{},
        series: [{
            type: 'bar',
            name: '销量',
            data: [5, 20, 36, 10, 10, 20]
        }]
});

// 饼状图
echarts.init(document.getElementById('pie')).setOption({
        title:{
          text:'饼状图'
        },
        series: {
            name: '访问来源',
            type: 'pie',
            radius:'60%',
            data: [
                {value:235, name:'视频广告'},
                {value:274, name:'联盟广告'},
                {value:310, name:'邮件营销'},
                {value:335, name:'直接访问'},
                {value:400, name:'搜索引擎'}
            ]
        }
});

// 直线图
echarts.init(document.getElementById('line')).setOption({
        title: {text: '直线图'},
        tooltip: {},
        toolbox: {
            // feature: {
            //     dataView: {},
            //     saveAsImage: {
            //         pixelRatio: 2
            //     },
            //     restore: {}
            // }
        },
        xAxis: {},
        yAxis: {},
        series: [{
            type: 'line',
            smooth: true,
            data: [[12, 5], [24, 20], [36, 36], [48, 10], [60, 10], [72, 20]]
        }]
});
```