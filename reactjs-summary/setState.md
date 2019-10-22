### React setState 运行机制
  * `setState`是异步操作函数
  * `setState`是同步执行的，但是`state`并不一定会同步更新
  * 经过React处理的事件(生命周期钩子和类似通过onClick引发的合成事件)是不会同步更新`this.state`
  * 通过`addEventListener`、`setTimeout/setInterval`、`promise`等异步方式处理的则会同步更新`this.state`
  * 受控组件(表单元素（如`<input>、 <textarea> 和 <select>`）之类的)通常自己维护`state`，并根据用户输入进行更新
  
  #### 同步批量执行
    1. 多次同步执行的setState,会提取单次传递setState的对象，
    2. 把他们合并在一起形成一个新的单一对象，并用这个单一的对象去做setState的事情，
    3. 就像Object.assign的对象合并，后一个key值会覆盖前面的key值
      ```javascript
      const a = {name : 'kong', age : '17'}
      const b = {name : 'fang', sex : 'men'}
      Object.assign({}, a, b);
      //{name : 'fang', age : '17', sex : 'men'}
      ```

  #### 同步更新策略
  * `React`的`setState`函数实现中，会根据变量`isBatchingUpdates`来判断 **直接更新** or **放在队列中,积攒着一次引发更新过程**
  * `isBatchingUpdates`默认是`false`，也就表示`setState`会同步更新`this.state`
  * 当React在调用事件处理函数之前就会调用这个`batchedUpdates`，切换`isBatchingUpdates`的值
  * 只同步执行不同步更新的目的是把`Virtual DOM` 和 `DOM 树`操作降到最小，用于提高性能。

  #### 保证setState的同步更新的两种方式
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
      this.setState((prevState, props) => {
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