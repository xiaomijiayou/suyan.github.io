---
layout: post
title: nodejs+webpack+antd+ajax
category: 资源
tags: nodejs+webpack+antd+ajax
description: 根据自己数据可视化的开发环境， 记录关于nodejs 前后端开发， 前端使用reactjs， 后端使用nodejs - koa， 数据交互使用ajax.
---

### 官方资源

- [官方首页](http://twitter.github.io/bootstrap/)
  
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

  

- [Bootstrap Form Helpers](http://vincentlamanna.com/BootstrapFormHelpers/index.html)

  扩展常用的表单功能，包括日期选择、时间选择等


