### React Decorator 装饰器
  #### 装饰器Decorator
  > 装饰/修饰器（Decorator）是一个函数，用来修改类的行为

  #### 配置使用装饰器
  1. 暴露由`create-react-app`创建的项目的配置项

     create-react-app`默认不支持装饰器,需要暴露当初创建的配置项

     	* 首先保证本地没有待提交git的代码
     	* `package.json`可以看到`eject`, 运行`npm run eject`	
     	* 完成后本地目录增加`config`

  2. 安装`babel`插件

```bash
// babel >= 7.x
yarn add @babel/plugin-proposal-decorators --dev
yarn add @babel/plugin-transform-react-jsx --dev
yarn add @babel/plugin-transform-react-jsx-self --dev
yarn add @babel/plugin-transform-react-jsx-source --dev
```
  3. 修改`package.json`文件的`babel`配置项

```json
// babel >= 7.x
"babel": {
  "plugins": [
    ["@babel/plugin-proposal-decorators", { "legacy": true }]
  ],
  "presets": [
    "react-app"
  ]
}
```
  4. 使`VS Code`支持装饰器语法`文件-首选项-设置-搜索setting.json`

```json
"javascript.implicitProjectConfig.experimentalDecorators": true
```

  #### 应用

##### 为类添加一个静态属性

```javascript
import React, {Component} from 'react';

// 定义一个函数，也就是Decorator
function testable(target) {
	target.isTestable = true;
}

// Decorator后面是Class，默认就已经把Class当成参数隐形传进Decorator了(理解像testable(AddStatic))

@testable
class AddStatic extends Component {
    render() {
    	return (<div>为类添加了一个静态属性</div>)
	}
}

console.log(AddStatic.isTestable)

export default AddStatic
```

##### 多个类使用一个Decorator

```javascript
import React, {Component} from 'react';

  // 在外层套一个函数,返回Decorator
  function testable(isTestable) {
    return function(target) {
      target.isTestable = isTestable;
    }
  }

  // 隐形传入了Class，语法类似于testable(true)(MyTestableClass)
  @testable(true)
  class MultClassA extends Component {
    render() {
      return (<div>1.多个类使用Decorator</div>)
    }
  }

  @testable(false)
  class MultClassB extends Component {
    render() {
      return (<div>2.多个类使用Decorator</div>)
    }
  }

  console.log(MultClassA.isTestable, MultClassB.isTestable);

  export {
    MultClassA,
    MultClassB
  }
```

##### 修改类的prototype对象

```javascript
import React, {Component} from 'react';

// 修改类的prototype对象
function testable(target) {
	target.prototype.isTestable = true;
}

@testable
class ModifyPrototype extends Component {
    render() {
    	return (<div>修改类的prototype对象</div>)
    }
}

let obj = new ModifyPrototype();
console.log(obj.isTestable)

export default ModifyPrototype
```

##### 将Math的add方法修改为打印函数，输入传入参数

```javascript
function log(target, name, descriptor) {
// target为目标对象，对应类实例 --> MathDemo实例
// name要修饰的属性名 --> add
// descriptor属性的描述对象 --> {writable: true, enumerable: false, value: f, configurable: true}
    var oldValue = descriptor.value;

    // 改了add方法，使其作用变成一个打印函数
    descriptor.value = function() {
        console.log(target);
        console.log(name);
        console.log(descriptor);
        console.log(`Calling "${name}" with`, arguments);
        return oldValue.apply(null, arguments);
    }

    return descriptor;
}

class Math {
    @log
    add(a, b) {
        return a+b;
	}
}

const math = new Math();
math.add(2, 4);
// Calling "add" with Argument[2, 4]
```

##### react的应用

  > 需求：
  > 有这么一个页面组件，用于显示用户资料的，当从Home组件进去到这个组件时
  > 希望title从“Home Page”变成“Profile Page”

```javascript
  import React from 'react';

  const setTitle = (title) => (WrapperComponent) =>{
    return class extends React.Component {
      componentDidMount() {
        document.title = title;
      }
      render() {
        return <WrapperComponent {...this.props} />
      }
    }
  }

  @setTitle('Profile Page')
  class Profile extends React.Component {
    render() {
      return (
        <div>修改页面的title</div>
      )
    }
  }

  export default Profile;
```

  ##### [JSS + React.Component](https://github.com/KayanChan/weekly-javascript/blob/master/reactjs-summary/jss.md)