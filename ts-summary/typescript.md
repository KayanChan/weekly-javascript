# TypeScript
@出自[参考文档](https://ts.xcatliu.com/)

## 关于TS
JS的一个超集，可以编译成纯JS，运行在任何浏览器上

主要提供类型系统和对ES6的支持，由微软Microsoft开发，开源项目

TS编译工具可以运行在任何服务器和任何系统上

## TS的优缺点
### 优点
#### 增加了代码的可读性和可维护性
* 类型系统
* 编译阶段发现大部分错误
* 增强了编辑器和`IDE`的功能

#### 包容性
* `.js`文件可以直接重命名为`.ts`即可
* 不显式的类型会自动做出类型推论
* 可以定义从简单到复杂的几乎一切类型
* 编译报错也会生成JS文件
* 兼容第三方库，即使不是用TS编写的

#### 用于活跃的社区
* 大部分第三方库都有提供给TS的类型定义文件
* 拥抱了`ES6`规范，也支持部分`ESNext`草案的规范

### 缺点
* 学习成本，需要理解接口、泛型、类、枚举类型等概念
* 短期可能增加开发成本换取较低的维护成本
* 集成到构建流程需要一些工作量
* 可能和一些库结合的不是很完美

## 安装TS
全局环境安装tsc命令 `npm install typescript -g`

编译一个ts文件 `tsc hello.ts`

约定使用`TypeScript`编写的文件以`.ts`为后缀，用`TypeScript`编写`React`时，以`.tsx`为后缀


* [下一节：Hello TypeScript](https://github.com/KayanChan/weekly-javascript/blob/master/ts-summary/hello-ts.md)
* [原始数据类型](https://github.com/KayanChan/weekly-javascript/blob/master/ts-summary/primitive-data-types.md)
* [任意值](https://github.com/KayanChan/weekly-javascript/blob/master/ts-summary/any.md)
* [类型推论](https://github.com/KayanChan/weekly-javascript/blob/master/ts-summary/type-inference.md)
* [联合类型](https://github.com/KayanChan/weekly-javascript/blob/master/ts-summary/union-types.md)
* [接口](https://github.com/KayanChan/weekly-javascript/blob/master/ts-summary/interfaces.md)
* [数组的类型](https://github.com/KayanChan/weekly-javascript/blob/master/ts-summary/array.md)
* [函数的类型](https://github.com/KayanChan/weekly-javascript/blob/master/ts-summary/function.md)
* [类型断言](https://github.com/KayanChan/weekly-javascript/blob/master/ts-summary/type-assertion.md)
* [声明文件](https://github.com/KayanChan/weekly-javascript/blob/master/ts-summary/declaration-files.md)
* [内置对象](https://github.com/KayanChan/weekly-javascript/blob/master/ts-summary/built-in-objects.md)
* [类型别名](https://github.com/KayanChan/weekly-javascript/blob/master/ts-summary/type-aliases.md)
* [字符串字面量类型](https://github.com/KayanChan/weekly-javascript/blob/master/ts-summary/string-literal-types.md)
* [元祖](https://github.com/KayanChan/weekly-javascript/blob/master/ts-summary/tuple.md)
* [枚举](https://github.com/KayanChan/weekly-javascript/blob/master/ts-summary/enum.md)
* [类](https://github.com/KayanChan/weekly-javascript/blob/master/ts-summary/class.md)
