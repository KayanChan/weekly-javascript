### Virtual Dom
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