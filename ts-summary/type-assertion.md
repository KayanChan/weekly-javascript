# 类型断言

类型断言（Type Assertion）可以用来手动指定一个值的类型

`(<类型>值)` 或 `值 as 类型` 将一个联合类型的变量指定为一个更加具体的类型

在 tsx 语法（React 的 jsx 语法的 ts 版）中必须用`值 as 类型`

```TypeScript
function  getLength(target: string | number): number {
    if((<string>target).length) {
        return (<string>target).length
    } else {
        return target.toString().length
    }
}
```

**类型断言不是类型转换，断言成一个联合类型中不存在的类型是不允许的**

* [下一节：声明文件](https://github.com/KayanChan/weekly-javascript/blob/master/ts-summary/declaration-files.md)