# 函数的类型

函数是 JS 中的一等公民
> 实际说的是函数跟其他对象都一样(普通公民)，没有什么特殊

在 JavaScript 中，有两种常见的定义函数的方式——函数声明（Function Declaration）和函数表达式（Function Expression）

## 函数声明
```TypeScript
function sum(x: number, y: number): number {
    return x+y
}

sum(1, 2)
sum(1) // 报错
sum(1, 2, 3) // 报错
```
> error TS2554: Expected 2 arguments, but got 1
> error TS2554: Expected 2 arguments, but got 3

**输入多余的（或者少于要求的）参数，是不被允许的**

## 函数表达式
### 过赋值操作进行类型推论而推断出来
```TypeScript
let sum2 = function (x: number, y: number): number {
    return x+y
}
sum2(1, 2)
```

### 手动添加类型
```TypeScript
let sum3: (x: number, y: number) => number = function (x: number, y: number): number {
    return x+y
}
```
在 TypeScript 的类型定义中，=> 用来表示函数的定义，左边是输入类型，需要用括号括起来，右边是输出类型。

在 ES6 中，=> 叫做箭头函数

## 用接口定义函数的形状
```TypeScript
interface SearchFunc {
    (source: string, subString: string): boolean
}

let mySearch: SearchFunc;
mySearch = function (source: string, subString: string) {
    return source.search(subString) !== -1
}
```

## 可选参数
用 ? 表示可选的参数，可选参数必须接在必需参数后面

**可选参数后面不允许再出现必需参数了**

```TypeScript
function sum4(x: number, y: number, z?: number) {
    return z ? (x+y+z) : (x+y)
}

sum4(1, 2, 3)
sum4(2, 3)
```

## 参数默认值
TypeScript 会将添加了默认值的参数识别为可选参数

```TypeScript
function buildName(firstName, lastName) {
    if (lastName === void 0) { lastName = 'Chan'; }
    return firstName + " " + lastName;
}
buildName('Tom');
buildName('Sally', 'Han');
```

## 剩余参数
ES6 中，可以使用 ...rest 的方式获取函数中的剩余参数（rest 参数）

rest 参数只能是最后一个参数

```TypeScript
function pushArray(array: any[], ...otherItems: any[]) {
    otherItems.forEach(function(item) {
        array.push(item)
    })
}

let a = []
pushArray(a, 1, 2, 3)
```

## 重载
重载允许一个函数接受不同数量或类型的参数时，作出不同的处理

使用重载定义多个 reverse 的函数类型

```TypeScript
function reverse(x: number): number;
function reverse(y: string): string;
function reverse(x: number | string): number | string {
    if (typeof x === 'number') {
        return Number(x.toString().split('').reverse().join(''));
    } else if (typeof x === 'string') {
        return x.split('').reverse().join('');
    }
}

reverse(123)
reverse('hello')
```

TypeScript 会优先从最前面的函数定义开始匹配，所以多个函数定义如果有包含关系，需要优先把精确的定义写在前面

* [下一节：类型断言](https://github.com/KayanChan/weekly-javascript/blob/master/ts-summary/type-assertion.md)