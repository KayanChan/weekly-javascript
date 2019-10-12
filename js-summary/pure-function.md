### 纯函数
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
