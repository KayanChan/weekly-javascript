# 数组的类型

## 「类型 + 方括号」表示法

数组的项中不允许出现其他的类型

```TypeScript
let arrayA: number[] = [1, 2, 3]

arrayA.push(4)
arrayA.push('5')
```
> error TS2345: Argument of type '"5"' is not assignable to parameter of type 'number'

## 数组泛型（Array Generic） Array<elemType> 来表示数组

```TypeScript
let arrayB: Array<number> = [1, 2, 3]
```

## 用接口表示数组
只要索引的类型是数字时，那么值的类型必须是数字

普通数组用接口表示法较复杂，不推荐使用；但是常用接口表示法来表示类数组

```TypeScript
interface NumberArray {
    [index:number]: number
}

let arrayC: NumberArray = [1, 2, 3]
```

## 类数组
类数组( Array-like Object )不是数组类型，比如 arguments

```TypeScript
function sum() {
    let args: {
        [index: number]: number;
        length: number;
        callee: Function;
    } = arguments;
}
```

**事实上常用的类数组都有自己的接口定义(内置对象)，如 IArguments, NodeList, HTMLCollection 等**

```TypeScript
function sum2() {
    let args: IArguments = arguments;
}
```

## any在数组中的应用
```TypeScript
let arrayD: any = [true, 1, 'caicai', {a: 'b'}]
```

* [下一节：函数的类型](https://github.com/KayanChan/weekly-javascript/blob/master/ts-summary/function.md)