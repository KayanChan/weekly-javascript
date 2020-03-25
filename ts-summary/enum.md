# 枚举

枚举（Enum）类型用于取值被限定在一定范围内的场景，比如一周只能有七天，颜色限定为红绿蓝等

枚举成员会被赋值为从 0 开始递增的数字，同时也会对枚举值到枚举名进行反向映射

```TypeScript
enum Days { Sun, Mon, Tue, Wed, Thu, Fri, Sat }

console.log(Days['Sun'] === 0)

console.log(0 === Days['Sun'])

```

## 手动赋值

未手动赋值的枚举项与手动赋值的重复，TS 是不会发现的

```TypeScript
enum Days2 { Sun = 3, Mon = 1, Tue, Wed, Thu, Fri, Sat }

console.log(Days2['Sun'] === 3); // true
console.log(Days2['Wed'] === 3); // true
console.log(Days2[3] === 'Sun'); // false 被后面的Wed覆盖了
console.log(Days2[3] === 'Wed'); // true
```

手动赋值的枚举项可以为小数或负数，此时后续未手动赋值的项的递增步长仍为 1
```TypeScript

enum Days3 { Sun = 'A', Mon = 0.5, Tue, Wed, Thu, Fri, Sat }

```

手动赋值的枚举项可以不是数字，此时需要使用类型断言来让 tsc 无视类型检查
```TypeScript

enum Days4 { Sun, Mon = 0, Tue, Wed, Thu, Fri, Sat = <any>"A" }

```

## 常数项和计算所有项

枚举项有两种类型：常数项（constant member）和计算所得项（computed member）

枚举成员是常数项的条件：
- 不具有初始化函数并且之前的枚举成员是常数
- 枚举成员使用常数枚举表达式初始化

计算所有项：

```TypeScript
enum Color {Red, Green, Blue = "blue".length}

enum Color {Red = "red".length, Green, Blue} // 报错
```

**如果紧接在计算所得项后面的是未手动赋值的项，那么它就会因为无法获得初始值而报错**

## 常数枚举

常数枚举是使用 const enum 定义的枚举类型

常数枚举与普通枚举的区别是，它会在编译阶段被删除，并且不能包含计算成员

```TypeScript
const enum Directions {
    Up,
    Down,
    Left,
    Right
}

let directions = [Directions.Up, Directions.Down, Directions.Left, Directions.Right];
```

## 外部枚举

外部枚举（Ambient Enums）是使用 declare enum 定义的枚举类型(declare 定义的类型只会用于编译时的检查，编译结果中会被删除)

```TypeScript
declare enum Directions {
    Up,
    Down,
    Left,
    Right
}

let directions = [Directions.Up, Directions.Down, Directions.Left, Directions.Right];
```

* [下一节：类](https://github.com/KayanChan/weekly-javascript/blob/master/ts-summary/class.md)