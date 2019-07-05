### 第三部分 高阶部分
@2019-07-04 整理出自[这里](http://huziketang.mangojuice.top/books/react/lesson28)

#### 高阶组件
  * 高阶组件就是**一个函数**，接受**一个组件为参数**，它返回一个新的组件
  * 新组件会把参数中的组件将会作为子组件
  * 组件可能有着某些相同的逻辑，把这些逻辑抽离出来，放到高阶组件中进行复用
  * 高阶组件内部的包装组件和被包装组件之间通过`props`传递数据

  **原来的组件**
  ```javascript
  class InputWithUserName extends Component {
    /* 开始： 相当于复用这部分 */
    constructor() {
      super()
      this.state = {
        data: null
      }
    }
    componentWillMount() {
      let data = localStorage.getItem(name)
      this.setState({ data })
    }
    /* 结束： 相当于复用这部分 */
    render () {
      return <input value={this.state.data} />
    }
  }
  ```

  **使用高阶组件**
  ```javascript
  // LocalStorageActions.js
  import React, { Component } from 'react'

  export default (WrapperComponent, name) => {
      // 1. 构建一个新组建 NewComponent，复用从本地读取数据的功能
      class NewComponent extends Component {
          constructor() {
              super()
              this.satte = {
                  data: null
              }
          }
          componentWillMount() {
              // 3. 在挂载阶段，获得数据
              let data = localStorage.getItem(name)
              // 4. 通过 setState 把数据放到 state 中
              this.setState({ data })
          }
          render() {
              return (
                  // 2. 把传进来的组件 WrapperComponent 渲染出来
                  // 5. state.data 通过 props.data 传给 WrapperComponent
                  <WrapperComponent data={this.state.data}/>
              )
          }
      }
      // 6.返回新组件
      return NewComponent
  }

  // InputWithUserName.js
  import LocalStorageActions from './LocalStorageActions'

  class InputWithUserName extends Component {
    render() {
      return <input value={this.props.data} />
    }
  }

  // 高阶组件 wrapWithLoadData， 传入组件，返回新组件
  InputWithUserName = LocalStorageActions(InputWithUserName, 'username')
  export default InputWithUserName


  // TextareaWithContent.js
  import LocalStorageActions from './LocalStorageActions'
  class TextareaWithContent extends Component {
    render() {
      return (<textarea value={this.props.data} />)
    }
  }

  TextareaWithContent = LocalStorageActions(TextareaWithContent, 'content')
  export default TextareaWithContent
  ```


#### context (不建议使用，实际可通过`Redux`去处理)
  * `context`存放一些状态，某个组件下的子组件无须通过`props`不断传递，组件之间直接通过`context`来访问
  * 一个组件的`context`只有它的子组件能够访问，它的父组件是不能访问到的

  ```javascript
  // 父组件
  import React, { Component } from 'react'
  import PropTypes from 'prop-types'
  import Dad from '../components/Dad'
  class GrandPa extends Component {
      // 3.必写，验证context
      static childContextTypes = {
          themeColor: PropTypes.string
      }
      constructor() {
          super()
          // 1.state 初始化一个状态
          this.state = {
              themeColor: '#555'
          }
      }
      // 2.设置context
      getChildContext() {
          return {
              themeColor: this.state.themeColor
          }
      }
      render() {
          return (
              <div>
                  <div style={{color: this.state.themeColor}}>GrandPa</div>
                  <Dad />
              </div>)
      }
  }
  ```
  ```javascript
  // 子组件
  import React, { Component } from 'react'
  import PropTypes from 'prop-types'
  class Dad extends Component {
      // 4.声明状态和验证状态的类型
      static contextTypes = {
          themeColor: PropTypes.string
      }
      render() {
          // 5.获取context
          return (<div>
              <div style={{color: this.context.themeColor}}>Dad</div>
          </div>)
      }
  }
  ```