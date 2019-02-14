---
title: sass
date: 2019-02-14 11:05:21
tags:
---

## 变量的声明与使用
`
$main-fonts: Arial, sans-serif;
$headings-color: green;
//To use variables:
h1 {
  font-family: $main-fonts;
  color: $headings-color;
}`

## mixins指令的使用
`@mixin box-shadow($x, $y, $blur, $c){ 
  -webkit-box-shadow: $x, $y, $blur, $c;
  -moz-box-shadow: $x, $y, $blur, $c;
  -ms-box-shadow: $x, $y, $blur, $c;
  box-shadow: $x, $y, $blur, $c;
}
div {
  @include box-shadow(0px, 0px, 4px, #fff);
}
`

## if判断指令的使用
`@mixin text-effect($val) {
  @if $val == danger {
    color: red;
  }
  @else if $val == alert {
    color: yellow;
  }
  @else if $val == success {
    color: green;
  }
  @else {
    color: black;
  }
}`

## for循环指令的使用
`<style type='text/sass'>
  @for $j from 1 to 6 {
    .text-#{$j} { font-size: 10px*$j; }
  }
</style>
`

## map遍历指令的使用
在每次迭代时，变量将从列表或映射分配给当前值。
`@each $color in blue, red, green {
  .#{$color}-text {color: $color;}
}
`
迭代的语法有不通，也可以这样写
`$colors: (color1: blue, color2: red, color3: green);

@each $key, $color in $colors {
  .#{$color}-text {color: $color;}
}
`

## while循环质量的使用
@for挑战给出了一个创建简单网格系统的示例。这也适用于@while。
首先，定义变量$ x并将其设置为1.接下来，使用@while指令创建网格系统，而$ x小于13。
`$x: 1;
@while $x < 13 {
  .col-#{$x} { width: 100%/12 * $x;}
  $x: $x + 1;
}`

## 引用变量文件_mixins.scss
`@import 'mixins'`

##将一组CSS样式扩展到另一个元素
例如，下面的CSS规则块为.panel类设置样式。它有背景颜色，高度和边框。
`.panel{
  background-color: red;
  height: 70px;
  border: 2px solid green;
}
`
现在你想要另一个名为.big-panel的面板。它具有与.panel相同的基本属性，但也需要宽度和字体大小。
extend指令是一种重用为一个元素编写的规则的简单方法，然后为另一个元素添加更多：
`
.big-panel{
  @extend .panel;
  width: 150px;
  font-size: 2em;
}
`


