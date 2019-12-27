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
- [ ] 第4章 连接管理
- [ ] 第5章 Web服务器
- [ ] 第6章 代理
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