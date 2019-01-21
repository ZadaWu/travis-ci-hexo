---
title: css-flex
date: 2019-01-21 11:16:05
tags: css
---


## flex 
Adding display: flex to an element turns it into a flex container. This makes it possible to align any children of that element into rows or columns. 
* 父元素是display:flex的情况下，按百分比显示，子元素可以并行显示，并且按比例平分

### flex-direction:
* row : 按行, 可以理解为左右布局
* col : 按列, 可以理解为上下不举
* row-reverse : 按行倒转
* col-reverse : 按列倒转

### justify-content
该属性是配合display:flex和flex-direction来使用，在子元素确定宽度/高度的情况下，可以改变排列方式，从而来实现一些我们想要的布局。
justify-content属性沿着主轴对齐flex项目。对于行，主轴是水平线，对于列，它是垂直线。

* justify-content: center 元素靠中对齐
* justify-content: flex-start 元素靠左排列显示,顺序不变
* justify-content: flex-end  元素靠右排列显示,顺序不变
* justify-content: space-between 元素靠两边显示，最左右不留空隙，中间等比出来，可以分成n等分
* justify-content: space-around 元素靠两边显示，最左右留空隙，中间等比出来，可以分成n等分

### align-items
Flex容器还具有与主轴相反的横轴。对于行，横轴是垂直的，对于列，横轴是横向。
CSS提供align-items属性以沿着交叉轴对齐flex项。对于一行，它告诉CSS如何在容器内向上或向下推动整行中的项目。对于列，如何在容器内向左或向右推送所有项目。

* flex-start: 将项目对齐到Flex容器的开头。对于行，这会将项目对齐到容器的顶部。对于列，这会将项目对齐容器的左侧。
* flex-end: 将项目对齐到Flex容器的末尾。对于行，这会将项目对齐到容器的底部。对于列，这会将项目对齐到容器的右侧。
* center: 将项目与中心对齐。对于行，这会垂直对齐项目（项目上方和下方的空间相等）。对于列，它会水平对齐它们（项目左侧和右侧的空格相等）。
* stretch: 拉伸项目以填充弹性容器。例如，行项目被拉伸以从上到下填充Flex容器。
* baseline: 将项目与其基线对齐。基线是一个文本概念，将其视为字母所在的行。


### flex-wrap
它告诉CSS包装项目。这意味着额外的项目将移动到新的行或列中。包装发生的断点取决于物品的大小和容器的大小。使用场景，可以用来list的item排列

* nowrap: 这是默认设置，不包装项目，会挤压项目，原来的宽度/高度会受影响。
* wrap: 如果项目在一行中，则从左到右包装，如果它们在列中，则从上到下包装。
* wrap-reverse:如果项目在一行中，则从下到上包装项目;如果它们在列中，则从右到左包装。


### flex-shrink
之上的属性都是用来父级元素，当它被使用时，如果flex容器太小，它允许物品收缩。当父容器的宽度小于其中所有flex项的组合宽度时，项会收缩。lex-shrink属性将数字作为值。数字越大，与容器中的其他项目相比，它将缩小得越多。
比如说：本来都是width100%的box，如果一个为1，一个为2，则为1的宽度为2的2倍

### flex-grow
与flex-shrink属性对立。当容器缩小时，flex-shrink控制项目的大小。当父容器展开时，flex-grow属性控制项的大小。数字越大,宽度越宽
比如说：本来都是width未设置的box，如果一个为1，一个为2，则为1的宽度为2的1/2

### flex-basis
flex-basis属性指定CSS在使用flex-shrink或flex-grow进行调整之前的项的初始大小

### 属性缩写
有一个快捷方式可以同时设置多个flex属性。通过使用flex属性，可以将flex-grow，flex-shrink和flex-basis属性设置在一起。
例如，flex：1 0 10px;将项目设置为flex-grow：1;，flex-shrink：0;和flex-basis：10px;。


### order
使用order属性重新排列项目
order大的顺序排列在前面

### align-self
此属性允许您单独调整每个项目的对齐方式，而不是一次性设置它们。这很有用，因为使用CSS属性float，clear和vertical-align的其他常见调整技术对flex项不起作用。
align-self接受与align-items相同的值，并将覆盖align-items属性设置的任何值。


