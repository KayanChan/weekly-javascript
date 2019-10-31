## webpack的基本使用

### 安装
  ```bash
    npm install -D webpack webpack-cli
  ```

### 概念
  1. `path`： [path](http://www.runoob.com/nodejs/nodejs-path-module.html)是node.js中提供的处理文件路径的小工具
  2. `__dirname`: node.js中的一个全局变量，它指向当前执行脚本所在的目录
  3. `path.join(__dirname, path1, path2...)`: 路径片段连接
  4. `path.resolve(__dirname, path1, path2...)`: 把`/`当成根目录
  5. `process.env.NODE_ENV`: `process`是node的全局变量，拥有`env`属性，`NODE_ENV`需要通过设置`webpack mode`可得到；`mode`为`development`，则`process.env.NODE_ENV`为`development`，`mode`为`production`，则`process.env.NODE_ENV`为`production`;只设置`NODE_ENV`,不会自动设置`mode`
  6. `module.rules`的常用属性：
      * `test`: 可以匹配的正则文件
      * `include`: 要编译的目录
      * `exclude`：要排除编译的目录
  7. `loader`的加载顺序是由右往左
  8. `[name]-[hash/chunkhash/contenthash].[ext]`
      * `name`为模块名称
      * `hash`是每次修改任何一个文件，所有文件名的hash至都将改变
      * `chunkhash`是根据不同的入口文件(Entry)进行依赖文件解析、构建对应的chunk，生成对应的哈希值(同一个模块下的文件的hash值是一样的)
      * `contenthash`是针对文件内容级别的，自身模块内容变了，hash才会变
      * hash值默认为20位，`[hash:16]`来指定16位
      * `ext`：文件后缀名

### 可参考文档
  1. [webpack的简单介绍](https://juejin.im/post/5c5150fc518825261f738443)
  2. [Webpack 开发环境配置](https://juejin.im/post/5c51520cf265da61180215e5)
  3. [Webpack 生产环境配置](https://juejin.im/post/5c5407296fb9a049bb7cc4ee)
  4. [从零开始搭建一个 React + Mobx + React Router 脚手架](https://juejin.im/post/5caee4266fb9a0688144ec68)