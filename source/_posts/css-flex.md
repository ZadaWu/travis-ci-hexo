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


