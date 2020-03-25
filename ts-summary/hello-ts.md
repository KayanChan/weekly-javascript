# Hello TypeScript

## 编写一个TS文件编译成JS文件
新建的`hello.ts`文件，编码：
```TypeScript
function sayHello(person: string) {
    return 'Hello, ' + person
}

let user = 'World'

console.log(sayHello(user))
```

执行`tsc hello.js`后得到`hello.js`

**TypeScript 只会进行静态检查，如果发现有错误，编译的时候就会报错**
**TypeScript 编译的时候即使报错了，还是会生成编译结果**

如果要在报错的时候终止js文件的生成，可以在`tsconfig.json`中配置`noEmitOnError`即可

`tsconfig.json`指定了用来编译这个项目的根文件和编译选项，所在目录是TypeScript项目的根目录

* [下一节：原始数据类型](https://github.com/KayanChan/weekly-javascript/blob/master/ts-summary/primitive-data-types.md)