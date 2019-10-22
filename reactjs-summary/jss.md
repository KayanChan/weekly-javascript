### JSS
  ##### [JSS](https://github.com/cssinjs/react-jss)是什么
  > CSS的抽象，使用JavaScript以声明和可维护的方式描述样式
  > 高性能的JS to CSS编译器，大约6KB（缩小和gzip压缩）

  ##### 优点
  1. 组件化，CSS模型抽象到组件级别，非文档级别
  2. 利用js生态系统来增强CSS
  3. 规则隔离，JSS规则不会继承属性
  4. 范围选择器，JSS将JSON表示编译为CSS时，JSS默认生成唯一的类名
  5. 自动添加前缀
  6. 代码共享，JS和CSS之间共享常量和函数
  7. CSS单元测试

  ##### 基础使用
  ```javascript
    import React from 'react'
    import {createUseStyles} from 'react-jss'

    const useStyles = createUseStyles({
      buttonA: {
        backgroundColor: '#f5f5f5',
        color: 'black',
        margin: {
          top: 5,
          bottom: 5,
          left: '1em',
          right: '1em'
        },
        border: '1px solid #999',
        '& span': {
          fontWeight: 'bold'
        }
      },
      label: {
        color: '#888',
        padding: 5,
        '&:hover': {
          border: '1px solid #999'
        }
      }
    })


    const BasicButton = ({children}) => {
      const classes = useStyles()
      return (
        <div>
          <label className={classes.label}>操作</label>
          <button className={classes.buttonA}>
            <span >{children}</span>
          </button>
        </div>   
      )
    }


    export default BasicButton
  ```

  ##### 动态值
```javascript
  import React from 'react';
  import {createUseStyles} from 'react-jss';

  const useStyles = createUseStyles({
    myButton: {
      padding: props => props.spacing
    },
    myLabel: props => ({
      display: 'block',
      color: props.labelColor,
      fontWeight: props.fontWeight,
      fontStyle: props.fontStyle
    })
  })

  const DynamicValue = ({children, ...props}) => {
    const classes = useStyles(props)
    return (
      <button className={classes.myButton}>
        <span className={classes.myLabel}>{children}</span>
      </button>
    )
  }

  DynamicValue.defaultProps = {
    spacing: 10,
    fontWeight: 'bold',
    labelColor: 'red'
  }

  export default DynamicValue
```

  ##### JSS的主题化: ThemeProvider
  1. 定义一个主题对象，用`ThemeProvider`包装应用程序，传递给`ThemeProvider`

```javascript
<ThemeProvider theme={theme}>
    <Theming>I am a button with green background</Theming>
</ThemeProvider>
```
  2. 接着在样式创建器函`createUseStyles ((theme) => { ... })`中使用`useTheme()`挂钩来访问主题

```javascript
// 当有很多主题依赖关系时，最好使用theme函数
let useStyles = createUseStyles(theme => ({
    button: {
      background: theme.colorPrimary
    },
    label: {
      fontWeight: 'bold'
    }
}))

// 只有很少的主题相关样式，则使用函数值可能会更好，并且props或state也用于其他值
let useStyles = createUseStyles({
    button: {
      background: theme => theme.colorPrimary
    },
    label: {
      fontWeight: 'bold'
    }
})
```
  3. 更改主题后，所有组件都将自动获得新主题

  ##### Decorators 配合React.Component([Decorators](https://github.com/KayanChan/weekly-javascript/blob/master/reactjs-summary/decorator.md))
```javascript
  import React from 'react';
  import injectSheet from 'react-jss';

  const styles = {
    button: {
      backgroundColor: 'yellow'
    },
    label: {
      fontWeight: 'bold'
    }
  }

  @injectSheet(styles)
  class Jss extends React.Component {
    render() {
      const {classes, children} = this.props;
      return (
        <div>
          <button className={classes.button}>
            <span className={classes.label}>{children}</span>
          </button>
        </div>
      )
    }
  }

  export default Jss;
```

  ##### 使用自定义主题上下文
  ##### 类名生成器选项
  ##### 服务端渲染