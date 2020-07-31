## debounce防抖和throttle节流

debounce(强力限流)：将短时间内多次触发的事件合并成一次事件响应函数执行（往往是在第一次事件或者在最后一次事件触发时执行），即该段时间内仅一次真正执行事件响应函数。
```
const debounce = function(fn,delay){
  let timer = null
  return ()=> {
    clearTimeout(timer)
    timer = setTimeout(()=>fn(), delay)
  }
}
```

throttle(一般限流)：假如在短时间内同一事件多次触发，那么每隔一段更小的时间间隔就会执行事件响应函数，即该段时间内可能多次执行事件响应函数。
```
const throttle = function(fn,delay){
  let prev = Date.now()
  return ()=> {
    let now = Date.now()
    if (now - prev >= delay) {
        fn()
        prev = Date.now()
    }  
  }
}
```
