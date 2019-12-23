# 2019前端进阶指南
> 转眼间，2019年进入倒计时，今年逐渐使用上ES6语法，学会了React框架的使用，尝试了微信小程序的开发。虽然没有具体业务的支撑，但是玩了一下，知道怎么回事。今天看了一前端er的文章，激起积极的情绪，心血来潮要好好确定一下接下来要努力的方向。

## The Building Blocks - 基础前端开发
1. HTML & CSS
    最基础的知识：
    * Semantic HTML5 Elememts - 语义化的HTML元素
    * Basic CSS (Positioning, box model, etc) - 基础的CSS语法
    * Flexbox & CSS Grid
    * CSS Variables (Custom Properities) - CSS变量
    * Browser Dev Toold - 浏览器开发者工具
2. Responsive Layout - 响应式布局
    Responsive layouts are no longer a luxury, they are a necessity.
    响应式设计不再是网页加分项，而是必须的。
    * Set viewport - 设置viewport
    * Fluid widths - 非固定宽度
    * Media queries - 媒体查询
    * rem over px - 使用rem代替px
    * Mobile first, stacked columns - 移动优先，柱状显示

    Suggested
    * Build an HTML5 Website With A Responsive Layout
    * Responsive Landing Page
    * Build A Responsive Mobile First Websites
    * Pluralsight Login Page Clone

3. Basic Deployment - 基础的部署工作
    Learn to deploy a static websites
    * Register a domain name - 注册一个域名
    * Managed shared hosting or VPS - 管理共享主机或虚拟机
    * FTP, SFTP File Upload - FTP, SFTP文件上传
    * Static Hosting - 静态页面托管

    Suggested
    * Github Deploy & Domain
4. CSS Pre-Processor - CSS预处理器
    Not mandatory but recommended. It is easy enough to learn the basics.
    * Structured CSS - 结构化CSS
    * Variables - 变量
    * Nested CSS - 嵌套样式表
    * Minxins & Functions - Minxins & 函数
    * inheritance - 继承
5. Vanilla JavaScrpt - 原生JavaScript
    Start learning JavaScript without library or framework.
    * Data Types, functions, conditionals, loops, operators - 数据类型，函数，条件判断，循环，操作符
    * DOM Mainipulation & Event - DOM操作和事件
    * JSON
    * Fetch API
    * ES6+ (Arrow Functions, promises, async/wait, destructuring) - ES6+ (箭头函数，Promise, async/await, 解构)
6. Basic Front-end Web Developer
    * Build static websites - 构建静态站点
    * Build UI layouts (Take a design and create the html/css) - 构建UI布局，还原设计稿
    * Add dynamic functionality (modals, slidersshows, etc) - 添加一些交互功能
    * Deploy and maintain websites - 部署和维护网站

## easier UIs prototyping - 成熟的前端开发
1. HTML & CSS Framework **Choose One**
    * BootStrap
    * Materialize
    * Bulma
    * ElementUI
    * Ant Design
2. Git & Tooling - Git 和其他工作流
    * Basic Command Line - 基础的命令行
    * Git (Version Control) - Git (版本控制)
    * NPM or Yarn (installing packages) - NPM or Yarn (包管理)
    * Webpack or Parcel (module building) - Webpack or Parcel (打包工具)
    * Gulp or Grunt (task runners) - Gulp or Grunt (任务管理和构建工具)
    * Editor Extensions (ESLint, Prettier, Live Server, etc) - 编辑器插件
3. Front-End Framework **Choose One**
    It is becoming a necessity to learn a JS front-end framework
    * Very popular in the industry - 大公司非常流行
    * More interactive & intersting UIs - 更多的交互和有趣的UI组件
    * Components & modular front end code - 组件化 & 模块化前端代码
    * Goods for teams - 对团队有利

    Front-End Framework
    * React - Most popular in the industry
    * Vue - Easy to use and really gaining traction - 获得关注
    * Angular - Fading A Bit - Used in enterprise 有点过时
4. State Management - 状态管理
    For larger apps with a framework , you may need to learn methods to manage app-level state.
    * Redux, Context API
    * Apollo (GraphQL Client)
    * Vuex
    * NgRx
5. Full Fledged Front-End Web Developer
    * Build incredible front-end applications - 构建一个优秀的前端应用
    * Smooth & steady front-end workflow - 流畅和稳定的前端工作流
    * Work well with teams & familiar with Git - 多人开发 & 熟练使用Git
    * Connect to backend APIs & work with data - 请求后端API & 前端数据响应


## Backend Programming - 全栈开发工程师
1. Server Side Language **Choose One**
    To Be a full stack or software engineer, you will need to learn a server-side language/technology.
    * Nodejs
    * Python
    * PHP
    * C#
    * Go

    Things To Learn - 学习顺序
    * Fundamental Syntax - 基础的后端语言语法
    * Structure & Workflow - 数据结构和工作流
    * Package Management - 包管理
    * HTTP/Routing - HTTP/路由
2. Server Side Framework **Choose One**
    Do not reinvent the wheel. Learn a framework to build and faster and faster.
    * Nodejs - Express, Koa, Adonis
    * Python - Django, Flask
    * PHP - Laravel, Symfony
    * C# - ASP.NET
3. Database **Choose One Or Two**
    Most applications will use some kind of database. There are different types, here are some options
    * Relational Database - MySQL、PostgreSQL、MS SQL - 关系型数据库
    * NoSQL - MongoDB、Couchbase - 非关系型数据库
    * Cloud - Firebase、AWS、Azure DocumentDB - 云服务
    * Lightweight - SQLite、NeDB、Redis - 轻量级
4. Server Rendered Pages - 服务端渲染
    Frameworks like React, Vue & Angular can also be rendered on the server which can actually make things relatively earier. 
    - 像React、Vue和Angular这些框架都可以进行服务端渲染
    * Next.js - React
    * Nuxt.js - Vue
    * Angular Universal - Angular
5. CMS **Choose One**
    Content management systems allow for quick development and give your clients the ability to update their content. May not be a bad idea to pick one up. Great for freelancers.
    内容管理系统允许快速开发并为您的客户提供更新内容的能力. 在你需要快速开发网站的时候, 它们是很适合的. 特别是对于自由开发者.
    * PHP Based - Wordpress、Drupal
    * JS Based - Ghost、Keystone
    * Python Based - Mezzazine
    * .NET - Piranha、Orchard CMS
6. DevOps, Deloyment & More
    Learning languages and frameworks is one thing, setting up environments, testing & deployment is another.
    * Deployment - Linux、SSH、Git、Server Software(Nginx, Apache)
    * Platforms - Digital Ocean、 AWS、 Heroku、 Azure
    * Virtualization - Docker、Vagrant - 可视化
    * Testing - Unit、integration、Functional、System - 测试(单元测试、集成测试、函数测试、系统测试)
7. Full Stack Badass
    * Setup full stack dev development & workflows - 设置全栈的开发环境和工作流
    * Build back-end APIs & micro-services - 构建后端服务API和微服务
    * Work with database - 数据库操作
    * Construct full-stack apps (Front-end framework & server) - 能够独立开发应用(前端和服务端) 
    * Deploy to the cloud (SSH, Git，Servers, etc) - 部署到云端

## Trend - 2019技术趋势
1. Mobile Development **Choose One**
    There are some framewors that allow us to create native apps with web technologies.
    * React Native - 使用React构建原生应用
    * NativeScript -  Angular, Type, Java
    * lonic - HTML/CSS/JS 实现混合应用
    * Flutter - 使用Dart语言开发原生应用的移动端SDK
    * Xamarin - 使用C#开发的移动端应用
2. Desktop Apps With Electron
    Electron is used to build powerful cross-platform desktop applications using JavaScript.
    * Uses Chromiun & Node.js - 使用到Chromiun内核和Node.js
    * Compatible with Windows、Mac & Linux - 兼容Windows, Mac & Linux
    * Crash reporting, debugging & profiling - 崩溃报告, 调试和性能分析
3. GraphQL & Apollo
    GraphQL is a revolutionary new way to think about APIs. Query language that is much less rigid than standard REST.
    * Ask for only what you want - 只查询你想要的东西
    * Front & back end can collaborate more smoothly - 前端和后端可以合作得更为顺利
    * Writing queries are very easy and simmilar to JSON - 查询语句非常简单且很像JSON语句
    * Apollo is a client to make requests to a GraphQL server - Apollo是一个发送请求到GraphQL的客户端
    * Used with the Gatsby static site generator - 使用的是Gatsby静态站点生成器
4. TypeScript
    TypeScript is a superset of JS with additional featires including static typing.
    * Types for variables, functions, etc - 变量, 函数等类型
    * Classes - 类
    * Other ES6-like features - 其他ES6的特性
    * Used in Angular but can be inplement in React & Vue - 在Angular中被使用到, 同时也可以在React和Vue中被使用
5. Serverless Architecture - 无服务架构
    Eilminate the need for creating and managing your own server
    * Used 3rd party services to execute "Serverless Functions" (FaaS) - 使用第三服务执行“无服务器功能”
    * Examples are AWS, Netlify & Firebase - 例如 AWS, Netify & Firebase
    * Popular with Gatsby static sites - 在Gatsby静态站点生成器很流行
    * Serverless framework - 无服务框架
6. AI & Machine Learning
    AI & Machine Learning have been huge in almost every area of propramming & technology including web development.
    AI和机器学习已经被广泛应用在所有的程序和技术中, 甚至包括web开发中.
    * Machine learning can allow web apps to adapt over time - 机器学习可以允许Web应用程序随时间进行调整
    * AI has a long way to go but I suspect we will see more of it in web dev - 虽然AI还有很长的路要走, 但是我们会看到它会更多的用在web中
    * Used heavily in Python but we also have JS libraries like Tensortflow.js and Brain.js -  虽然目前绝大多数都是Python写的, 但也有Tensorflow.js和Brain.js这些JS的库
7. Blockchain Technology
    Companies are using Blockchain for digital transactions in order to make them more exfficient and secure.
    * Solidity - Language for implementing contracts - Solidity(一门智能合约的编程语言)
    * Mist - Used for storing Ethereum, sending transactions & contracts - Mist(以太坊开发的浏览器, 用于发送交易和合约)
    * Coinbase API - Blockchain devs can easily build apps and integrate Bitcoin - 比特币API(可以构建app和整和比特币的区块链开发)
8. PWA
    Progressive Web Apps are regular web apps but give the user a native app experience in terms of layout and functionality - Progressive Web Apps是一个web app但是在功能和样式上给用户带来原生应用使用体验的一项技术.
    * Responsive to fit any form fator - 响应式
    * Server workers for offline availability - 在离线环境下也能提供服务
    * App-like interactions - 类似APP交互
    * HTTPS
    * Reliable, Fast & Engaging - 可靠、迅速、更好
9. Web Assembly
    Assembly-like binary format for code that can be executed by web browsers. Can be generated from higher level languages like C/C++&Rust.
    类似汇编的二进制格式的代码可以被浏览器执行. 可以使用类似C/c++和Rust等高级语言进行编写
    * Faster than JavaScript - 比JavaScript执行效率快
    * Secure-Enfore same origin & security policies in the browser - 更安全 – 强制的浏览器同源和安全协议
    * Open & debuggable - 开放 & 可调试
