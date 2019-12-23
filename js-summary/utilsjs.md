## utils.js常见JS方法封装
[笔记来源](https://juejin.im/post/5deb2cdf518825122671b637#heading-23)

### 日期

1. 年份
```javascript
dateY = time => {
  let newDate = new Date(time)
  let {y} = {y: newDate.getFullYear()}
  return `${y}`
}
```

2. 年-月
```javascript
dateYM = time => {
  let newDate = new Date(time)
  let {y, m} = {y: newDate.getFullYear(), m: newDate.getMonth()+1}
  return `${y}-${m}`
}
```

3. 年-月-日
```javascript
dateYM = (time) => {
  let newDate = new Date(time)
  let {y, m, d} = {y: newDate.getFullYear(), m: newDate.getMonth()+1, d: newDate.getDate()}
  return `${y}-${m}-${d}`
}
```

4. 年-月-日 时：分：秒
```javascript
dateTime = (time) => {
  let newDate = new Date(time)
  let {y, M, d, h, m, s} = {
    y: newDate.getFullYear(),
    M: newDate.getMonth()+1,
    d: newDate.getDate(),
    h: newDate.getHours(),
    m: newDate.getMinutes(),
    s: newDate.getSeconds()
  }
  const checkTime = val => (val < 10) ? `0${val}` : val
  return `${y}-${checkTime(M)}-${checkTime(d)} ${checkTime(h)}:${checkTime(m)}:${checkTime(s)}`
}
```

## JS原生

1. 防抖(只执行最后一次操作)
```javascript
Debounce = (fn, t) => {
  let delay = t || 500
  let timer
  return function() {
    let args = arguments
    if(timer) {
      clearTimeout(timer)
    } else {
      timer = setTimeout(() => {
        timer = null
        fn.apply(this, args)
      }, delay)
    }
  }
}

```

2. 节流(隔一段时间执行操作)
```javascript
Throttle = (fn, t) => {
  let last
  let timer
  let interval = t || 500
  return function() {
    let args = arguments
    let now = +new Date()
    if(last && now-last < interval) {
      clearTimeout(timer)
      timer = setTimeout(() => {
        last = now
        fn.apply(this, args)
      })
    } else {
      last = now
      fn.apply(this, args)
    }
  }
}
```