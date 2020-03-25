### weekly-javascript

#### @2019-07-01 [ES6的常用数组操作](https://github.com/KayanChan/weekly-javascript/blob/master/es6-summary/array.md)

#### @2019-07-02  [前端组件化](https://github.com/KayanChan/weekly-javascript/blob/master/frontend-componentization/README.md)（理解基础的 React.js 的概念）

   * 如何尽量减少手动`DOM 操作`：一旦状态发生改变，就重新调用`render`方法，构建一个新的`DOM 元素`(React)。
   * 通过类实现组件的继承，抽象出公共组件类`Component`

#### @2019-07-03 React.js汇总

##### catalog

   - [第一部分 基础语法](https://github.com/KayanChan/weekly-javascript/blob/master/reactjs-summary/basic-grammer.md)

   - [第二部分 生命周期](https://github.com/KayanChan/weekly-javascript/blob/master/reactjs-summary/life-cycle.md)

   - [第三部分 高阶组件](https://github.com/KayanChan/weekly-javascript/blob/master/reactjs-summary/high-order-component.md)
   
   - [第四部分 Redux](https://github.com/KayanChan/weekly-javascript/blob/master/reactjs-summary/Redux.md)

##### Question&Answer

   > 为什么`react-dom`不包含在`react`当中？

   > 如何更好的管理这种被多个组件所依赖或影响的状态？

#### @2019-07-04 [纯函数(Pure Function)](https://github.com/KayanChan/weekly-javascript/blob/master/js-summary/pure-function.md)

#### @2019-07-05 [ES6的`...`符号](https://github.com/KayanChan/weekly-javascript/blob/master/es6-summary/spread.md)： 浅复制对象，还可以覆盖、拓展对象属性

#### @2019-07-09 时钟的绘制
   * [原生js+DOM绘制](https://github.com/KayanChan/weekly-javascript/blob/master/clock/clock/dom-clock.html)
   * [canvas绘制](https://github.com/KayanChan/weekly-javascript/blob/master/clock/canvas-clock.html)
   * [使用Redux原理绘制](https://github.com/KayanChan/weekly-javascript/blob/master/clock/redux-clock.html)

#### @2019-10-14 Flex
   * display: flex  //设置Flex模式
   * flex-direction: column  [row|row-reverse|column|column-reverse] //决定元素是横排还是竖着排
   * flex-wrap: wrap  [nowrap|wrap|wrap-reverse] //决定元素换行格式
   * justify-content: space-between [flex-start|flex-end|center|space-between|space-around] //同一排下对齐方式，空格如何隔开各个元素
   * align-items: center [stretch|center|flex-start|flex-end|baseline] //同一排下元素如何对齐
   * align-content: space-between [stretch|center|flex-start|flex-end|space-between|space-around] //多行对齐方式

#### @2019-10-14 文本省略
   * 单行
      ```CSS
      width: 100%;
      white-space: no-wrap;
      text-overflow: ellipsis;
      overflow : hidden;
      ```
   * 多行: `-webkit-line-clamp` 指定行数
      ```CSS
      display: -webkit-box;
      -webkit-line-clamp: 3;
      -webkit-box-orient: vertical;
      text-overflow: ellipsis;
      overflow : hidden;
      ```

#### @2019-10-14 React核心原理
   * [Virtual Dom模型](https://github.com/KayanChan/weekly-javascript/blob/master/reactjs-summary/virtual-dom.md)
   * [生命周期管理](https://github.com/KayanChan/weekly-javascript/blob/master/reactjs-summary/life-cycle.md)
   * [setState运行机制](https://github.com/KayanChan/weekly-javascript/blob/master/reactjs-summary/setState.md)
   * [Diff算法](https://github.com/KayanChan/weekly-javascript/blob/master/reactjs-summary/diff.md)
   * [组件](https://github.com/KayanChan/weekly-javascript/blob/master/reactjs-summary/component.md)
   * React patch、事件系统

#### @2019-10-21 [(未完待补充)JSS与React集成](https://github.com/KayanChan/weekly-javascript/blob/master/reactjs-summary/jss.md)

#### @2019-10-21 [MobX](https://github.com/KayanChan/weekly-javascript/blob/master/reactjs-summary/Mobx.md)

#### @2019-10-22 [react使用装饰器@](https://github.com/KayanChan/weekly-javascript/blob/master/reactjs-summary/decorator.md)

#### @2019-10-30 [webpack基本使用](https://github.com/KayanChan/weekly-javascript/blob/master/webpack/basic.md)

#### @2019-12-05 [长列表优化](https://github.com/KayanChan/weekly-javascript/blob/master/js-summary/long-list.md)

#### @2019-12-09 [utils.js常见JS方法封装](https://github.com/KayanChan/weekly-javascript/blob/master/js-summary/utilsjs.md)
   * fn.apply(obj, args): obj将代替fn类里的this;args是**数组**，作为参数传给fn
   * fn.call(obj, params): obj将代替fn类里的this;params是参数列表
   > apply与call区别在于参数列表不同

#### @2019-12-23 [2019web前端进阶指南](https://github.com/KayanChan/weekly-javascript/blob/master/frontend-guide/2019-advanced-guide.md)

#### @2019-12-24 http权威指南
- [x] [第1章 HTTP概述](https://github.com/KayanChan/weekly-javascript/blob/master/http/%E7%AC%AC1%E7%AB%A0_HTTP%E6%A6%82%E8%BF%B0.md)
- [x] [第2章 URL与资源](https://github.com/KayanChan/weekly-javascript/blob/master/http/%E7%AC%AC2%E7%AB%A0_URL%E4%B8%8E%E8%B5%84%E6%BA%90.md)
- [x] [第3章 HTTP报文](https://github.com/KayanChan/weekly-javascript/blob/master/http/%E7%AC%AC3%E7%AB%A0_HTTP%E6%8A%A5%E6%96%87.md)
- [x] [第4章 连接管理](https://github.com/KayanChan/weekly-javascript/blob/master/http/%E7%AC%AC4%E7%AB%A0_%E8%BF%9E%E6%8E%A5%E7%AE%A1%E7%90%86.md)
- [x] [第5章 Web服务器](https://github.com/KayanChan/weekly-javascript/blob/master/http/%E7%AC%AC5%E7%AB%A0_Web%E6%9C%8D%E5%8A%A1%E5%99%A8.md)
- [x] [第6章 代理](https://github.com/KayanChan/weekly-javascript/blob/master/http/%E7%AC%AC6%E7%AB%A0_%E4%BB%A3%E7%90%86.md)
- [ ] 第7章 缓存
- [ ] 第8章 集成点：网关、隧道及中继
- [ ] 第9章 Web机器人
- [ ] 第10章 HTTP-NG
- [ ] 第11章 客户端识别与cookie机制
- [ ] 第12章 基本认证机制
- [ ] 第13章 摘要认证
- [ ] 第14章 安全HTTP
- [ ] 第15章 实体和编码
- [ ] 第16章 国际化
- [ ] 第17章 内容协商与转码
- [ ] 第18章 Web主机托管
- [ ] 第19章 发布系统
- [ ] 第20章 重定向与负载均衡
- [ ] 第21章 日志记录与使用情况跟踪

#### 2020-01-13 性能优化

##### 骨架屏减少用户等待体验
问题一：基于Webpack脚手架和Vue框架开发的项目，采用动态生成静态资源的链接，会打包生成一个依赖JS文件，一个业务JS文件；浏览器往往会并行下载多个外部静态资源，如果业务JS文件一旦先于依赖JS文件执行，则找不到依赖变量，页面就会卡死

优化：Webpack打包自动注入静态资源链接的形式，但快速迭代需求的情况下，需要修改几十个静态资源的版本号

问题二：为了缓解用户在等待页面渲染中的焦急心情，早已经在返回的HTML增加了骨架屏，但在 IOS 系统中骨架屏并不会出现，而是直接呈现出最终渲染的页面

常规的浏览器渲染机制：HTML解析器会从HTML文件的头部到尾部，逐个遍历这些节点，加入到DOM树中；遇到JS/CSS代码，控制权交给JS/CSS解析器；遇到外联的JS/CSS代码还在请求中，DOM树上有可视元素的话，浏览器通常会选择在这个时候，将一些内容提前渲染到屏幕上来

但在IOS系统中的WebView并没有将首屏直出的这部分HTML页面显示出来。HTML中直出的DOM结构会等待外部CSS和JS加载执行后才统一进行渲染

验证：红色div位于挂载元素之中，直接被生成的Vue页面替换掉了；绿色div是和Vue页面一起渲染出来
```html
<body>
   <div style="width:100%;height: 200px;background:green;"></div>
   <div id="app">
      <div style="width:100%;height: 200px;background:red;"></div>
   </div>
   <!-- built files will be auto injected -->
</body>
```

结果：PC浏览器会显示红绿div块，IOS系统中的WebView不显示红色div块，绿色div会与Vue页面同时显示
优化：采用待骨架屏加载完之后，再去动态引入JS和CSS，由于首页骨架屏的代码量本身并不大，待其加载后再去动态引入静态资源，时间影响不大，但又回到上面问题一

最终解决：采用了引入事件监听的方法，核心思想是待依赖文件都加载完之后，再去执行业务代码。保证了静态资源的并行下载，不影响原有下载方式；保证了代码执行的顺序

注意：
1. HTML不要写ES6代码，避免没有babel编译导致低版本不兼容
2. 生成多个JS标签，先挂载到虚拟的节点对象 再统一挂载到body上，减少页面的重绘
```javascript
var oFragment = document.createDocumentFragment();
var indexScript1 = document.createElement('script');
var indexScript2= document.createElement('script');
oFragment.appendChild(indexScript1);
oFragment.appendChild(indexScript2);
body.appendChild(oFragment);
```
3. 兼容本地开发，本地开发的时候仍然使用Webpack自动引入静态资源的形式，打包和线上的再用动态生成静态资源的方式

##### 楼层内部滚动懒加载
页面楼层懒加载，能够很有效的提高首页加载速度，减少不必要的请求。为了进一步减少首页不必要的加载，我们使用了 Vue-lazyload 插件，来实现组件的懒加载功能，并且使用预加载技术，让浏览器空闲时间先把该文件下载下来，避免用户滑动到商品楼测才去下载对应的静态资源。

##### PWA
PWA是一种思想和概念，目的就是对标原生app，将Web网站通过一系列的Web技术去优化它，提升其安全性，性能，流畅性，用户体验等各方面指标，最后达到用户就像在用app一样的感觉。

##### TypeScipt
TS是JavaScript的一个超集，主要提供了类型系统和对ES6的支持。它的出现让开发人员在编译阶段就能检测大部分错误，增加了代码的可读性和可维护性。

##### 核心数据减少请求接口时间
##### 使用Webp缩小图片大小
WebP是一种支持有损压缩和无损压缩的图片文件格式，派生自图像编码格式VP8。

#### 2020-01-14 [TypeScipt学习](https://github.com/KayanChan/weekly-javascript/blob/master/ts-summary/typescript.md)
[官网文档](http://www.typescriptlang.org/)
[非官方中文文档](https://www.tslang.cn/)
[参考文档](https://ts.xcatliu.com/)

#### 2020-01-15 [待阅：JS 函数式编程指南](https://legacy.gitbook.com/book/llh911001/mostly-adequate-guide-chinese/details)

#### 2020-03-25 host
Hosts文件主要作用是定义IP地址和主机名的映射关系，是一个映射IP地址和主机名的规定

在浏览器中通过域名访问网站，首先查看hosts文件中是否存在域名与IP的地址转换，如果存在则直接根据IP地址进行访问；否则向DNS服务器发送请求，根据返回结果中的IP进行访问

HOSTS文件是在`C:\windows\system32\drivers\etc`

用途：
1. 在hosts中配置了常用的网址和IP的映射关系，就省去了向DNS服务器发送请求获取IP的过程，从而`更快的访问网站速度`
2. 屏蔽网站，如在hosts中配置`127.0.0.1 www.baidu.com`，则访问百度时指向本地服务器地址，达到`屏蔽网站`的效果
3. 记录常用IP地址，可将常用的ip地址(如内网中使用的一些IP地址，IP地址通常比较难记)转为域名记录，即达到访问域名，实际访问IP地址

行首添加`#`以关闭映射转换(注释掉)