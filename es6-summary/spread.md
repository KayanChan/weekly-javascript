### 扩展运算符(ES6的`...`符号)： 浅复制对象，还可以覆盖、拓展对象属性
   ```javascript
   const obj = { a: 1, b: 2}
   const obj2 = { ...obj } // => { a: 1, b: 2 }
   const obj3 = { ...obj, b: 3, c: 4} // => { a: 1, b: 3, c: 4 }，覆盖了 b，新增了 c
   ```