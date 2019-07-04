---
title: '2019-07-04:原型链继承的优缺点是什么？使用原型链继承实现 Dog 继承 Animal'
date: 2019-07-04 11:51:31
tags: [Step-By-Step]
---

## 前言 
这是来自于参与刘小夕同学的GitHub项目的每日一题，[地址在此](https://github.com/YvetteLau/Step-By-Step/issues/34)，感兴趣的同学可以联系她哟～

## 原型链
### 原型链继承的优缺点是什么？
优点：子能继承父的方法和属性，不需要重新写一遍，能增加代码的服用
缺点：子类只能用父类的属性和方法

### 使用原型链继承实现Dog继承Animal

```
function Animal(type, name){
    this.type = type
    this.name = name
}

Animal.prototype.getNameAndType = function () {
    console.log(`name: ${this.name} , type: ${this.type}`)
} 

function Dog() {
}

Dog.prototype = new Animal('dog', '小黑')
var dog = new Dog()
dog.getNameAndType()
```

