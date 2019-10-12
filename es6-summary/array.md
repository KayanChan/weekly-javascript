### ES6的常用数组操作

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


