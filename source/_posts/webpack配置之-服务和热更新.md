---
title: webpack配置之 服务和热更新
date: 2018-08-24 11:11:30
tags:
---
执行 npm install webpack-dev-server --save-dev 
对webpack.config.js 进行配置 配置如下
```javascript
devServer: {
  // 设置基本目录结构
  contentBase: path.resolve(__dirname, 'dist'),
  // 服务器的IP地址，可以使用IP也可以使用localhost
  host: 'localhost',
  // 服务端压缩是否开启
  compress: true,
  // 配置服务端口号
  port: 8088
}
```