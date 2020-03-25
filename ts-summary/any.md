# 任意值
任意值( Any )用来表示允许赋值为任意类型，允许在赋值过程中改变类型是被允许的，反之原始数据类型不被允许

```TypeScript
let anyValue: any = true
anyValue = 'hello world'
```

在任意值上访问任何属性都是允许的(编译不报错，但 js 文件执行可能会报错)
```TypeScript
let anyThing: any = 'one'
console.log(anyThing.myName)
console.log(anyThing.myName.firstName)
```

也允许调用任何方法
```TypeScript
anyThing.setName('Jerry')
anyThing.sayHi()
```

**声明一个变量为任意值之后，对它的任何操作，返回的内容的类型都是任意值**

变量如果在声明的时候，未指定其类型，那么它会被识别为任意值类型

* [下一节：类型推论](https://github.com/KayanChan/weekly-javascript/blob/master/ts-summary/type-inference.md)