# 联合类型( Union Types )
联合类型（Union Types）表示取值可以为多种类型中的一种。

联合类型使用 | 分隔每个类型

```TypeScript
let unionTypesValue: string | number
unionTypesValue = 'string'
unionTypesValue = 7
```

只能访问此联合类型的所有类型里**共有的**属性或方法，例如 string 和 number 共有的方法 toString()

```TypeScript
function getString(something: string | number): string {
    return something.toString()
}
```

联合类型的变量在被赋值的时候，会根据类型推论的规则推断出一个类型，只能访问当前类型的属性
```TypeScript
let unionTypesValue: string | number
unionTypesValue = 'string'
unionTypesValue.length
unionTypesValue = 7
unionTypesValue.length // 报错
```
> error TS2339: Property 'length' does not exist on type 'number'

* [下一节：接口](https://github.com/KayanChan/weekly-javascript/blob/master/ts-summary/interfaces.md)