---
title: '2019-06-19:请实现一个 flattenDeep 函数'
date: 2019-06-19 16:12:43
tags: [Step-By-Step]
---

## 前言 
这是来自于参与刘小夕同学的GitHub项目的每日一题，[地址在此](https://github.com/YvetteLau/Step-By-Step/issues/27)，感兴趣的同学可以联系她哟～

## 请实现一个 flattenDeep 函数，将嵌套的数组扁平化
### 使用递归实现的方式（我的）

```
flattenDeep([1, [2, [3, [4]], 5]])   // [ 1, 2, 3, 4, 5 ]
```
实现如下：

```
function isArray (array) {
    return typeof array === 'object' && array instanceof Array
}
var result = []
function flatternDeep(array) {
    if (!isArray(array)) {
        return array
    }
    // 本质上仍旧是需要递归来解决
     array.forEach(arrayItem => {
        if (isArray(arrayItem)) {
            flatternDeep(arrayItem)
        } else {
            result.push(arrayItem)
        }
    })
}
```

### 大佬的:flat deep

```
var arr3 = [1, 2, [3, 4, [5, 6]]];
//使用 Infinity 作为深度，展开任意深度的嵌套数组
arr3.flat(Infinity); // // [1, 2, 3, 4, 5, 6]
```
flat()简直是黑魔法，请查看[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/flat)

### 大佬的:栈，先入后出，后入先出

```
const arr = [1, 2, 3, [4, 5, 6, [7, 8, 9, [10, 11, 12]]]];
const flattenDeep = arr => {
    const resArr = [];
    while (arr.length > 0) {
        const next = arr.pop();
        if (Object.prototype.toString.call(next) === '[array Object]') {
                arr.push(...next);
        } else {
          	resArr.push(next);  
        };
    };
    return resArr.reverse();
};
```

### 大佬的：reduce

```
const flattenDeep = (arr) => arr.reduce((cur,pre) => cur.concat(Array.isArray(pre) ? flattenDeep(pre) : pre), [])
```



