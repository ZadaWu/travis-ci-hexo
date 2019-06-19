---
title: '2019-06-19:实现 Promise.all 方法'
date: 2019-06-19 15:08:45
tags: [面试]
---

## 前言 
这是来自于参与刘小夕同学的GitHub项目的每日一题，[地址在此](https://github.com/YvetteLau/Step-By-Step/issues/25)，感兴趣的同学可以联系她哟～

## 实现Promise.all
 
```
function isArray(object){
    return object && typeof object==='object' &&
            object instanceof Array;
}

Promise.myall = function (promiseList) {
  if (!isArray(promiseList)) {
    return 'not an array'
  }
  return new Promise ((resolve, reject)=> {
    let count = 0
    promiseList.forEach(element => {
        element.then(() => {
          count ++;
          if (promiseList.length === count) {
            resolve()
          }
        }).catch(error =>{
          reject(error)
        })
    })
  })
}
```

### 测试代码
```
var p1 = Promise.resolve(1),
    p2 = Promise.reject(2),
    p3 = Promise.resolve(3);
Promise.myall([p1, p2, p3]).then(function (results) {
    //then方法不会被执行
    console.log(results);
}).catch(function (e){
    //catch方法将会被执行，输出结果为：2
    console.log(2);
});
```

