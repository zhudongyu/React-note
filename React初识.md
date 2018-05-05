## React

> 一、React概述

React 是一个用于构建用户界面的 JavaScript 库，它主要用于构建UI，其实React就是 MVC 中的 V（视图）。

React 起源于 Facebook 的内部项目，因为该公司对市场上所有 JavaScript MVC 框架，都不满意，就决定自己写一套，用来架设 Instagram 的网站。做出来以后，发现这套东西很好用，就在2013年5月开源了。

狭义来讲 React 是 Facebook 内部开源出来的一个前端 UI 开发框架，广义来讲 React 不仅仅是 js 框架本身，更是一套完整的前端开发生态体系，这套体系包括：
1. React.js
2. ReactRenders: ReactDOM / ReactServer / ReactCanvas
3. Flux 模式及其实现（Redux , Fluxxor，Mobx）
4. React 开源组件（包括UI库）
5. React Native

任何技术都是一样，技术本身的核心不会太复杂，但是围绕这个主体会有很多依附的知识点形成了体系化的技术栈。 所以在 React 这条路上不仅仅是学习 React 本身，而是学习这套开发体系，整个技术栈。

    官方网址：https://reactjs.org/
    React中文网：https://doc.react-china.org/  
    GitHub: https://github.com/facebook/react  问题参见 issues

> 二、React中的基本概念

    1.React.js
      React.js 是 React 的核心库，在应用中必须先加载核心库。
    2.ReactDOM.js
      ReactDOM.js 是 React 的 DOM 渲染器。
      React 将核心库和渲染器分离开了，为了在 web 页面中显示开发的组件，需要调用 ReactDOM.render 方法， 第一个参数是 React 组件，第二个参数为 HTMLElement。
    3.JSX
      作用：描述DOM元素
      JSX 是 React 自定义的语法，可以理解成用js编写的xml格式代码。最终 JSX 会转化为 JS 运行于页面当中。
    4.组件
      组件是 React 中的核心概念，页面当中的所有元素都是通过 React 组件来表达，我们将要写的 React 代码绝大部分都是在做 React 组件的开发。
    5.VIRTUAL DOM
      React 抽象出来的虚拟 DOM 树，虚拟树是 React 高性能的关键。
    6.单向数据流：one-way reactive data flow
      React 应用的核心设计模式，数据流向自顶向下（组件层级关系传递）

> 三、React环境搭建 之 Create-react-app
    
    1.Create-react-app 是开始构建新的React单页应用程序的最佳方式
      @1.npm install -g create-react-app 一次全局安装
      @2.create-react-app my-app
      @3.cd my-app
      @4.npm start 进入开发模式
      @5.npm run build 打包用于生产
      @6.npm run eject 解绑webpack配置到文件下
    2.初始化项目结构分析
      运行方式: index.html -> index.js -> App.js

```javascript
    .
    ├── build                                      // 打包后的生产环境文件
    |   ├── static                                 // 1
    |   |   ├── css                                // 1
    |   |   |   └── main.xxx.css                   // 1
    |   |   |   └── main.xxx.css.map               // 1
    |   |   ├── js                                 // 1
    |   |   |   └── main.xxx.js                    // 1
    |   |   |   └── main.xxx.js.map                // 1 
    |   |   ├── media                              // 1
    |   |       └── xxx.png                        // 1   
    |   ├── index.html 
    |   ├── manifest.json
    |   ├── asset-manifest.json 
    |   ├── favicon.ico       
    |   ├── service-worker.js  
    .   .
    .   .
    ├── node_modules                                // npm 管理的第三方包
    ├── public                                      // 公共资源
    |   └── favicon.ico                             // 浏览器tab页及收藏时显示的图标
    |   └── index.html                              // 单页应用入口文件
    |   └── manifest.json                           //          
    |                               
    ├── src                                         // 开发源码目录
    |   └── App.js                                  // React组件
    |   └── App.css                                 // React组件样式
    |   └── index.js                                // webpack打包的入口文件
    |   └── index.css                               // 全局样式,一般会引入index.js中进行打包
    |   └── registerServiceWorker.js                // 
    |   └── logo.svg                                // 
    |   └── App.test.js                             // 
    ├── package.json                                // npm 包管理文件
    ├── README.md                                   // React学习关键
    .
```  
    
> 四、组件库的安装与使用

    1.Ant Design             
      @1.在国内热度很高，偏向国内的业务需求
      @2.官网：https://ant.design/index-cn
      @3.安装步骤： https://ant.design/docs/react/introduce-cn 

    2.Material-ui
      @1.动画的支持更好，配色更欧美范。
      @2.官网：http://www.material-ui.com/

    3.React-bootstrap
      @1.虽然Bootstrap也是facebook的产品，但是对于React 并没投入资源。
      @2.官网：
      