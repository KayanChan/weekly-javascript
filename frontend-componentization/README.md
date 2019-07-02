#### 基础的 React.js 的概念
@2019-07-02 整理来自[前端组件化](http://huziketang.mangojuice.top/books/react/lesson2)
##### 为什么要对前端页面进行组件化？
> 组件化可以帮助我们解决前端结构的复用性问题，整个页面可以由这样的不同的组件组合、嵌套构成。

> 一个组件有自己的显示形态（上面的 HTML 结构和内容）行为，组件的显示形态和行为可以由数据状态（state）和配置参数（props）共同决定。数据状态和配置参数的改变都会影响到这个组件的显示形态。

> 当数据变化的时候，组件的显示需要更新。所以如果组件化的模式能提供一种高效的方式自动化地帮助我们更新页面，那也就可以大大地降低我们代码的复杂度，带来更好的可维护性。

* step1: 首先实现了一个简单的[点赞功能](https://github.com/KayanChan/weekly-javascript/blob/master/frontend-componentization/like.html)，点击切换点赞状态
  ```javascript
  const button = document.querySelector('.like-btn')
  const buttonText = document.querySelector('.like-text')
  let isLiked = false
  button.addEventListener('click', () => {
    isLiked = !isLiked
    buttonText.innerHTML = isLiked ? '取消' : '点赞'
  })
  ```

* step2: 通过类构建实例，达到结构复用，使[其](https://github.com/KayanChan/weekly-javascript/blob/master/frontend-componentization/like-class.html)具备一定的复用性
  ```javascript
  class LikeButton {
    render() {
      return `
        <button class='like-btn'>
          <span class='like-text'>点赞</span>
          <span>👍</span>
        </button>
      `
    }
  }
  ```

* step3: 简单的[组件化](https://github.com/KayanChan/weekly-javascript/blob/master/frontend-componentization/like-simple-componentization.html)
  ```javascript
    const createDOMFromString = (domString) => {
      const div = document.createElement('div')
      div.innerHTML = domString
      return div
    }

    class LikeButton {
      constructor() {
        this.state = {
          isLiked: false
        }
      }
      changeLikeText() {
        const likeText = this.el.querySelector('.like-text')
        this.state.isLiked = !this.state.isLiked
        likeText.innerHTML = this.state.isLiked ? '取消' : '点赞'
      }
      render() {
        this.el = createDOMFromString(`
          <button class='like-btn'>
            <span class='like-text'>点赞</span>
            <span>👍</span>
          </button>
        `)
        /* bind里面的this指向当前实例，否则内部this会指向this.el */
        this.el.addEventListener('click', this.changeLikeText.bind(this), false)
        return this.el
      }
    }
  ```

* step4: [优化DOM操作](https://github.com/KayanChan/weekly-javascript/blob/master/frontend-componentization/like-optimize-dom.html): 一旦状态发生改变，就重新调用`render`方法，构建一个新的`DOM元素`
  ```javascript
    class LikeButton {
      constructor() {
        this.state = {
          isLiked: false
        }
      }

      setState(state) {
        const oldEl = this.el
        this.state = state
        this.el = this.render()
        if(this.onStateChange) this.onStateChange(oldEl, this.el)
      }

      changeLikeText() {
        this.setState({
          isLiked: !this.state.isLiked
        })
      }

      render() {
        console.log('render')
        console.log(this.state)
        this.el = createDOMFromString(`
          <button class='like-btn'>
            <span class='like-text'>${this.state.isLiked ? '取消' : '点赞'}</span>
            <span>👍</span>
          </button>
        `)
        this.el.addEventListener('click', this.changeLikeText.bind(this), false)
        return this.el
      }
    }
    const wrapper = document.querySelector('.wrapper')
    const likeButton1 = new LikeButton()
    wrapper.appendChild(likeButton1.render())
    likeButton1.onStateChange = (oldEl, newEl) => {
      wrapper.insertBefore(newEl, oldEl)
      wrapper.removeChild(oldEl)
    }
  ```

* step5: 把[这种模式](https://github.com/KayanChan/weekly-javascript/blob/master/frontend-componentization/like-abstract-public-component-class.html)抽象出来，代码更灵活，可以写更多组件
  ```javascript
  class Component {
    constructor(props = {}) {
      this.props = props
    }
    setState(state) {
      const oldEl = this.el
      this.state = state
      this._renderDOM()
      if(this.onStateChange) this.onStateChange(oldEl, this.el)
    }

    _renderDOM() {
      this.el = createDOMFromString(this.render())
      if(this.onClick) this.el.addEventListener('click', this.onClick.bind(this), false)
      return this.el
    }
  }
  const createDOMFromString = (domString) => {
    const div = document.createElement('div')
    div.innerHTML = domString
    return div
  }

  const mount = (component, wrapper) => {
    wrapper.appendChild(component._renderDOM())
    component.onStateChange = (oldEl, newEl) => {
      wrapper.insertBefore(newEl, oldEl)
      wrapper.removeChild(oldEl)
    }
  }
  ```

  *点赞组件*
  ```javascript
    class LikeButton extends Component {
      constructor(props) {
        super(props)
        this.state = {isLiked: false}
      }

      onClick() {
        this.setState({
          isLiked: !this.state.isLiked
        })
      }

      render() {
        return `
          <button class='like-btn' style="background-color: ${this.props.bgColor}">
            <span class='like-text'>${this.state.isLiked ? '取消' : '点赞'}</span>
            <span>👍</span>
          </button>
        `
      }
    }

    mount(new LikeButton({bgColor: '#999'}), document.querySelector('.wrapper'))
  ```

  *计数器组件*
  ```javascript
    class Counter extends Component {
      constructor(props) {
        super(props)
        this.state = {count: 0}
      }

      onClick() {
        this.setState({
          count: ++this.state.count
        })
      }

      render() {
        return `<button>计数器</button> <span>${this.state.count}</span>`
      }
    }

    mount(new Counter(), document.querySelector('.wrapper'))
  ```
