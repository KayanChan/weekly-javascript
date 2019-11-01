### React路由

#### `react-router` 和 `react-router-dom`
  * react-router: 实现了路由的核心功能
  * react-router-dom: 基于`react-router`，加入了在浏览器运行环境下的一些功能(`Link`组件、`BrowserRouter`、`HashRouter`等)
  * react-router-native: 基于`react-router`, 加入了`react-native`运行环境下的一些功能

#### [react-router-dom](https://react-router.docschina.org/web/guides/quick-start)

#### 知识点
  1. `exact`：路径信息需要完全匹配，不可匹配一部分
  2. ReactRouter动态传值
      ```javascript
      componentDidMount() {
        // 接收传递值
        console.log(this.props.match); // {patch: '', url: '', params: {}}
      }
      ```
      ```jsx
      <li><Link to="/list/123">列表</Link> </li>
      <Route path="/list/:id" component={List} />
      ```

      * `patch`: 定义的路由规则
      * `url`: 真实的访问路径
      * `params`: 传递过来的参数
      * 设置了动态传值，但是不传参数时会导致无法匹配
  3. 重定向
    * 标签重定向`<Redirect to="/home/" />`
    * 编程式重定向` this.props.history.push("/home/"); `(在`constructor`里处理则跟上面标签重定向效果一样))