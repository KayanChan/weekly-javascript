### 组件
#### 函数组件(**尽量使用无状态组件**)
  > 接收唯一带有数据的`props`（代表属性）对象与并返回一个`React`元素
  > 本质上就是`JavaScript`函数
  > 无状态组件：不涉及到要`state`状态的操作
  ```javascript
  function Welcome(props) {
    // 使用ref来获取组件挂载到dom中后所指向的dom元素
    return <h1>Hello, <span ref={(node) => ref = node}>{props.name}</span></h1>;
  }
  ```

  ##### 特点
  1. 组件不会被实例化，整体渲染性能得到提升: 组件被精简成一个render方法的函数来实现的,无实例化过程也就不需要分配多余的内存
  2. 组件不能访问this对象: 由于没有实例化过程
  3. 组件无法访问生命周期的方法
  4. 无状态组件只能访问输入的props

  > 无状态组件内部其实是可以使用ref功能的
  > 虽然不能通过`this.refs`访问到，但是可以通过将ref内容保存到无状态组件内部的一个本地变量中获取到

#### `React.createClass`(**不建议使用此方式,仅了解**)
  > `ES5`的原生的JavaScript来实现的React组件

  ```javascript
  var InputControlES5 = React.createClass({
    propTypes: {//定义传入props中的属性各种类型
        initialValue: React.PropTypes.string
    },
    defaultProps: { //组件默认的props对象
        initialValue: ''
    },
    // 设置 initial state
    getInitialState: function() {//组件相关的状态对象
        return {
            text: this.props.initialValue || 'placeholder'
        };
    },
    handleChange: function(event) {
        consoel.log(this);//this represents react component instance
        this.setState({
            text: event.target.value
        });
    },
    render: function() {
        return (
            <div>
                Type something:
                <input onChange={this.handleChange} value={this.state.text} />
            </div>
        );
    }
  });
  ```
  ##### 特点
  1. 创建有状态的组件，要被实例化的，并且可以访问组件的生命周期方法
  2. 每一个成员函数的this都有React自动绑定，直接使用(见`handleChange内的console`)
  3. 有关组件props的属性类型及组件默认的属性会作为**组件实例的属性**来配置(`defaultProps`是使用`getDefaultProps`的方法来获取默认组件属性的)
  4. `state`是通过`getInitialState`方法来配置组件相关的状态
  5. 在创建组件时可以使用`mixins`属性，以数组的形式来混合类的集合

#### React.Component(**需要state、生命周期方法等推荐使用**)
  > 以ES6的形式来创建react的组件
  > 是React目前极为推荐的创建有状态组件的方式
  > 最终会取代`React.createClass`形式

  ```javascript
  class Contacts extends React.Component {
    static propTypes = {//类的静态属性
        name: React.PropTypes.string
    };

    static defaultProps = {//类的静态属性
        name: ''
    };

    constructor(props) {
      super(props);
      this.state = {};
    }
    handleClick() {
      console.log(this); // null
    }
    render() {
      return (
        <div onClick={this.handleClick}></div>
      );
  }
  ```

  ##### 特点
  1. 创建有状态的组件，要被实例化的，并且可以访问组件的生命周期方法
  2. 成员函数不会自动绑定this，需要开发者手动绑定，否则this不能获取当前组件实例对象(见`handleClick内的console`)
  3. 组件props的属性类型及组件默认的属性，通过**类(作为组件类)的静态属性**来配置的
  4. state是在constructor中像初始化组件属性一样声明的
  5. 不支持`Mixins`,可以用`Higher-Order Components`来取代

  ##### 手动绑定this
  1. 构造函数中绑定

```javascript
constructor(props) {
    super(props);
    this.handleClick = this.handleClick.bind(this);
}
```
  2. 使用bind来绑定`<div onClick={this.handleClick.bind(this)}></div>`
  3. 使用箭头函数绑定

```javascript
// 方法一：直接在DOM使用箭头函数
// 不建议，在 render 方法中使用箭头函数也会在每次组件渲染时创建一个新的函数，这会破坏基于恒等比较的性能优化。
// <div onClick={()=>this.handleClick()}></div>

// 方法二：函数定义时使用箭头函数，jsx直接使用this
	// jsx
	// <DatePicker onChange={this.handleChange}/>

    handleChange = (date) => {
      console.log(date)
      message.info(`您选择的日期是:${date.format('YYYY-MM-DD')}`)
      this.setState({date})
    }
```