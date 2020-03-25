# 内置对象

内置对象是指根据标准在全局作用域（Global）上存在的对象

## ECMAScript内置对象
ECMAScript 标准提供的内置对象有：Boolean、Error、Date、RegExp 等

```TypeScript
let b: Boolean = new Boolean(1);

let e: Error = new Error('Error occurred');

let d: Date = new Date();

let r: RegExp = /[a-z]/;
```

## DOM & BOM的内置对象

DOM 和 BOM 提供的内置对象有：Document、HTMLElement、Event、NodeList 等

```TypeScript
let body: HTMLElement = document.body;

let allDiv: NoteList = document.querySelectorAll('div')

document.addEventListener('click', function(e: MouseEvent) {
    // do something
})
```

## TypeScript 核心库的定义文件

TypeScript 核心库的定义文件定义了所有浏览器环境需要用到的类型，并且是预置在 TypeScript 中的，但TypeScript 核心库的定义中不包含 Node.js 部分

## 用 TypeScript 写 Node.js

Node.js 不是内置对象的一部分，如果想用 TypeScript 写 Node.js，则需要引入第三方声明文件

`npm install @types/node --save-dev`

* [下一节：类型别名](https://github.com/KayanChan/weekly-javascript/blob/master/ts-summary/type-aliases.md)