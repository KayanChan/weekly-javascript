# 元祖

数组合并了相同类型的对象，而元组（Tuple）合并了不同类型的对象

当直接对元组类型的变量进行初始化或者赋值的时候，需要提供所有元组类型中指定的项

当赋值或访问一个已知索引的元素时，会得到正确的类型，也可以赋值其中一项

```TypeScript
let tom: [string, number] = ['Tom', 25]

let tom2: [string, number]

tom2[0] = 'Tom'
```

## 越界的元素

当添加越界的元素时，它的类型会被限制为元组中每个类型的联合类型

```TypeScript
let tom2: [string, number]

tom2[0] = 'Tom'

tom2.push('male')

tom2.push(2)
```

* [下一节：枚举](https://github.com/KayanChan/weekly-javascript/blob/master/ts-summary/enum.md)