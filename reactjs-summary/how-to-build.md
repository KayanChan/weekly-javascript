### How to build a react-app

1. 新建项目`react-study`
    ```bash
    create-react-app react-study
    ```
2. 配置使用装饰器
    * 暴露项目的配置项(保证git commit)
        ```bash
        npm run eject
        ```
    * 安装`babel`插件
        ```bash
        yarn add @babel/plugin-proposal-decorators @babel/plugin-transform-react-jsx @babel/plugin-transform-react-jsx-self @babel/plugin-transform-react-jsx-source --dev
        ```
    * 修改`package.json`文件的`babel`配置项
        ```json
        "babel": {
            "plugins": [
                ["@babel/plugin-proposal-decorators", { "legacy": true }]
            ],
            "presets": [
                "react-app"
            ]
        }
        ```
3. 配置`webpack`，使用`@`来`import`模块
    ```json
    // webpack.config.js
    alias: {
        '@': path.resolve(__dirname, '../src'),
        ...
    }
    ```
4. CSS Reset
    > `src/index.css`: 标签重置
    > `src/App.css`: 自定义样式、覆盖antd样式
5. React路由
    * 安装`react-router-dom`
        ```bash
        yarn add react-router-dom
        ```
    * router/config.js: 路由配置表
    * router/index.js：路由处理
    * 路由重定向(404，默认路由)、路由渲染、菜单高亮展开
    * `React(Suspense/Lazy)`实现路由懒加载
    * `react-transition-group`实现路由跳转过渡动画 [文档](https://reactcommunity.org/react-transition-group/)
6. UI组件库：ant-design
    * 安装
        ```bash
        yarn add antd
        ```
    * 按需加载，只需从`antd`引入模块,不用单独引入样式
        ```bash
        yarn add babel-plugin-import
        ```
        package.json添加配置
        ```json
        "babel": {
            "plugins": [
                [
                    "import",
                    {
                    "libraryName": "antd",
                    "libraryDirectory": "es",
                    "style": "css"
                    }
                ]
            ]
        }
        ```
7. CSS-in-JS
    * 安装`jss`
        ```bash
        yarn add react-jss
        ```
    * 公共部分提取到文件夹`styles/`下，组件内部通过`object spread`操作符或者`Object.assign`获取
        ```javascript
        subRoutes: {
            ...style.ul,
            paddingLeft: 10
        }
        ```
    * 组件内部通过`injectSheet`来绑定
        ```javascript
        import injectSheet from 'react-jss';
        import styles from './style';

        @injectSheet(styles)
        class Mainbox extends Component {
        render() {
            const { classes } = this.props;
            return <div className={classes.mainContainer}>
            <Router />
            </div>
        }
        }
        ```

