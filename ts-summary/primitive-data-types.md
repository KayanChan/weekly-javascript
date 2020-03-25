# 原始数据类型( Primitive data types )

## JavaScript数据类型
JavaScript 数据类型分为两种：原始数据类型( Primitive data types ) 和 对象类型( Object types )

原始数据类型: 布尔值、数值、字符串、null、undefined 以及 ES6的新类型symbol

## 布尔值
在 TypeScript 中， boolean 是 JavaScript 中的基本类型，而 Boolean 是 JavaScript 中的构造函数，其他基本类型（除了 null 和 undefined ）一样

```TypeScript
let isDone: boolean = false
let isFinished: boolean = Boolean(1)

let BooleanObject: Boolean = new Boolean(1)

console.log(typeof isDone) // boolean
console.log(typeof isFinished) // boolean
console.log(typeof BooleanObject) // object
```

## 数值
ES6中的二进制和八进制表示法，会被编译成十进制
```TypeScript
// 十进制
let decLiteral: number = 6
// 十六进制
let hexLiteral: number = 0xf00d
// 二进制
let binaryLiteral: number = 0b1010
// 八进制
let octalLiteral: number = 0o744
// Number.NaN 是一个特殊值，说明某些算术运算（如求负数的平方根）的结果不是数字
let notANumber: number = NaN
// 表示正无穷大的数值
let infinityNumber: number = Infinity


console.log(decLiteral, hexLiteral, binaryLiteral, octalLiteral, notANumber, infinityNumber)
// 6, 0xf00d, 10, 484, NaN, Infinity
```

## 字符串
ES6的模板字符串和模板字符串中嵌入表达式`${expr}`
```TypeScript
let name = 'Sally'
let age = 25
let sentence = `Hello, my name is ${name}, I am ${age} years old`
```
> 报错 error TS2451: Cannot redeclare block-scoped variable 'name'
在默认状态下，TS将DOM typings作为全局的运行环境，与DOM中的全局window对象下的name重名

解决方法一，配置 tsconfig.json ，更改运行环境
```json
{
    "compilerOptions": {
        "lib": [
            "es2015"
        ]
    }
}
```

解决方法二，在TS中，只要文件存在 import 或 export 关键字，都被视为 module ；在脚本的最后一行，添加了`export {};`

## Null & Undefined
undefined 和 null 是所有类型的子类型，即可以赋值给其他类型的变量

```TypeScript
let u: undefined = undefined // 未定义
let n: null = null // 空对象指针
let numberA: undefined // var numberA;
let numberB: number = u // var numberB = u;
```
## void 空值
JS没有 void 空值的概念，但TS中，可以用 void 表示**没有任何返回值**的函数

```TypeScript
function alertHelloWorld(): void {
    alert('Hello World')
}
```

void 类型的变量，只能赋值 null 和 undefined；但不能像 null 和 undefined一样赋值给其他类型的变量
```TypeScript
let voidNull: void = null
let voidUndefined: void = undefined
```

* [下一节：任意值](https://github.com/KayanChan/weekly-javascript/blob/master/ts-summary/any.md)