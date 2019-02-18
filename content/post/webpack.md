+++
title = "Webpack"
date = 2019-02-15T14:29:05+08:00
draft = false

# Tags and categories
# For example, use `tags = []` for no tags, or the form `tags = ["A Tag", "Another Tag"]` for one or more tags.
tags = ['webpack']
categories = []

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder. 
[image]
  # Caption (optional)
  caption = "https://webpack.js.org/d19378a95ebe6b15d5ddea281138dcf4.svg"

  # Focal point (optional)
  # Options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
  focal_point = ""
+++
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 600 600" style="width:2rem;height:2rem"><path fill="#FFF" d="M300 .1L565 150v299.9L300 599.8 35 449.9V150z"/><path fill="#8ED6FB" d="M517.7 439.5L308.8 557.8v-92L439 394.1l78.7 45.4zm14.3-12.9V179.4l-76.4 44.1v159l76.4 44.1zM81.5 439.5l208.9 118.2v-92l-130.2-71.6-78.7 45.4zm-14.3-12.9V179.4l76.4 44.1v159l-76.4 44.1zm8.9-263.2L290.4 42.2v89l-137.3 75.5-1.1.6-75.9-43.9zm446.9 0L308.8 42.2v89L446 206.8l1.1.6 75.9-44z"/><path fill="#1C78C0" d="M290.4 444.8L162 374.1V234.2l128.4 74.1v136.5zm18.4 0l128.4-70.6v-140l-128.4 74.1v136.5zM299.6 303zm-129-85l129-70.9L428.5 218l-128.9 74.4-129-74.4z"/></svg>
[官网](https://webpack.js.org/)&nbsp;&nbsp;[文档](https://webpack.js.org/concepts)
### Entry
Webpack的入口，通过入口文件，webpack开始搭建内部依赖网
```js 
// webpack.config.js
module.exports = {
  entry: './path/to/my/entry/file.js'
};
```
### Output
输出配置
```js
module.exports = {
  output: {
    filename: 'bundle.js',
  }
};
```
### Mode
主要是两种环境，开发环境（development）和生产环境（production），相应的环境，webpack会做出具体的优化方案。
<br>（default：production）
```js
module.exports = {
  mode: 'production' // 'development'
}
```
### [Loaders](https://webpack.js.org/loaders/)
加载器，用于加载资源，如scss文件或者将一些拓展语言（TypeScript,Scss）转换成合适的格式。
<br>webpack内置可以处理的文件类型：`JSON`
```js
module.exports = {
  module: {
    rules: [
      { test: /\.css$/, use: 'css-loader' },
      { test: /\.ts$/, use: 'ts-loader' }
    ]
  }
};
```
* `css-loader` => 处理.css文件
* `style-loader` => 通过\<style\>标签将css-loader内部样式注入到html中
* `Less-loader`
* `Sass-loader`
* `post-css-loader`

### [Plugins](https://webpack.js.org/plugins/)
插件，webpack的支柱，webpack本身就是建立在类似的插件系统上的。
* banner-pulgin:

### Webpack-dev-server
##### 安装依赖
```npm
npm install --save-dev webpack-dev-server
```
##### 配置
```js
module.export = {
  plugin:[
    new webpack.HotModuleReplacementPlugin()  // HMR功能插件
  ]
  devServe:{
    contentBase:'./public', // 本地服务器加载的页面所在目录
    historyApiFallback:true, // true为不跳转，所有的跳转都会指向index.html
    inline:true // 为入口页面添加"热加载"功能
    hot:true // 开启"热替换"（Hot Module Replacement HMR）功能
  },
}
```
##### 开启服务
* 直接在terminal中输入`node_modules/.bin/webpack-dev-server`,node_modeules下的.bin目录有许多执行文件可以直接运行

* 在package.json中的script对象中添加`"server":"webpack-dev-server"`

<br>在terminal中输入`npm run server`就可以了~
### Babel
编译Javascript的工具，使代码变得风骚，使用最新的javascript代码（ES6，ES7）并使用像react的JSX的扩展语言。
<br>babel核心包 => `babel-core`
<br>解析ES6的包 => `babel-env-preset`
<br>解析JSX的包 => `babel-preset-react`
### CSS模块化
利用css-loader和style-loader容易使全局样式遭到污染，css模块化通过将css的class名传递到具体的组件中，就可以有效的避免全局样式被污染
```js
modules.export = {
  loader:{
    rules:[
      {
        test:/\.css$/,
        use:[
          {
            loader:"style-loader"
          },
          {
            loader:"css-loader",
            options:{
            modules:true,
            localIdentName:'[name]__[local]--[hash:base64:5]' // css的类名格式
          }
        ]
      }
    ]
  }
}
```