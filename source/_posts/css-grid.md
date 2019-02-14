---
title: css-grid
date: 2019-01-21 15:14:21
tags: css
---

## Grid
通过将其display属性设置为grid，将任何HTML元素转换为网格容器。这使您能够使用与CSS Grid关联的所有其他属性。
example: dislplay:grid;

### grid-template-columns
除了设置display,还需要定义网格的结构。要向网格添加一些列，请在网格容器上使用grid-template-columns属性，如下所示：
```.container {
  display: grid;
  grid-template-columns: 50px 50px;
}```

给grid-template-columns属性的参数数量表示网格中的列数，每个参数的值表示每列的宽度。
一行设置3个div宽度为100px：

```display: grid;
grid-template-columns: 100px 100px 100px;
```
px表示多宽

#### 使用repeact 来减少重复的工作
让我们说你想要一个100行相同高度的网格。单独插入100个值是不太实际的。幸运的是，有一种更好的方法 - 使用repeat函数指定要重复列或行的次数，后跟逗号和要重复的值。这是一个创建100行网格的示例，每行高度为50px的例子：
`grid-template-rows: repeat(100, 50px);`
您还可以使用repeat函数重复多个值，并在定义网格结构时将该函数插入其他值中。这就是我的意思：
`grid-template-columns: repeat(2, 1fr 50px) 20px;`
等同于：
`grid-template-columns: 1fr 50px 1fr 50px 20px;`

#### 使用minmax来限制大小
用于在网格容器更改大小时限制项目的大小。要执行此操作，您需要指定项目的可接受大小范围。这是一个例子：
`grid-template-columns: 100px minmax(50px, 200px);`

#### 使用auto-fill创建灵活布局（可以考虑用来做六部剧）
重复功能带有一个名为自动填充的选项。这允许您根据容器的大小自动插入所需大小的行或列。将auto-fill与minmax组合时，可以创建灵活的布局。如果您的容器无法在一行中容纳所有项目，则会将其移动到新行。
当容器改变大小时，此设置将继续插入60px列并拉伸它们，直到它可以插入另一个：
`
display: grid;
repeat(auto-fill, minmax(60px, 1fr));
grid-template-rows: 1fr 1fr 1fr;
grid-gap: 10px;
`

#### 使用auto-fit 创建灵活布局
auto-fit几乎与auto-fill相同。唯一的区别是当容器的大小超过所有项目组合的大小时，auto-fill会一直插入空行或列，并将项目推向一边，而auto-fit会折叠这些空行或列并拉伸项目以适合容器的大小。
始终元素是一行这几个，并且宽度随着变宽会拉伸。
如果您的容器无法在一行中容纳所有项目，则会将其移动到新行。


###  grid-template-rows
grid-template-columns的网格将自动设置行数。要手动调整行，请使用grid-template-rows属性，方法与用grid-template-columns的方式相同。
px表示多高

### 使用CSS网格单位更改列和行的大小
您可以在CSS Grid中使用绝对和相对单位（如px和em）来定义行和列的大小。你也可以使用这些：

* fr：将列或行设置为可用空间的一小部分。
* auto：自动将列或行设置为其内容的宽度或高度。
* ％：将列或行调整为其容器的百分比宽度。

ex:grid-template-columns: auto 50px 10% 2fr 1fr;
代码段创建了五列。第一列与其内容一样宽，第二列是50px，第三列是其容器的10％，最后两列;剩下的空间分为三个部分，两个分配给第四列，一个分配给第五个。
n个元素都会按照这个样式每行如此现实


### grid-column-gap
到目前为止，在你创建的网格中，列都相互紧密相连。有时您希望列之间存在间隙。要在列之间添加间隙，请使用grid-column-gap属性，如下所示三行三列每列中间有10px的间隙：
```grid-template-columns: 1fr 1fr 1fr;
grid-template-rows: 1fr 1fr 1fr;
grid-column-gap: 10px;```

### grid-column-row
类似于grid-column-gap，用与设置每行的间隙。

### grid-gap
可以同时设置行列的gap，在行之间引入10px间隙，在列之间引入20px间隙：
```grid-gap: 10px 20px;```

### grid-column
到目前为止，所讨论的所有属性都是针对网格容器的。 grid-column属性是第一个用于网格项本身的属性。
创建网格的假设水平和垂直线称为线。这些线在网格的左上角从1开始编号，向右移动列，向下移动行，向上计数。

要控制项目将使用的列数，您可以将grid-column属性与您希望项目开始和停止的行号一起使用，这将使项目从左侧网格的第一个垂直线开始，并跨越到网格的第3行，消耗该行的第一个和第二个格子：
```grid-column: 1 / 3;```
消耗第二个和第三个：
```grid-column: 2 / 4;```

### grid-row
当然，您可以像使用列一样使项目消耗多行。您可以使用网格项上的网格行属性定义项目开始和停止的水平线。

### grid-column-start
 单元格从第几个格子开始。

### grid-column-end
* 不设置的默认情况是只占一格子,
* 设置的情况意思是到第几格结束,
* 可以为负值，意味着该行的倒数第几个结束
* 可以使用span关键字根据所需的列宽定义网格项，而不是根据网格线的起始位置和结束位置定义网格项。请记住，跨度仅适用于正值。  grid-column-end: span 2;

### justify-self
使用justify-self水平对齐项目。在CSS Grid中，每个项目的内容位于一个称为单元格的框中。您可以使用网格项上的justify-self属性水平对齐内容在其单元格中的位置。默认情况下，此属性的值为stretch，这将使内容填充单元格的整个宽度。此CSS Grid属性也接受其他值：

* stretch: 使内容填充单元格的整个宽度
* start：对齐单元格左侧的内容
* center：对齐单元格中心的内容 
* end：对齐单元格右侧的内容

### align-self
使用align-self垂直对齐项目。使用类似于justify-self

### justify-items
使用对齐项目水平对齐所有项目。有时您希望CSS Grid中的所有项目共享相同的对齐方式。您可以使用以前学过的属性并单独对齐它们，也可以使用网格容器上的justify-items将它们水平对齐。

### align-items
使用网格容器上的align-items属性将为网格中的所有项目设置垂直对齐方式。

### grid-template-areas
您可以将网格的单元格组合到一个区域中，并为该区域指定一个自定义名称。通过在容器上使用grid-template-areas来执行此操作,代码中的每个单词代表一个单元格，每对引号代表一行。 除自定义标签外，您还可以使用句点（.）指定网格中的空单元格。
前三个单元格合并为一个名为header的区域，将底部三个单元格合并为一个页脚区域，并在中间行中生成两个区域;广告和内容。如下所示：
`grid-template-areas:
  "header header header"
  "advert content content"
  "footer footer footer";`
  
  
### grid-area 配合 grid-template-areas使用
为网格容器创建区域模板后，如上一个所示，您可以通过引用您提供的名称将项目放在自定义区域中。为此，您可以在项目上使用grid-area属性，如下所示：
`.item1 { grid-area: header; }`
这使网格知道您希望item1类进入名为header的区域。在这种情况下，该项将使用整个顶行，因为整行被命名为标题区域。

### 单独使用grid-area
如果您的网格没有要引用的区域模板，您可以动态创建一个区域，以便放置一个项目，如下所示：
`item1 { grid-area: 1/1/2/4; }`
这是使用您之前了解的行号来定义此项目的区域。上例中的数字代表以下值：
`grid-area: horizontal line to start at / vertical line to start at / horizontal line to end at / vertical line to end at;`
解读：示例中的项目将使用第1行和第2行之间的行以及第1行和第4行之间的行。
  
  
### 使用media查询 
通过使用媒体查询重新排列网格区域，更改网格的尺寸以及重新排列项目的位置，CSS网格可以轻松地使您的网站更具响应性。

### 在Grids中使用Grids
可以在子元素中使用Grids来实现复杂的布局


