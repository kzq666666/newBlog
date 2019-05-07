+++
title = "JsAlg"
date = 2019-04-27T09:25:17+08:00
draft = false
+++

### 数组去重
```js
function noRepeat(arr){
  return arr.filter((ele,index)=>{
    return arr.indexOf(ele) == index;
  })
}
```
