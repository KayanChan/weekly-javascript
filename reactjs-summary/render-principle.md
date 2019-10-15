### React渲染原理
#### Virtual Dom
  > 对实际Dom的一个抽象，是一个js对象(标签名，属性，子元素), **真实的 DOM 树转换成 Javascript 对象树**。
  > react所有的表层操作实际上是在操作Virtual dom(经过 Diff 算法会计算出 Virtual DOM 的差异，然后将这些差异进行实际的DOM操作更新页面)。

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

  ##### JSX 如何生成Element
  > JSX: 由于js对象描述的篇幅过长，于是通过扩展js的语法，即`jsx`来处理。实际`jsx`会通过`Babel编译+React.js的构造`得到`js对象`，从而去操作`DOM`（`React-DOM.render`）

  ```javascript
  class HelloWorld extends Component {
    // 承载了构建HTML结构化页面的职责（View层组件化）
    render() {
      return <div>Hello World !</div>
    }
  }

  _createClass(HelloWorld, [{
    key: 'render',
    value: function render() {
      return React.createElement('div', null, 'Hello World !')
    }
  }])
  ```

  1. `React组件`通过`Babel`编译到纯javascript
  2. `React.createElement`就是用于创建`ReactElemet`实例对象，即虚拟元素`Virtual Element`(真实Dom元素的对应)，可彼此嵌套和混合
  3. 在内存中完成虚拟元素`Virtual Element`构建与更新(不会真正渲染到真实Dom中去)
  4. 每次数据更新后，重新计算`Virtual Dom`，并和上一次生成的`Virtual Dom`做对比，对发生变化的部分做批量更新


  ##### Element 如何生成DOM
  `ReactDom.render = (ReactElemnt, HTMLElement |SVGElement) => ReactDomRender`
  1. 函数`instantiateReactComponent(node)`创建一个`ReactComponent`实例(具有基本的数据结构：`ReactComponent`类),并return这个实例
    * 当 node 为空的时候，初始化空组件。
    * 当 node 为对象，类型 type 字段标记为是字符串，初始化 DOM 标签。否则初始化自定义组件。
    * 当 node 为字符串或者数字时，初始化文本组件。
  2. 创建了`ReactComponent`实例后，调用component的`mountComponent`方法(批量mount),开始渲染DOM

#### [生命周期管理](https://github.com/aermin/blog/issues/55)
  ##### React组件
    1. React组件由属性`props`、状态`state`、生命周期方法组成
    2. 一旦接受到的参数 props 或自身状态 state 有所改变，React组件就会执行相应的生命周期方法。

  ##### 生命周期阶段(react16版前后具体钩子函数有区别)
    1. 组件初始化(initialization)阶段
    2. 组件的挂载(Mounting)阶段
    3. 组件的更新(update)阶段
    4. 组件的卸载(unMount)阶段

#### Diff算法: Diff算法用于计算出两个virtual dom的差异，是React中开销最大的地方
  * 不使用跨层级移动节点的操作
  * 对于条件渲染多个节点时，尽量采用隐藏等方式切换节点，而不是替换节点
  * 尽量避免将后面的子节点移动到前面的操作，当节点数量较多时，会产生一定的性能问题

#### React setState 运行机制
  * `setState`是异步操作函数
  * `setState`是同步执行的，但是`state`并不一定会同步更新
  * 经过React处理的事件(生命周期钩子和类似通过onClick引发的合成事件)是不会同步更新`this.state`
  * 通过`addEventListener`、`setTimeout/setInterval`、`promise`等异步方式处理的则会同步更新`this.state`
  
  ##### 同步批量执行
    1. 多次同步执行的setState,会提取单次传递setState的对象，
    2. 把他们合并在一起形成一个新的单一对象，并用这个单一的对象去做setState的事情，
    3. 就像Object.assign的对象合并，后一个key值会覆盖前面的key值
      ```javascript
      const a = {name : 'kong', age : '17'}
      const b = {name : 'fang', sex : 'men'}
      Object.assign({}, a, b);
      //{name : 'fang', age : '17', sex : 'men'}
      ```

  ##### 同步更新策略
  * `React`的`setState`函数实现中，会根据变量`isBatchingUpdates`来判断 **直接更新** or **放在队列中,积攒着一次引发更新过程**
  * `isBatchingUpdates`默认是`false`，也就表示`setState`会同步更新`this.state`
  * 当React在调用事件处理函数之前就会调用这个`batchedUpdates`，切换`isBatchingUpdates`的值
  * 只同步执行不同步更新的目的是把`Virtual DOM` 和 `DOM 树`操作降到最小，用于提高性能。

  ##### 保证setState的同步更新的两种方式
  1. 利用setState在状态更新完毕后的回调操作(第二个参数) + ES7的`Async/Await`实现异步转同步
    ```javascript
      class Count extends React.Component {
      constructor(props) {
        super(props);
        this.state = {
          count: 0
        };
      }
      // componentDidMount() {
      //   // setState函数并不会阻塞等待状态更新完毕，所以UI显示1
      //   this.setState({count: 1}, () => {
      //     console.log(this.state.count); // 1
      //   });
      //   console.log(this.state.count); // 0
      // }

      // Promise来封装setState
      setStateAsync(state) {
        return new Promise((resolve) => {
          this.setState(state, resolve);
        });
      }
      async componentDidMount() {
        // async 表示这是一个async函数，await只能用在这个函数里面
        // await 表示在这里等待promise对象返回结果了，再继续执行
        await this.setState({count: 1}, () => {
          console.log(this.state.count); // 1
        });
        console.log(this.state.count); // 1
      }
      render() {
        return (<button>{this.state.count}</button>)
      }
    }
    ```
    
  2. 传入状态计算函数
    ```javascript
    class IncrementCount extends React.Component {
    constructor(props) {
      super(props);
      this.state = {
        count: 0
      };
    }

    incrementCount() {
      // 1,2,3没有达到期望
      // this.setState({
      //   count: this.state.count + 1
      // });

      // 3,6,9达到期望
      this.setState((prevState) => {
        return {count: prevState.count + 1}
      })
    }

    handleIncrementCount() {
      this.incrementCount();
      this.incrementCount();
      this.incrementCount();
    }

    render() {
      return (<button onClick={() => this.handleIncrementCount()}>{this.state.count}</button>);
    }
    ```