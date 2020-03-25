# 类型推论( Type Inference )
类型推论是指 TS 会在没有明确的指定类型的时候推出一个类型

如果没有指定类型，则使用任意值 any 这个类型，否则 TS 编译错误

```TypeScript
let myNumber = 'seven'
myNumber = 7

// 或者
let myNumber: string = 'seven'
myNumber = 7
```
> error TS2322: Type '7' is not assignable to type 'string'

如果定义的时候没有赋值，不管之后有没有赋值，都会被推断成 any 类型而完全不被类型检查

```TypeScript
let myNumber: any = 'seven'
myNumber = 7

// 或者
let myNumber
myNumber = 'seven'
myNumber = 7
```

* [下一节：联合类型](https://github.com/KayanChan/weekly-javascript/blob/master/ts-summary/union-types.md)