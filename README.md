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

#### @2019-07-02 jsx的原理
每个 DOM 元素的结构都可以用 JavaScript 的对象来描述。一个`DOM`元素包含的信息其实只有三个：标签名，属性，子元素
```javascript
{
  tag: 'div',
  attrs: { className: 'box', id: 'content'},
  children: [
    {
      tag: 'div',
      arrts: { className: 'title' },
      children: ['Hello']
    },
    {
      tag: 'button',
      attrs: null,
      children: ['Click']
    }
  ]
}
```
`React.createElement`会构建一个 JavaScript 对象来描述`HTML`结构的信息，包括标签名、属性、还有子元素等。由于js对象描述的篇幅过长，于是通过扩展js的语法，即`jsx`来处理。实际`jsx`会通过`Babel编译+React.js的构造`得到`js对象`，从而去操作`DOM`（`React-DOM.render`）。另外，`jsx`不直接操作`DOM`是避免浏览器的重排，性能的优化；而且得到一个表示UI的结构和信息的对象，不一定会把元素渲染到浏览器的普通页面上，如`canvas`。

