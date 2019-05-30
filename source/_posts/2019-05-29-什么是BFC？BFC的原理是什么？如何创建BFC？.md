---
title: '2019-05-29:什么是BFC？BFC的原理是什么？如何创建BFC？'
date: 2019-05-29 18:34:09
tags: 面试
---

## 前言 
这是来自于参与刘小夕同学的GitHub项目的每日一题，[地址在此](https://github.com/YvetteLau/Step-By-Step/issues/15)，感兴趣的同学可以联系她哟～

今日的题目是“什么是BFC？BFC的原理是什么？如何创建BFC？”， 回答这个问题我准备从 **what how why** 这5个方面来回答。

## 我的观点

### what（什么是BFC）
参考[MDN](https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Block_formatting_context)，BFC（块格式化上下文）是Web页面的可视化CSS渲染的一部分，是块盒子的布局过程中发生的区域，而且存在浮动元素与其他元素交互的区域。
我看完的感觉是哦，但是还没怎么懂，之前也是只知道能怎么用。那么我就继续去看了相关的[术语文档](https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Visual_formatting_model)。所以我理解下来就是一个包含子元素的块级元素，在这个区域里面布局，或者浮动作用于子元素上，这样的情况就是BFC。

#### 术语普及
块盒子：block box，如果一个块级盒子同时也是一个块容器盒子（见下），则称其为块盒子。除具名块盒子之外，还有一类块盒子是匿名的，称为匿名块盒子（Anonymous block box），匿名盒子无法被CSS选择符选中。
块级元素：block-level element，元素的 display 为 block、list-item、table 时，该元素将成为块级元素。元素是否是块级元素仅是元素本身的属性，并不直接用于格式化上下文的创建或布局。
块容器盒子：block container box或block containing box，块容器盒子侧重于当前盒子作为“容器”的这一角色，它不参与当前块的布局和定位，它所描述的仅仅是当前盒子与其后代之间的关系。换句话说，块容器盒子主要用于确定其子元素的定位、布局等。

### why（为什么要用BFC）
因为在写css的过程中，我们会遇到这样的情况：
1. 父元素和子元素的外边距合并
2. 子元素在使用浮动的时候，父元素出现高度塌陷
3. 同级元素被同级浮动元素覆盖
为了解决这些问题，我们需要触发BFC

### how（怎么做）
继续往下说，怎么解决上面的问题
1. 父元素和子元素的外边距合并： overflow: hidden;
2. 子元素在使用浮动的时候，父元素出现高度塌陷：  overflow: hidden;
3. 同级元素被同级浮动元素覆盖：overflow: hidden;

当然，这只是上面三个问题的解决方案。
MDN上介绍触发BFC的方式如下：

* 根元素或包含根元素的元素
* 浮动元素（元素的 float 不是 none）
* 绝对定位元素（元素的 position 为 absolute 或 fixed）
* 行内块元素（元素的 display 为 inline-block）
* 表格单元格（元素的 display为 table-cell，HTML表格单元格默认为该值）
* 表格标题（元素的 display 为 table-caption，HTML表格标题默认为该值）
* 匿名表格单元格元素（元素的 display为 table、table-row、 table-row-group、table-header-group、table-footer-group（分别是HTML table、row、tbody、thead、tfoot的默认属性）或 inline-table）
* overflow 值不为 visible 的块元素
* display 值为 flow-root 的元素
* contain 值为 layout、content或 strict 的元素
* 弹性元素（display为 flex 或 inline-flex元素的直接子元素）
* 网格元素（display为 grid 或 inline-grid 元素的直接子元素）
* 多列容器（元素的 column-count 或 column-width 不为 auto，包括 column-count 为 1）
* column-span 为 all 的元素始终会创建一个新的BFC，即使该元素没有包裹在一个多列容器中（标准变更，Chrome bug）。





