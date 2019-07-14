# 了解一下 flex

###1、介绍
　　布局的传统解决方案，基于盒状模型，依赖 display属性 + position属性 + float属性。它对于那些特殊布局非常不方便，比如，垂直居中就不容易实现。2009年，W3C提出了一种新的方案—-Flex布局，可以简便、完整、响应式地实现各种页面布局。
flex（flexible box：弹性布局盒模型）。在webkit内核的浏览器中使用时，必须加上 `-webkit-`前缀。
使用flex布局的容器(flex container)，它内部的元素自动成为flex项目(flex item)。
容器默认存在两根轴：水平的主轴（main axis）和垂直的交叉轴（cross axis）。项目默认沿主轴排列。
注意：flex容器内元素，即`flex item`的float、clear、vertical-align属性将失效

### 2、容器属性
```
1：flex-direction
2：flex-wrap
3：flex-flow
4：justify-content
5：align-items
6：align-content
```
#### 2.1 `flex-direction`属性
　　决定主轴的方向，即项目排列的方向。有四个可选值：row(默认)|row-reverse|column|column-reverse
 - row（默认值）：主轴为水平方向，起点在左端
 - row-reverse：主轴为水平方向，起点在右端
 - column：主轴为垂直方向，起点在上沿
 - column-reverse：主轴为垂直方向，起点在下沿

#### 2.2 `flex wrap` 属性
　　默认情况下，item排列在一条直线上，flex-wrap决定当排列不下时是否换行以及换行的方式.
可选值有：nowrap(默认)|wrap|wrap-reverse
 - nowrap（默认）：不换行
 - wrap：换行，第一行在上方
 - wrap-reverse：换行，第一行在下方

#### 2.3 `justify-content`属性
　　justify-content属性定义了项目在主轴上的对齐方式。可选值有：flex-start | flex-end | center | space-between | space-around
 - flex-start（默认值）：左对齐
 - flex-end：右对齐
 - center： 居中
 - space-between：两端对齐，项目之间的间隔都相等
 - space-around：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍

#### 2.4 `align-items`属性
　　align-items属性定义项目在交叉轴上如何对齐。可选值有：flex-start | flex-end | center | baseline | stretch
 - flex-start：交叉轴的起点对齐
 - flex-end：交叉轴的终点对齐
 - center：交叉轴的中点对齐
 - baseline: 项目的第一行文字的基线对齐
 - stretch（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度

#### 2.5 `align-content`属性
　　align-content属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。可选值有：flex-start | flex-end | center | space-between | space-around | stretch
 - flex-start：与交叉轴的起点对齐
 - flex-end：与交叉轴的终点对齐
 - center：与交叉轴的中点对齐
 - space-between：与交叉轴两端对齐，轴线之间的间隔平均分布
 - space-around：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍
 - stretch（默认值）：轴线占满整个交叉轴

#### 2.6 `flex-flow` 属性
　　flex-flow属性是flex-direction属性和flex-wrap属性的简写形式，默认值为row nowrap。

### 3、`flex item` 属性
``` javascript
1：order
2：flex-grow
3：flex-shrink
4：flex-basis
5：flex
6：align-self
```

#### 3.1 `order` 属性
　　order属性定义项目的排列顺序。数值越小，排列越靠前，默认为0
#### 3.2 `flex-grow` 属性
　　flex-grow属性定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大
#### 3.3 `flex-shrink` 属性
　　flex-shrink属性定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小
#### 3.4 `flex-basis` 属性
　　flex-basis属性定义了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为auto，即项目的本来大小
#### 3.5 `flex` 属性
　　flex属性是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto。后两个属性可选
#### 3.6 `align-self` 属性
　　align-self属性允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch

**资料**
------------
[3分钟看懂flex布局](https://www.cnblogs.com/lixuemin/p/6110434.html)
