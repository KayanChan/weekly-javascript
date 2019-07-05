### weekly-javascript

#### @2019-07-01  ES6的常用数组操作

   * 数组复制，不可变操作

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



   * 数组过滤(也可以删除)，不可变操作

      `Array.filter`

      ```
      var words = ['spray', 'limit', 'elite', 'exuberant', 'destruction', 'present'];

      const result = words.filter((word, index) => word.length > 6);

      console.log(result);
      ```



   * 数组元素更新，不可变操作

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

##### catalog

   - [第一部分 基础语法](https://github.com/KayanChan/weekly-javascript/blob/master/reactjs-summary/basic-grammer.md)

   - [第二部分 生命周期](https://github.com/KayanChan/weekly-javascript/blob/master/reactjs-summary/life-cycle.md)

   - [第三部分 高阶组件](https://github.com/KayanChan/weekly-javascript/blob/master/reactjs-summary/high-order-component.md)
   
   - [第四部分 Redux](https://github.com/KayanChan/weekly-javascript/blob/master/reactjs-summary/Redux.md)

##### Question&Answer

   > 为什么`react-dom`不包含在`react`当中？

   > 如何更好的管理这种被多个组件所依赖或影响的状态？

#### @2019-07-04 纯函数(Pure Function)

   * 函数的返回结果只依赖于它的参数
   * 函数执行过程里面没有副作用
   * 编写纯函数优点在于结果可预测，不会对外部产生影响，调试方便

   ```javascript
      // 不是纯函数，因为依赖于外部变量a
      const a = 1
      function foo(b) {
          return a+b
      }
      const c = foo(2) // =>3

      // 是纯函数
      function foo(a, b) {
          return a+b
      }
      const c = foo(1, 2) // =>3
   ```

   ```javascript
   // 不是纯函数，函数的执行对外部 obj 产生了副作用
      const obj = {a: 1}

      function foo(obj, b) {
          obj.a = 2
          return obj.a + b
      }

      const c = foo(obj, 2) // =>4
      console.log(obj) // => {a: 2}


      // 是纯函数
      const obj = {a: 1}

      function foo(obj, b) {
          return obj.a + b
      }

      const c = foo(obj, 2) // =>3
   ```

#### @2019-07-05 ES6的`...`符号： 浅复制对象，还可以覆盖、拓展对象属性
   ```javascript
   const obj = { a: 1, b: 2}
   const obj2 = { ...obj } // => { a: 1, b: 2 }
   const obj3 = { ...obj, b: 3, c: 4} // => { a: 1, b: 3, c: 4 }，覆盖了 b，新增了 c
   ```
