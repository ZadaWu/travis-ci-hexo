---
title: css 之 animation, transform
date: 2018-12-21 18:08:00
tags: css
---

先强烈推荐一个前端程序员可以自己练习基础的网站：[https://learn.freecodecamp.org](https://learn.freecodecamp.org)，作为一个工作了3年半的前端工程师，表示在这里也收集了不少自己缺少的技能点。

今天要分享的就是animation, 和transform

## transfrom
属性允许你旋转，缩放，倾斜或平移给定元素。且transform默认是绕着中心点旋转的。
你可以通过transform-origin修改中心点位置，比如：
transform-origin: bottom left;-中心点为左下角位置角
transform-origin: 50px 70px; -中心点位置有中间移到了距离左侧50像素，顶部70像素的地方


```
scale(x,y) 放大／缩小倍数
rotate(deg) 旋转角度
skewX(xdeg) 横向拉升 
skewY(ydeg) 纵向拉升
skew(xdeg, ydeg) 横纵向都拉伸
translate(x, y) 原点向右或向下挪动
matrix(a, b, c, d, e, f) 理解成3*3矩阵，原点位置x, y, 则实际x变化位置为ax+cy+e,y变化位置为bx+dy+f,等同于transform: translate(ax+cy+e+'px', bx+dy+f+'px') [详情请点击](https://segmentfault.com/a/1190000011942578)
matrix3d() 3D变换 4*4矩阵
```

## animation
annimation配合keyframes一起用

```
@keyframes slidein {
  from { transform: scaleX(0); }
  to   { transform: scaleX(1); }
}
```


```
animation-name  动画name
animation-duration 一个动画周期的时长，单位为秒(s)或者毫秒(ms)
animation-timing-function 定义CSS动画在每一动画周期中执行的节奏 ease／ease-in／ease-out／linear [贝塞尔曲线原理](https://www.jianshu.com/p/d999f090d333) [贝塞尔曲线对比](http://cubic-bezier.com/#.25,.1,.25,1)
animation-delay 定义动画于何时开始，即从动画应用在元素上到动画开始的这段时间的长度。
animation-iteration-count 循环次数
animation-direction 属性指示动画是否反向播放 normal／reverse／alternate／alternate-reverse
animation-fill-mode 用来指定在动画执行之前和之后如何给动画的目标应用样式。 none／forwards／backwards／both／应用多个none, backwards／应用多个both, forwards, none
```

