# 对象的类型 - 接口( Interfaces )

在 TypeScript 中，我们使用接口（Interfaces）来定义对象的类型。

在面向对象语言中，接口（Interfaces）是一个很重要的概念，它是对行为的抽象，而具体如何行动需要由类（classes）去实现（implement）。

TypeScript的接口除了可用于对类的一部分行为进行抽血以外，也常用于对对象的形状进行描述

```TypeScript
interface Person {
    name: string;
    age: number;
}

let child: Person = {
    name: 'Tom',
    age: 25
}
```
> 定义了一个接口Person, 定义一个变量child, 它的类型是Person

接口首字符大写`Person`；赋值的时候，变量的形状必须和接口的形状保持一致(定义的变量的属性需要跟接口一样，需要有`name`和`age`)

也可以通过可选属性(即可以不存在)，不完全匹配接口的形状

但也不允许出现接口没添加的属性

```TypeScript
interface Person {
    name: string;
    age: number;
    hobby?: string;
}

let child: Person = {
    name: 'Tom',
    age: 25,
    sex: 'male' // 报错
}
```
> error TS2322: Type '{ name: string; age: number; sex: string; }' is not assignable to type 'Person'

或者让接口允许有任意的属性，但定义了任意属性，那么确定属性和可选属性的类型都必须是它的类型的子集

```TypeScript
interface Person {
    name: string;
    age: number;
    hobby?: string;
    [propName: string]: string;
}

let child: Person = {
    name: 'Tom',
    age: '25',
    sex: 'male'
}
```

> age如果是number的话，会报错，因为number不是任意属性的类型string的子集

用 readonly 定义只读属性，令字段只能在创建的时候被赋值

**只读的约束存在于第一次给对象赋值的时候，而不是第一次给只读属性赋值的时候**

```TypeScript
interface Person {
    readonly id: number;
    name: string;
    age: string;
    hobby?: string;
    [propName: string]: any;
}

let child: Person = {
    id: 1,
    name: 'Tom',
    age: '25',
    sex: 'male'
}

child.id = 2
```

>  error TS2540: Cannot assign to 'id' because it is a read-only property

* [下一节：数组的类型](https://github.com/KayanChan/weekly-javascript/blob/master/ts-summary/array.md)