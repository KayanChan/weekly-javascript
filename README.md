### weekly-javascript

#### @2019-07-01  ES6的常用数组操作

数组复制，不可变操作

1. `object.assign([], source)`

   ```js
   let a = [1,2,3]
   let b = Object.assign([], a)
   b.push(4)
   // a: [1,2,3]
   // b: [1,2,3,4]
   ```

   

2. 操作符`...`

   ```js
   let a = [1,2,3]
   let b = [...a,4,5]
   // a: [1,2,3]
   // b: [1,2,3,4,5]
   ```



数组过滤(也可以删除)，不可变操作

`Array.filter`

```
var words = ['spray', 'limit', 'elite', 'exuberant', 'destruction', 'present'];

const result = words.filter((word, index) => word.length > 6);

console.log(result);
```



数组元素更新，不可变操作

`Array.map`

```js
var arr = [1,2,3,4,5] ;
var newArr = arr.map(function(item,index){
   return item*2 ;
}) 
// arr: [1,2,3,4,5]
// newArr: [2, 4, 6, 8, 10]
```



#### @2019-07-02  [前端组件化](https://github.com/KayanChan/weekly-javascript/blob/master/frontend-componentization/README.md)（理解基础的 React.js 的概念）

* 如何尽量减少手动`DOM 操作`：一旦状态发生改变，就重新调用`render`方法，构建一个新的`DOM 元素`。
* 通过类实现组件的继承，抽象出公共组件类`Component`



#### @2019-07-03 React.js汇总

### catalog

- [第一部分 基础语法](https://github.com/KayanChan/weekly-javascript/blob/master/reactjs-summary/basic-grammer.md)

### Question&Answer

> 为什么`react-dom`不包含在`react`当中？

