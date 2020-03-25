# 类型别名

使用 type 创建类型别名，类型别名常用于联合类型

```TypeScript

type Name = string;
type NameResolver = () => string;
type NameOrResolver = Name | NameResoler;
function getName(n: NameOrResolver): Name {
    if(typeof n === 'string') {
        return n;
    } else {
        n();
    }
}

```

* [下一节：字符串字面量类型](https://github.com/KayanChan/weekly-javascript/blob/master/ts-summary/string-literal-types.md)