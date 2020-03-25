# 声明文件

## 声明语句
当使用第三方库时，我们需要引用它的声明文件，才能获得对应的代码补全、接口提示等功能

**声明语句中只能定义类型，切勿在声明语句中定义具体的实现**

jquery的使用

```TypeScript
declare var jQuery: (selector: string) => any

jQuery('#foo')
```

> declare var 并没有真的定义一个变量，只是定义了全局变量 jQuery 的类型，仅仅会用于编译时的检查，在编译结果中会被删除

## 全局变量模式声明文件
通常会把声明语句放到一个单独的文件（jQuery.d.ts）中

**声明文件必需以 .d.ts 为后缀**

`*.d.ts`文件仅仅会用于编译时的检查，声明文件里的内容在编译结果中会被删除

```TypeScript
// jQuery.d.ts

declare var jQuery: (selector: string) => any
```

## 第三方声明文件
社区已经定好 jQuery 的声明文件，可以直接下载使用，更推荐是使用 @types 统一管理第三方库的声明文件

@types 的使用方式很简单，直接用 npm 安装对应的声明模块即可，可以通过[搜索](https://microsoft.github.io/TypeSearch/)出需要的声明文件

```C
npm install @types/jquery --save-dev
```

## 书写声明文件
库的使用场景主要有以下几种

1. 全局变量 - 通过 <script> 标签引入第三方库，注入全局变量

2. npm包 - 通过 import foo from 'foo' 导入，符合 ES6 模块规范

3. UMD库 - 既可以通过 <script> 标签引入，又可以通过 import 导入

4. 直接扩展全局变量 - 通过 <script> 标签引入后，改变一个全局变量的结构

5. 在 npm 包或 UMD 库中扩展全局变量 - 引用 npm 包或 UMD 库后，改变一个全局变量的结构

6. 模块插件 - 通过 <script> 或 import 导入后，改变另一个模块的结构

## 全局变量

### declare var / declare let

定义一个全局变量的类型

```TypeScript
declare var jQuery: (selector: string) => any

declare let jQuery: (selector: string) => any
```

### declare const

定义一个全局变量的类型，且此全局变量为一个常量，不允许再去修改其值

一般来说，全局变量都是禁止修改的常量，所以**大部分情况全局变量都应该使用 const 而不是 var 或 let**

```TypeScript
declare const jQuery: (selector: string) => any
```

### declare function

定义全局函数的类型

```TypeScript
declare function jQuery(selector: string): any
```
> jQuery 其实就是一个函数，所以也可以用function来定义

在函数类型的声明语句中，支持函数重载

```TypeScript
// jQuery.d.ts
declare function jQuery(selector: string): any
declare function jQuery(domReadyCallback: () => any): any

// index.ts
jQuery('#foo')
jQuery(function() {
    alert('Dom Ready')
})
```

### declare class

定义一个类的全局变量

```TypeScript
// *.d.ts
declare class Person {
    name: string;
    constructor(name: string);
    sayHi(): string
}
```

declare class 语句也只能用来定义类型，不能用来定义具体的实现

### declare enum

使用 declare enum 定义的枚举类型也称作外部枚举（Ambient Enums）

Directions 是由第三方库定义好的全局变量

```TypeScript
// *.d.ts
declare enum Directions {
    Up,
    Down,
    Left,
    Right
}

let directions = [Directions.Up, Directions.Down, Directions.Left, Directions.Right]
```

### declare namespace
namespace 是 ts 早期时为了解决模块化而创造的关键字，中文称为命名空间

ES6 使用了 module 关键字，ts 为了兼容 ES6，使用 namespace 替代了自己的 module，更名为命名空间

随着 ES6 的广泛应用，现在已经不建议再使用 ts 中的 namespace，而推荐使用 ES6 的模块化方案了

### interface & type

在类型声明文件`*.d.ts`中，我们可以直接使用 interface 或 type 来声明一个全局的接口或类型

```TypeScript
// *.d.ts
interface AjaxSettings {
    method?: 'GET' | 'POST';
    data?: any
}

// *.ts
let settings: AjaxSettings = {
    method: 'POST',
    data: {
        name: 'foo'
    }
}
```

暴露在最外层的 interface 或 type 会作为全局类型作用于整个项目中

尽可能的减少全局变量或全局类型的数量，故最好放到 namespace 下

```TypeScript
// *.d.ts

declare namespace jQuery {
    interface AjaxSettings {
        method?: 'GET' | 'POST'
        data?: any;
    }
    function ajax(url: string, settings?: AjaxSettings): void;
}
```

### 声明合并
 jQuery 既是一个函数，可以直接被调用 jQuery('#foo')，又是一个对象，拥有子属性 jQuery.ajax()，那么可以组合声明
```TypeScript
declare function jQuery(selector: string): any;
declare namespace jQuery {
    function ajax(url: string, settings?: any): void;
}
```

### npm
npm 包声明文件存在的两个地方：
1. 与该 npm 包绑定在一起
    package.json 有 types 字段，或者有一个 index.d.ts 声明文件

    不需要额外安装其他包，最为推荐

2. 发布到 @types 里
    尝试安装一下对应的 @types 包来检查是否存在声明文件 `npm install @types/foo --save-dev`

    一般是由于 npm 包的维护者没有提供声明文件，所以其他人发布到@types里面

以上两种方式都没有找到声明文件，则自行创建对应的声明文件，有两种方案可以通过 import 语句导入的模块：
1. 创建一个 node_modules/@types/foo/index.d.ts 文件，存放 foo 模块的声明文件

    不需要额外配置，但 node_modules 目录不稳定，代码也没有被保存到仓库中，无法回溯版本，存在被删的风险

    一般只作测试用

2. 创建一个 types 目录，专门用来管理自己写的声明文件，将 foo 的声明文件放到 types/foo/index.d.ts 中

    需要配置下 tsconfig.json 中的 paths 和 baseUrl 字段

    ```json
    {
        "compilerOptions": {
            "module": "commonjs",
            "baseUrl": "./",
            "paths": {
                "*": ["types/*"]
            }
        }
    }
    ```

npm 包声明文件的主要语法：
- export: 导出变量
- export namespace: 导出(含子属性的)对象
- export default: ES6默认导出
- export =: commonjs导出模块

### export
```TypeScript
export const name: string;

export function getName(): string;

export class Animal {
    constructor(name: string);
    sayHi(): string;
}

export enum Directions {
    Up,
    Down,
    Left,
    Right
}

export interface Options {
    data: any
}
```

在 npm 包的声明文件中，使用 declare 不再会声明一个全局变量，而只会在当前文件中声明一个局部变量

只有在声明文件中使用 export 导出，然后在使用方 import 导入后，才会应用到这些类型声明

**与全局变量的声明文件类似，interface 前是不需要 declare 的**

```TypeScript
declare const name: string;

declare function  getName(): string;

declare class Animal {
    constructor(name: string);
    sayHi(): string;
}

declare enum Directions {
    Up,
    Down,
    Left,
    Right
}

interface Options {
    data: any
}

export {name, getName, Animal, Directions, Options}
```

### export namespace
```TypeScript
export namespace foo {
    const name2: string;
    function getName2 (): string;
    class Animal2 {
        constructor(name2: string);
        sayHi2(): string;
    }
    enum Directions2 {
        Up,
        Down,
        Left,
        Right
    }
}
```

### export default
在 ES6 模块系统中，使用 export default 可以导出一个默认值，使用方可以用 import foo from 'foo' 而不是 import { foo } from 'foo' 来导入这个默认值

**只有 function、class 和 interface 可以直接默认导出，其他的变量需要先定义出来，再默认导出**

```TypeScript
export default function foo(): string;
export default class AnimalFoo {
    constructor(name: string);
    getAnimal(): string
}
export default enum Directions3 {
    Up,
    Down,
    Left,
    Right
}

// 普通类型
export default name3;
declare const name3: string;

// 枚举
export default Directions;
declare enum Directions {
    Up,
    Down,
    Left,
    Right
}
```

**默认导出语句放在整个声明文件的最前面**

### export =

在 commonjs 规范中，导出整个 module.exports = foo，导出单个 exports.bar = bar

TS 有多种方式可以整体导出/单个导入：
1. const ... = require
```TypeScript
const foo = require('foo')

const bar = require('foo').bar
```

2. import ... from
```TypeScript
import * from 'foo'

import { bar } from 'bar'
```

3. import ... require，**官方推荐**
```TypeScript
import foo = require('foo')

import bar  = foo.bar
```

## UMD库
既可以通过 <script> 标签引入，又可以通过 import 导入的库，称为 UMD 库

### export as namespace
先有了 npm 包的声明文件，再基于它添加一条 export as namespace 语句，即可将声明好的一个变量声明为全局变量

```TypeScript
// types/foo/index.d.ts

export as namespace foo;
export default foo;

declare function foo(): string;
declare namespace foo {
    const bar: number;
}
```

## 直接扩展全局变量
```TypeScript
declare namespace JQuery {
    interface CustomOptions {
        bar: string;
    }
}

interface JQueryStatic {
    foo(options: JQuery.CustomOptions): string;
}
```

## 在 npm 包或 UMD 库中扩展全局变量
对于一个 npm 包或者 UMD 库的声明文件，只有 export 导出的类型声明才能被导入

导入此库之后会扩展全局变量，则需要通过 declare global 在声明文件中扩展全局变量的类型

### declare globar
```TypeScript
// types/foo/index.d.ts

declare global {
    interface String {
        prependHello(): string;
    }
}

export {};
```

> 导出一个空对象，用来告诉编译器这是一个模块的声明文件，而不是一个全局变量的声明文件

##  模块插件
ts 提供了一个语法 declare module，它可以用来扩展原有模块的类型，使得没有类型声明文件的插件模块补充上类型声明

**需要扩展原有模块，在类型声明文件中先引用原有模块**

declare module 在一个文件中一次性声明多个模块的类型

```TypeScript
import * as moment from 'moment';

declare module 'moment' {
    export function foo(): moment.CalendarKey;
}

declare module 'foo' {
    export interface Foo {
        foo: string;
    }
}
```

## 声明文件中的依赖
一个声明文件有时会依赖另一个声明文件中的类型

可以在声明文件中通过 import 导入另一个声明文件中的类型
```TypeScript
import * as moment from 'moment';
```

也可以通过三斜线指令来导入另一个声明文件

三斜线指令也是 ts 在早期版本中为了描述模块之间的依赖关系而创造的语法。随着 ES6 的广泛应用，现在已经不建议再使用 ts 中的三斜线指令来声明模块之间的依赖关系

三斜线指令的语法：`///`后面使用 xml 的格式

三斜线指令必须放在文件的最顶端，三斜线指令的前面只允许出现单行或多行注释

当且仅当在以下几个场景下，我们才需要使用三斜线指令替代 import:
- 当我们在书写一个全局变量的声明文件时
- 当我们需要依赖一个全局变量的声明文件时

### 书写一个全局变量的声明文件
```
// 添加了对 jquery 类型的依赖
/// <reference types="jquery" />

declare function foo(options: JQuery.AjaxSettings): string;
```

### 依赖一个全局变量的声明文件
```
// 引入了 node 的类型，然后在声明文件中使用了 NodeJS.Process
/// <reference types="node" />

export function foo(p: NodeJS.Process): string;
```

### 拆分声明文件
当全局变量的声明文件太大时，可以通过拆分为多个文件，然后在一个入口文件中将它们一一引入，来提高代码的可维护性

types 用于声明对另一个库的依赖，而 path 用于声明对另一个文件的依赖

```TypeScript
// node_modules/@types/jquery/index.d.ts

/// <reference types="sizzle" />
/// <reference path="JQueryStatic.d.ts" />
/// <reference path="JQuery.d.ts" />
/// <reference path="misc.d.ts" />
/// <reference path="legacy.d.ts" />

export = jQuery;
```

## 自动生成声明文件
库的源码本身就是由 ts 写的，那么在使用 tsc 脚本将 ts 编译为 js 的时候，添加 declaration 选项，就可以同时也生成 .d.ts 声明文件

方式一：在命令行中添加 --declaration（简写 -d）

方式二：添加和配置 declaration 选项()
```TypeScript
// tsconfig.json
{
    "compilerOptions": {
        "module": "commonjs",
        "outDir": "lib",
        "declaration": true,
    }
}
```

* [下一节：内置对象](https://github.com/KayanChan/weekly-javascript/blob/master/ts-summary/built-in-objects.md)