---
title: js面向对象编程
date: 2019-02-13 10:46:32
tags:
---

## 构造函数
构造函数遵循一些约定：
1.构造函数使用大写名称定义，以区别于非构造函数的其他函数。
2.构造函数使用关键字this来设置它们将创建的对象的属性。在构造函数中，这指的是它将创建的新对象。
3.构造函数定义属性和行为，而不是像其他函数那样返回值。


```
function Bird() {
  this.name = "Albert";
  this.color = "blue";
  this.numLegs = 2;
}
```

## 创建对象
`let blueBird = new Bird();`
你可以使用对象的属性
`blueBird.name = 'Elvira';`

## 给构造函数传参数

```
function Dog(name, color) {
  this.name = name;
  this.color = color;
  this.numLegs = 4;
}

var terrier = new Dog('小黑', 'black');
```


## 使用instanceof验证Object的构造函数

```
function House(numBedrooms) {
  this.numBedrooms = numBedrooms;
}

var myHouse = new House(2);
myHouse instanceof House; // => true

```

## 判断是不是自有属性

``` 
  if (canary.hasOwnProperty(property)){
    ownProps.push(property);
  }
```

## 使用Prototype属性减少重复代码
由于numLegs对于Bird的所有实例可能具有相同的值，因此在每个Bird实例中基本上都有一个重复的变量numLegs。
当只有两个实例时，这可能不是问题，但想象一下是否有数百万个实例。这将是许多重复的变量。
更好的方法是使用Bird的原型。原型是一个在Bird的所有实例之间共享的对象。以下是如何将numLegs添加到Bird原型中：
`Bird.prototype.numLegs = 2;`

## 区分自由属性和原型属性
自己的属性直接在对象实例本身上定义。原型属性在原型上定义。

```
function Bird(name) {
  this.name = name; //own property
}

Bird.prototype.numLegs = 2; // prototype property

let duck = new Bird("Donald");
let ownProps = [];
let prototypeProps = [];

for (let property in duck) {
  if(duck.hasOwnProperty(property)) {
    ownProps.push(property);
  } else {
    prototypeProps.push(property);
  }
}

console.log(ownProps); // prints ["name"]
console.log(prototypeProps); // prints ["numLegs"]
```


## 请记住在更改原型时设置构造函数属性

```
Bird.prototype = {
  constructor: Bird, // define the constructor property
  numLegs: 2,
  eat: function() {
    console.log("nom nom nom");
  },
  describe: function() {
    console.log("My name is " + this.name); 
  }
};
```

## 理解对象的属性从哪里而来

```
function Bird(name) {
  this.name = name;
}

let duck = new Bird("Donald");
Bird.prototype.isPrototypeOf(duck); // true

````

## Object.create 
Object.create 不会有父类的自带属性，只有有父类的原生链属性
Object.create ( O [ , Properties ] ) 操作步骤很简单，如下： 
1. If Type(O) is neither Object nor Null, throw a TypeError exception. 
2. Let obj be ObjectCreate(O). 
3. If the argument Properties is present and not undefined, then a. Return ObjectDefineProperties(obj, Properties).
4. Return obj.

## 将Child的Prototype设置为Parent的实例
`Bird.prototype = Object.create(Animal.prototype);`
Bird的所有实例对象将拥有Animal的所有的prototype属性

## 重置继承之类的构造函数属性

```
function Bird() { }
Bird.prototype = Object.create(Animal.prototype);
let duck = new Bird();
duck.constructor // function Animal(){...
Bird.prototype.constructor = Bird;
duck.constructor // function Bird(){...}
```

## 添加/覆盖继承的方法
直接通过原型链修改

## 使用Mixin在不相关的对象之间添加常见行为
行为是通过继承共享的。但是，有些情况下继承不是最佳解决方案。对于像Bird和Airplane这样的无关对象，继承不起作用。它们都可以飞行，但是Bird不是一种飞机，反之亦然。
对于不相关的对象，最好使用mixins。 mixin允许其他对象使用一组函数。

```
let flyMixin = function(obj) {
  obj.fly = function() {
    console.log("Flying, wooosh!");
  }
};
```

flyMixin接受任何对象并为其提供fly方法。

```
let bird = {
  name: "Donald",
  numLegs: 2
};

let plane = {
  model: "777",
  numPassengers: 524
};

flyMixin(bird);
flyMixin(plane);
```

结果

```
bird.fly(); // prints "Flying, wooosh!"
plane.fly(); // prints "Flying, wooosh!
```

## 使用闭包保护对象内的属性不被外部修改

```
function Bird() {
  let hatchedEgg = 10; // private property

  this.getHatchedEggCount = function() { // publicly available method that a bird object can use
    return hatchedEgg;
  };
}
let ducky = new Bird();
ducky.getHatchedEggCount(); // returns 10
```



