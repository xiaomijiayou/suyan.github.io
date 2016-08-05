---
layout: post
title: nodejs+webpack+antd+ajax
category: 资源
tags: nodejs+webpack+antd+ajax
description: 根据自己数据可视化的开发环境， 记录关于nodejs 前后端开发， 前端使用reactjs， 后端使用nodejs - koa， 数据交互使用ajax.
---


### 官方资源

- [官方首页](http://twitter.github.io/bootstrap/)

### 官方资源
    
    - [1](http://twitter.github.io/bootstrap/)
    svn checkout svn://192.168.1.1/pro/domain
    svn co

### node开发环境

    - [Nodejs-install](http://www.kancloud.cn/summer/nodejs-install/71975)
    
    1:安装nvm
      git clone nvm
      直接从 github clone nvm 到本地, 这里假设大家都使用 ~/git 目录存放 git 项目:
      $ cd ~/git
      $ git clone https://github.com/creationix/nvm.git
      配置终端启动时自动执行 source ~/git/nvm/nvm.sh,
      在 ~/.bashrc, ~/.bash_profile, ~/.profile, 或者 ~/.zshrc 文件添加以下命令:
      source ~/git/nvm/nvm.sh
    
    2:安装nodejs(最新版本是v6.3.1)
      NVM_NODEJS_ORG_MIRROR=https://npm.taobao.org/mirrors/node nvm install 6  
      node 自带了npm， 后面的安装就可以使用npm

### webpack安装

    - [webpack](https://github.com/webpack/webpack)
    - [webpack安装事例](https://www.codementor.io/reactjs/tutorial/beginner-guide-setup-reactjs-environment-npm-babel-6-webpack)
        其中包含了webpac的hello world， react安装， babel安装配置；
        Babel 是一个 JavaScript 编译器，Babel 用于转化你的 JavaScript 代码， 可以使用最新的js语法。
        Loader： - [webpack的loader介绍](http://zhaoda.net/webpack-handbook/loader.html)
          Webpack 本身只能处理 JavaScript 模块，如果要处理其他类型的文件，就需要使用 loader 进行转换， 后面需要的less， css， json图片等都需要相应的loader进行转换.
  


### antd安装

    - [antd官网](http://ant.design/)
    
    1： npm install antd --save-dev
    2：这里使用 babel，通过 babel-plugin-antd 来进行按需加载，加入这个插件后。你可以仍然这么写：
      import { Button } from 'antd';
      插件会帮你转换成上面的写法。另外此插件配合 style 属性可以做到模块样式的按需自动加载。
      npm install babel-plugin-antd --save-dev
      配置：➜ vim .babelrc 
      {
        "plugins": [["antd", {"style":true,"css":true}]]
      }
      但是后面运行时报如下错误：
        （1）：error in ./~/antd/lib/style/index.less  =》  因为webpack缺少less-loader                 
          - [less-loader官网](https://fakefish.github.io/react-webpack-cookbook/Loading-LESS-or-SASS.html ) 
        （2）：error: cannot resolve module 'style' in ....   =》 因为webpack缺少style-loader
          - [style-loader官网](https://github.com/webpack/style-loader )
 
### koa安装（搭建简单的服务器， 根据请求解析json文件， 并返回给客户端）

    - [koa 官网](http://koajs.com/)
    
    npm install koa
    1：服务器端
    vim readJson.js
    
        var fs = require('fs')
        var app = require('koa')()
        var cors = require('koa-cors')    //跨域
        var bodyParser = require('koa-bodyparser');
        var readFile = function(dir) {
          return function(fn) {
            fs.readFile(dir, fn)
          }
        }
        app.use(cors());
        app.use(bodyParser());
        app.use(function* () {
        
        var  jsonOb = this.request.query;
          var arr = yield [jsonOb.jsonPath].map(function(path) {
          	console.log("path", path);
            return readFile(path)
          });
          this.body = arr.join(',');
        })
        app.listen(8888)
    访问 http://localhost:8888 
    
    2：客户端ajax发送json文件解析请求
    
      $.ajax({
       url:"http://localhost:8888/list?jsonPath="+jsonPath,
       type: "GET",
       dataType: "json",
       error: function(XMLHttpRequest, textStatus, errorThrown){
          var s1=XMLHttpRequest;
          var s2=textStatus;
          var s3=errorThrown;
          alert("error message : "+errorThrown.toString())
          },
       success: function(data){
          console.log("data", data);
          this.setState({data:data,loading:false, dateList: dateList, date: dateList[0], dataTime: this.getTimeData(data, dateList[0])} );

          }.bind(this) 
      }); 
    
    



    










