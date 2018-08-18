---
title: webpack配置之 入口出口
date: 2018-08-18 17:49:11
tags:
---
### webpack 3.0 入口出口
## 配置文件 webpack.config.js
webpack.config.js 就是webpack的配置文件 这个文件需要自己在项目根目录下手动创建。文件大致结构如下
```javascript
module.exports = {
    // 入口文件的配置项 可以是单一的入口 也可以是多入口
    entry: {},
    //出口文件的配置项 支持多出口配置
    output: {},
    //模块： 例如css 图片如何转换 压缩
    module: {},
    //插件：用于生产模版和各项功能
    plugins: [],
    //配置webpack开发服务功能
    devServer: {}
}
```
# entry 选项（入口配置）
这个选项就是我们配置我们要压缩的文件一般是 javascript 文件 （也可以是css） 
webpack.config.js 中的entry 选项
```javascript
// 入口文件的配置项
entry: {
    entry: './src/index.js' // index.js 这里的路径可以随意指定
}
```
# output选项 （出口配置）
出口配置是用来告诉webpack最后打包文件的地址和文件名称的。一般都是打包到一个叫做 dist 文件的目录下 代码如下
```javascript
// 出口文件的配置
output: {
    path: path.resolve(_dirname, 'dist'),
    filename: 'bundle.js'
}
```
## 多入口 多出口配置
配置文件如下
```javascript
const path = require('path')
module.exports = {
  entry: {
    entry: './src/index.js',
    entry2: './src/other.js'
  },
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: '[name].js'
  },
  module: {},
  plugins: [],
  devServer: {}
}
```