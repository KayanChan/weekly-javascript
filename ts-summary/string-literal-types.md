# 字符串字面量类型

字符串字面量类型用来约束取值只能是某几个字符串中的一个

使用 type 定了一个字符串字面量类型 EventNames，它只能取**三种字符串中的一种**

```TypeScript
type EventNames = 'click' | 'scroll' | 'mousemove';

function handleEvent(ele: Element, event: EventNames) {
    // do something
}

handleEvent(document.getElementById('hello'), 'scroll'); 
```

* [下一节：元祖](https://github.com/KayanChan/weekly-javascript/blob/master/ts-summary/tuple.md)