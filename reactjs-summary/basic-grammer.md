### 第一部分 基础语法

#### 脚手架
  ```bash
  npm install -g create-react-app

  create-react-app hello-react
  cd hello-react
  npm start
  ```

#### `index.js`头部
  * 引入`React`和`React.js`的组件父类`Component`
    `import React, { Component } from 'react'`

  * 处理React组件的渲染
    `import ReactROM from 'react-dom'`

#### JSX原理
  每个 DOM 元素的结构都可以用 JavaScript 的对象来描述。一个`DOM`元素包含的信息其实只有三个：标签名，属性，子元素
  ```javascript
  {
    tag: 'div',
    attrs: { className: 'box', id: 'content'},
    children: [
      {
        tag: 'div',
        arrts: { className: 'title' },
        children: ['Hello']
      },
      {
        tag: 'button',
        attrs: null,
        children: ['Click']
      }
    ]
  }
  ```
  `React.createElement`会构建一个 JavaScript 对象来描述`HTML`结构的信息，包括标签名、属性、还有子元素等。由于js对象描述的篇幅过长，于是通过扩展js的语法，即`jsx`来处理。实际`jsx`会通过`Babel编译+React.js的构造`得到`js对象`，从而去操作`DOM`（`React-DOM.render`）。另外，`jsx`不直接操作`DOM`是避免浏览器的重排，性能的优化；而且得到一个表示UI的结构和信息的对象，不一定会把元素渲染到浏览器的普通页面上，如`canvas`。

#### render方法
  * 一个组件类必须要实现一个`render`方法
  * `render`方法返回一个`JSX对象`
  * 必须要用一个外层的`JSX`元素把所有内容包裹
  * 在`JSX`当中以插入`JavaScript`的代码(`变量`、`表达式`、`函数执行`), 用`{}`包裹
  * `{}`不仅可以用在标签内部，也可以用在标签属性上
  * `React.js`定义了`className`来给元素添加类名，`label`元素的`for`在`JSX`中用`htmlFor`代替

  ```javascript
  class UseRender extends Component {
    render() {
        const text = 'hello'
        const isGood = true
        const className = 'box'
        function showTitle() {
            return 'hello react'
        }
        return (
            <div className={className}>
                <div>{text}</div>
                <div>{isGood ? '好' : '不好'}</div>
                <div>{showTitle()}</div>
                <label htmlFor="radioname">
                    <input type="radio" name="radioname" value="all"/>
                    选中
                </label>
            </div>
        )
    }
  }
  ```

#### 组件树
  * 自定义组件必须**大写字母**开头，普通HTML标签小写字母开头
  * 组件与组件之间不断组合、嵌套，构成组件树

#### 组件中的事件监听
  * 监听某个元素的某事件时，使用`on*`的属性，不需要考虑兼容问题
  * 事件监听只能用在普通的`HTML`的标签上，而不能用在组件标签上
  * 事件监听函数会被自动传入一个`event`对象，具有`event.stopPropagation`、`event.preventDefault`
  * 在事件函数当中使用当前的实例，需要手动地将实例方法`bind`到当前实例上再传入给`React.js`

  ```javascript
  class UseEventListen extends Component {
    constructor() {
        super()
        this.state = {
            text: '你点击了外面'
        }
    }
    clickOuter() {
        alert(this.state.text)
    }
    clickInter(event) {
        if(event) event.stopPropagation();
    }
    render() {
        return (
            <div onClick={this.clickOuter.bind(this)}>
                外面点击一下
                <div onClick={this.clickInter}>里面点击没反应的</div>
            </div>
        )
    }
  }
  ```

#### state & setState
  * `state`用来储存组件的数据状态，`state`对象在构造函数中初始化
  * `setState`方法由父类`Component`提供，用于更新组件的`state`，并且重新调用`render`，从而更新视图
  * `setState`接受一个对象或者函数作为参数
  * 调用`setState`时，`React.js`会把这个对象放到一个更新队列里面，稍后才会从队列当中把新的状态(最终的状态)提取出来合并到`state`当中，然后再触发组件更新，期间的状态可以通过`prevState`获得

  ```javascript
  class StateAndSetState extends Component {
    constructor() {
        super()
        this.state = {
            isLiked: false,
            isDeleted: false
        }
    }

    toggleLike() {
        this.setState({
            isLiked: !this.state.isLiked
        })
    }

    toggleDelete() {
        this.setState((prevState) => {
            return {isDeleted: !prevState.isDeleted}
        })
    }

    render() {
        return (
            <div>
                <button type="button" onClick={this.toggleLike.bind(this)}>{this.state.isLiked ? '取消' : '点赞'}</button>
                <button type="button" onClick={this.toggleDelete.bind(this)}>{this.state.isDeleted ? '取消' : '删除'}</button>
            </div>
        )
    }
  }
  ```

#### props & defaultProps
  * `props`用来储存组件的配置数据，在组件标签上加属性来传入配置参数，组件内部通过`this.props`获得
  * 组件可添加类属性`defaulProps`用来处理默认配置
  * `props`在组件内不可变，需要通过组件使用者主动通过重新渲染的方式(`render`)来把新的`props`传进来，即通过父层组件的`setState`来更新当前组件的`props`
  ```javascript
  class UseProps extends Component {
      static defaultProps = {
          unLikedText: '取消',
          likedText: '点赞'
      }
      constructor(prop) {
          super(prop)
          this.state = {
              isLiked: false
          }
      }
      toggleLike() {
          this.setState({
              isLiked: !this.state.isLiked
          })
      }
      render() {
          return (
              <button type="button" onClick={this.toggleLike.bind(this)}>{this.state.isLiked ? this.props.unLikedText : this.props.likedText}</button>
          )
      }
  }
  ```
  ```javascript
  class ParentState extends Component {
      constructor() {
          super()
          this.state = {
              unLikedText: '取消',
              likedText: '点赞'
          }
      }
      changeText() {
          this.setState(() => {
              return {
                  unLikedText: '已赞',
                  likedText: '赞'
              }
          })
      }
      render() {
          return (
              <div>
                  <UseProps unLikedText={this.state.unLikedText} likedText={this.state.likedText}/>
                  <button type="button" onClick={this.changeText.bind(this)}>改变按钮文案</button>
              </div>
          )
      }
  }
  ```
  ```javascript
  ...
  <UseProps />
  <UseProps unLikedText="已赞" likedText="赞" />
  <ParentState />
  ...
  ```

#### state vs props
  **state**
  1. 用于组件保存、控制、修改自己的可变状态
  2. 在组件内部初始化，可以被组件自身修改，而外部不能访问也不能修改
  3. 通过`this.setState`方法来更新视图

  **props**
  1. 让使用该组件的父组件可以传入参数来配置该组件
  2. 组件内部无法控制也无法修改
  3. 通过外部组件主动传入新的`props`来达到更新效果

  * 尽量少地用`state`，尽量多地用`props`
  * 无状态组件(stateless component)： 没有state的组件；
    有状态组件(stateful component)： 设置了state的状态的组件
  * 状态会带来管理的复杂性，尽量多地写**无状态组件**
  * 函数式组件： 定义了不能使用state，即为无状态组件
    ```javascript
    const HelloWorld = (props) => {
      const sayHi = (event) => alert('Hello World')
      return (
        <div onClick={sayHi}>Hello World</div>
      )
    }
    ```

#### 渲染列表数据
  * 使用`map`来渲染列表数据
  * 对于用表达式套数组罗列到页面上的元素，都要为每个元素加上`key`属性(每个元素唯一的标识)
  ```javascript
  class List extends Component {
    render() {
        const lists = [
            { username: 'Jerry', age: 21, gender: 'male' },
            { username: 'Tomy', age: 22, gender: 'male' }
        ]
        return (
            lists.map((user, index) => {
                return (
                    <div key={index}>
                        <div>姓名：{user.username}</div>
                        <div>年龄：{user.age}</div>
                        <div>性别：{user.gender}</div>
                        <hr />
                    </div>
                )
            })
        )
    }
  }
  ```