### 第二部分 生命周期
@2019-07-03 整理出自[这里](http://huziketang.mangojuice.top/books/react/lesson17)

#### 组件挂载阶段的过程
  * `React.js`的页面挂载
    ```javascript
    ReactDOM.render(
      <Header />, 
      document.getElementById('root')
    )
    ```
  * 通过`Babel编译`和`React.js的构造`得到`js对象`
    ```javascript
    ReactDOM.render(
      React.createElement(Header, null),
      document.getElementById('root')
    )
    ```
  * `js对象`是如何操作`DOM`
    ```javascript
    // 实例化一个实例
    const header = new Header(props, children)

    // 调用实例组件内部的render得到渲染内容，即JSX对象
    const headerJsxObject = header.render()

    // 创建元素
    const headerDOM = createDOMFromJsxObject(headerJsxObject)

    // 插入到根节点
    document.getElementById('root').appendChild(headerDOM)
    ```

#### 组件挂载阶段的钩子函数

  * constructor: 组件自身的状态的初始化（state初始化）

  * componentWillMount： 组件挂载开始之前，在组件调用`render`方法之前调用（Ajax 数据的拉取操作、一些定时器的启动）

  * render: `DOM`元素已经插入页面，视图渲染

  * componentDidMount: 组件挂载完成以后，也就是`DOM`元素已经插入页面后调用（依赖的DOM，如动画的启动, 自动focus）

  * componentWillUnmount: 组件对应的`DOM`元素从页面中删除之前调用（定时器的清除）

  > 在componentDidMount事件中想要打印出setState之后的值，由于异步分原因，需要在`setState`方法中加入一个回调函数
  > this.setState({ height: height},()=>console.log(this.state.height))

#### 组件更新阶段的钩子函数

  > 组件更新阶段: `setState`导致`React.js`重新渲染组件并且把组件的变化应用到 DOM 元素上的过程

  * shouldComponentUpdate(nextProps, nextState): 控制组件是否重新渲染。如果返回 false 组件就不会重新渲染，性能优化上非常有用（也可以通过继承`React.PureComponent`来代替）

  * componentWillReceiveProps(nextProps)： 组件从父组件接收到新的`props`之前调用

  * componentWillUpdate: 组件开始重新渲染之前调用

  * componentDidUpdate: 组件重新渲染并且把更改变更到真实的`DOM`以后调用

#### ref & React.js的DOM操作
  * 在`JSX元素`的`ref`属性来获取已经挂载的`DOM节点`
  * `ref`属性的值是一个函数，当该元素在页面上挂载完成就会调用这个函数
  ```javascript
  ...
  <input type="text" value={this.state.value} onChange={this.handleUsernameChange.bind(this)} ref={(input => this.input = input)}/>
  ...
  ```

#### props.children & 容器组件
  * 组件内部通过`props.children`可获得组件中所嵌套的内部(`JSX结构`)
  * `props.children`是数组机制，组件内部可灵活安置各部分的`JSX结构`
  ```javascript
  import React, { Component } from 'react'

  class PropsChildren extends Component {
      render() {
          return (
              <div className="wrapper">{this.props.children[0]}{this.props.children[1]}</div>
          )
      }
  }

  export default PropsChildren
  ```

  ```javascript
    ...
    <PropsChildren>
      <div className="content">content</div>
      <div className="content">content2</div>
    </PropsChildren>
    ...
  ```

#### dangerouslySetInnerHTML
  * 出于安全考虑的原因（XSS 攻击），在`React.js`当中所有的表达式插入的内容都会被自动转义
  * 属性`dangerouslySetInnerHTML={{__html: this.state.x}}`可以把HTML结构渲染处理，避免被转义
  ```javascript
  class DangerouslySetInnerHTML extends Component {
    constructor() {
        super()
        this.state = {
            content: '<div>content</div>'
        }
    }
    render() {
        return (
            <div dangerouslySetInnerHTML={{__html: this.state.content}}></div>
        )
    }
  }

#### 类型验证：第三方库`prop-types`

  * 安装第三方库，检查组件的配置参数的类型
    ```bash
    npm install --save prop-types
    ```

  * 组件添加类属性`propTypes`
  ```javascript
  class CommentList extends Component {
    static propTypes = {
      comment: PropTypes.array
      // comment: Protypes.array.isRequired
    }
    static defaultProps = {
      lists: []
    }
    render() {
      return (
        this.props.lists.map((item, index) => {
          return (
            <Comment key={index} comment={item} />
          )
        })
      )
    }
  }
  ```

  * `PropTypes`提供一系列的数据类型，通过`isRequired`关键字来强制组件某个参数必须传入
  ```javascript
  PropTypes.array
  PropTypes.bool
  PropTypes.func
  PropTypes.number
  PropTypes.object
  PropTypes.string
  ```

#### 推荐组件内容编写顺序

  1. `static`开头的类属性，如`defaultProps`，`propTypes`

  2. 构造函数`constructor`

  3. `getter/setter`

  4. 组件生命周期(钩子函数)

  5. `_`开头的私有方法

  6. 事件监听方法，`handle*`

  7. `render*`render里面的内容分到不同函数处理

  8. `render`

  > 钩子函数尽量调用私有方法，内部业务在私有方法处理