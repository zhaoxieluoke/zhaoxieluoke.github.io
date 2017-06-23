---
title: 用webpack来构建es6编译环境
date:
tags:
---
# 用webpack来构建es6编译环境
>创建项目
```
npm init  
```

>安装babel webpack 
webpack-derv-server
```
npm install babel-core babel-loader babel-preset-es2015 webpack webpack-dev-server  --save-dev 
```

>配置scripts  test为默认命令 build为要使用的命令 在命令中同时对webpack-dev-server 进行配置 端口 热加载 
```
"scripts":{
      "test": "echo \"Error: no test specified\" && exit 1",    
      "build":"webpack-dev-server --port 8397 --hot --inline",  
  }
```
>创建webpack.config.js文件进行配置
```
 var webpack = require('webpack');
  var path = require('path');
  module.exports = {
      entry:'./src/index.js', // 输出文件入口
      output:{    // 输出路径
          path:__dirname, // 取得当前目录路径
          filename:'bundle.js' // 输出文件路径、文件名
      },
      module:{    // 加载模块插件
          loaders:[   // 加载器 插件
              {
                  test:/\.css$/,  // 正则匹配css文件
                  loader: "babel-loader",   //
                  exclude:'/node_module/' ,// 排除的文件夹
                  query:{
                        presets:["es2015"]
                  }
                  /*include:'/app/'       // 多个就用数组*/
              }
          ]
       }
    //   devServer: {
    //         //  contentBase: "./public",//本地服务器所加载的页面所在的目录
    //         port: 6666, //端口
    //         historyApiFallback: true,//不跳转
    //         inline: true//实时刷新
    //   }
  };
```
>*可选* 创建.babelrc文件 进行预设 (**如果在package.json文件中进行过预设则，这个文件可以省略--**)
```
{
  "presets":["es2015"]
}
```
>最后执行npm run build 打开浏览器输入localhost:端口号 进行查看


<font style="color:#666">*注: npm指可用cnpm替换，具体方法请自行搜索，此处不再赘述 </font>
