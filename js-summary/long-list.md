### 长列表

  * 数据长度比较大(数千条)

  * 并且不能分页

#### 思考

  1. 完整渲染的长列表的优化

  2. 非完整的渲染长列表的方案

#### 完整渲染长列表

  1. 测试一次完整渲染长列表的渲染

    ```javascript
    // createElements
    const createElements = (count) => {
        
    console.log('!createElements开始----------')
        
    const start = new Date()
    
    for(let i=0; i<count; i++) {
        
      const element = document.createElement('div')
      
      element.appendChild(document.createTextNode(` ${i}`))
        
      document.body.appendChild(element)
        
    }
    setTimeout(() => {
        
      console.log(new Date() - start)
        
      console.log('!createElements结束----------')
        
    }, 0)
    ```
    ```javascript
    // createElementWithFragment

    console.log('!createElementWithFragment开始----------')

    const start = new Date()
    
    // 创建虚拟节点对象
    let fragment = document.createDocumentFragment()
    
    for(let i=0; i<count; i++) {
        
      const element = document.createElement('div')
      
      element.appendChild(document.createTextNode(` ${i}`))
        
      fragment.appendChild(element)
        
    }

    document.body.appendChild(fragment)

    setTimeout(() => {
        
      console.log(new Date() - start)
        
      console.log('!createElementWithFragment结束----------')
        
    }, 0)
    ```
    ```javascript
    // innerHTML
    console.log('!createElementWithHTML开始----------')

    const start = new Date()
    
    let array = []

    for(let i=0; i<count; i++) {
        
      array.push(`<div> ${count}</div>`)
        
    }

    const element = document.createElement('div')
    
    element.innerHTML = array.join('')

    document.body.appendChild(element)

    setTimeout(() => {
        
      console.log(new Date() - start)
        
      console.log('!createElementWithFragment结束----------')
        
    }, 0)
    ```

  2. 结论

     `innerHTML` 比 `createElement` 和 `createDocumentFragment` 有性能优势(大约10%)，但是对于解决性能瓶颈，作用不大，所以完整渲染的长列表基本上很难达到业务上的要求的

#### 非完整渲染长列表
  1. 懒渲染: 无限滚动，不断加载数据
      * 后端一次加载比较少的数据可以节省流量
      * 前端首次渲染更少的数据速度会更快
      * 产品方必须接受这种形式的列表

      **思路实现**
      监听父元素的 scroll 事件（一般是 window），通过父元素的 scrollTop 判断是否到了页面是否到了页面底部，如果到了页面底部，就加载更多的数据

      **[代码查看](https://github.com/KayanChan/weekly-javascript/blob/master/code/vue/LazyList.vue)**

  2. 可视区域渲染: 只渲染可见部分，不可见部分不渲染

      **思路实现**
      1. `list-view`容器为可视区域容器`overflow:auto`

      2. `list-view-phantom`填充全部数据`listData`，不可见但可使可视区域可滚动

      3. `list-view-content`根据可视区域的高度,，来显示由起始和结束索引`start、end`截取的可视区域数据`visibleData`

      4. `scroll`滚动事件中修改位移值`transform: translateY(y)`或者`translate3d(0, y, 0)`

      **[代码查看](https://github.com/KayanChan/weekly-javascript/blob/master/code/vue/VisibleAreaRenderList.vue)**