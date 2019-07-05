### 第一部分 Redux
@2019-07-05 整理出自[这里](http://huziketang.mangojuice.top/books/react/lesson30)

#### Redux的推演
* 定一个状态变量`appState`，页面渲染
  ```html
  <div id='title'></div>
  <div id='content'></div>
  ```

  ```javascript
  const appState = {
      title: {
          text: 'React.js',
          color: 'red'
      },
      content: {
          text: 'React',
          color: 'blue'
      }
  }

  function renderApp(appState) {
      renderTitle(appState.title)
      renderContent(appState.content)
  }

  function renderTitle(title) {
      const titleDOM = document.getElementById('title')
      titleDOM.innerHTML = title.text
      titleDOM.style.color = title.color
  }

  function renderContent(content) {
      const contentDOM = document.getElementById('content')
      contentDOM.innerHTML = content.text
      contentDOM.style.color = content.color
  }

  renderApp(appState)
  ```

* `appState`为共享状态，会被任意修改，故需要避免全局变量；
  解决思路为：模块（组件）之间可以共享数据，不能直接改，所有对数据的操作必须通过指定函数`dispatch`
  ```javascript
  function dispatch(action) {
      switch(action.type) {
          case 'UPDATE_TITLE_TEXT':
              appState.title.text = action.text
              break
          case 'UPDATE_CONTENT_COLOR':
              appState.content.color = action.color
              break
          default:
              break
      }
  }

  dispatch({type: 'UPDATE_TITLE_TEXT', text: 'hello'})
  dispatch({type: 'UPDATE_CONTENT_COLOR', color: 'green'})
  renderApp(appState)
  ```

* 针对不同的App可以通过**构建一个函数`createStore`，生产`state`和`dispatch`的集合**来处理内部状态
  ```javascript
  // 返回一个对象，包含 getState 和 dispatch 两个方法
  function createStore(state, stateChanger) {
      const getState = () => state

      const dispatch = (action) => stateChanger(state, action)

      return {getStore, dispatch}
  }

  function stateChanger(state, action) {
      switch(action.type) {
          case 'UPDATE_TITLE_TEXT':
              state.title.text = action.text
              break
          case 'UPDATE_CONTENT_COLOR':
              state.content.color = action.color
              break
          default:
              break
      }
  }

  const store = createStore(appState, stateChanger)
  // getState: 获取state
  renderApp(store.getState())

  // dispatch: 修改数据
  store.dispatch({type: 'UPDATE_TITLE_TEXT', text: 'hello'})
  store.dispatch({type: 'UPDATE_CONTENT_COLOR', color: 'green'})
  renderApp(store.getState())
  ```

* 监听数据的变化，自动更新视图(**观察者模式**)

  ```javascript
  function createStore(state, stateChanger) {
      // 存放回调函数
      const listeners = []
      // 添加回调函数，回调函数内容就是更新数据之后要处理的业务(如重新渲染页面)
      const  subscribe = (listener) => listeners.push(listener)
      const getState = () => state
      const dispatch = (action) => {
          stateChanger(state, action)
          // 执行回调函数
          listeners.forEach((listener) => listener())
      }
      return { getState, dispatch, subscribe }
  }

  function stateChanger(state, action) {
      switch(action.type) {
          case 'UPDATE_TITLE_TEXT':
              state.title.text = action.text
              break
          case 'UPDATE_CONTENT_COLOR':
              state.content.color = action.color
              break
          default:
              break
      }
  }

  const store = createStore(appState, stateChanger)
  store.subscribe(() => renderApp(store.getState()))
  store.subscribe(() => console.log('I am callback 2'))

  renderApp(store.getState())
  store.dispatch({type: 'UPDATE_TITLE_TEXT', text: 'hello'})
  store.dispatch({type: 'UPDATE_CONTENT_COLOR', color: 'green'})
  ```

* 上述更新视图是一旦发现数据变化就重新渲染整个App，性能优化方案：
  在每个渲染函数执行渲染操作之前先做个判断，判断传入的新数据和旧的数据是不是相同，相同的话就不渲染了
  ```javascript
    ...
    // 防止oldAppState 没有传入，所以加了默认参数 oldAppState = {}
    function renderApp(newState, oldState = {}) {
        // 数据没变化则不处理
        if(newState === oldState) return
        console.log('render app...')
        renderTitle(newState.title, oldState.title)
        renderContent(newState.content, oldState.content)
    }

    function renderTitle(newTitle, oldTitle = {}) {
        if(newTitle === oldTitle) return
        const titleDOM = document.getElementById('title')
        titleDOM.innerHTML = newTitle.text
        titleDOM.style.color = newTitle.color
        console.log('renderTitle')
    }

    function renderContent(newContent, oldContent = {}) {
        if(newContent === oldContent) return
        const contentDOM = document.getElementById('content')
        contentDOM.innerHTML = newContent.text
        contentDOM.style.color = newContent.color
        console.log('renderContent')
    }

    ...
    const store = createStore(appState, stateChanger)
    let oldState = store.getState() // 缓存旧的state
    store.subscribe(() => {
        const newState = store.getState() // 数据可能发生变化，获取新的state
        console.log(newState === oldState) // => true
        renderApp(newState, oldState) // 新旧state传进去renderApp进行对比
        oldState = newState // 渲染完成后，新state变成旧state
    })
    renderApp(oldState)
    store.dispatch({type: 'UPDATE_TITLE_TEXT', text: 'hello'})
    store.dispatch({type: 'UPDATE_CONTENT_COLOR', color: 'green'})
  ```

  **由于新旧state都指向同一个对象**: `newState === oldState`是`true`，实际期望是指向不同的对象来进行对比

* 优化渲染性能，产生共享结构的对象(没有更新的状态不重新渲染)

  ```javascript
  function createStore(state, stateChanger) {
    const listeners = []
    const  subscribe = (listener) => listeners.push(listener)
    const getState = () => state
    const dispatch = (action) => {
        // stateChanger不会直接修改原来的对象，而是返回一个新的对象覆盖
        state = stateChanger(state, action)

        listeners.forEach((listener) => listener())
    }
    return { getState, dispatch, subscribe }
  }

  function stateChanger(state, action) {
      switch(action.type) {
          case 'UPDATE_TITLE_TEXT':
              // 构造新的对象并且返回
              return {
                  ...state,
                  title: {
                      ...state.title,
                      text: action.text
                  }
              }
          case 'UPDATE_CONTENT_COLOR':
              return {
                  ...state,
                  content: {
                      ...state.content,
                      color: action.color
                  }
              }
          default:
              // 没有修改，返回原来的对象
              return state
      }
  }

  const store = createStore(appState, stateChanger)
  let oldState = store.getState()
  store.subscribe(() => {
      const newState = store.getState()
      console.log(newState === oldState) // => false
      renderApp(newState, oldState)
      oldState = newState
  })
  renderApp(oldState)
  store.dispatch({type: 'UPDATE_TITLE_TEXT', text: 'hello'})
  store.dispatch({type: 'UPDATE_CONTENT_COLOR', color: 'green'})
  ```