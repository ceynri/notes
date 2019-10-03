---
title: "Flex 布局教程"
date: "2019-10-03"
---

# Flex 布局教程

传统的网页布局解决方案都是采用盒状模型，但是在多个盒的存在相互影响或者想要达到比较特殊的布局效果时，盒状模型的布局实现就较为麻烦。

Flex 布局，即 **Flex**ible Box 布局（弹性布局），基于盒状模型提供了更大的灵活性。

## 基本概念

任何容器都可以通过设置`display: flex;`指定为 Flex 布局，被指定的容器称为“flex container”（简称**容器**），而它的子成员则会自动成为“flex item”（简称**项目**）。

容器存在两根轴：

- 主轴（main axis）默认为水平方向的轴。
- 交叉轴（cross axis）默认为垂直方向的轴。

项目沿主轴排列，主轴的方向可以改变。

一般来说，水平方向的轴的起点为容器的最左边，终点为最右边；垂直方向的轴的起点为容器的最上面，终点为最下面。

## 属性速览

- **容器**
  - flex-flow
    - flex-direction 排列方向
    - flex-wrap 换行方式
  - justify-content 水平对齐
  - align-items 垂直对齐
  - align-content 垂直排列分布

- **项目**
  - order 顺序
  - flex
    - flex-grow 占领剩余空间的比例
    - flex-shrink 缩小自身时的比例
    - flex-basis 界定是否换行的宽度
  - align-self 特立独行的对齐方式

<br/>

## 容器属性

### flex-direction

`flex-direction`属性决定项目的**排列方向**（即主轴的方向）。

| 值             | 排列方向 |
| -------------- | -------- |
| row（默认值）  | →        |
| row-reverse    | ←        |
| column         | ↓        |
| column-reverse | ↑        |

```
# row
① ② ③

# row-reverse
③ ② ①

# column
①
②
③

# column-reverse
③
②
①
```

<br/>

### flex-wrap

wrap 即换行，该属性指定项目一行塞不下时如何**换行**。

| 值               | 方式                             |
| ---------------- | -------------------------------- |
| nowrap（默认值） | 不换行，互相压缩一下             |
| wrap             | 正常的换行，优先填满主轴前面的行 |
| wrap-reverse     | 反着换行，从主轴底下开始往上换行 |

```
# nowrap
|①②③④⑤⑥⑦⑧⑨⑩|

# wrap
|① ② ③ ④ ⑤ ⑥|
|⑦ ⑧ ⑨ ⑩    |

# wrap-reverse
|⑦ ⑧ ⑨ ⑩    |
|① ② ③ ④ ⑤ ⑥|
```

<br/>

### flex-flow

是`flex-direction`和`flex-wrap`的简写形式。

```css
.box {
  flex-flow: <flex-direction> <flex-wrap>;
}
```

<br/>

### justify-content

定义了项目在**主轴**上的**对齐方式**。

| 值                   | 对齐方式                    |
| -------------------- | --------------------------- |
| flex-start（默认值） | 左对齐                      |
| flex-end             | 右对齐                      |
| center               | 居中                        |
| space-between        | 两端对齐，项目之间间隔相等 |
| space-around         | 每个项目两侧的间隔相等    |

```
# flex-start
|①②③      |

# flex-end
|      ①②③|

# center
|   ①②③   |

# space-between
|①   ②   ③|

# space-around
| ①  ②  ③ |
```

其中：

- `space-between`使最靠边的项目会紧贴容器，项目之间间隔相等；
- 而`space-around`则是每个项目左右边距相等，所以“项目之间的间隔”为“项目与边框之间的间隔”的两倍。

<br/>

### align-items

设置项目在**交叉轴**上的**对齐方式**。

| 值                | 对齐方式                                        |
| ----------------- | ----------------------------------------------- |
| flex-start        | 交叉轴的起点对齐                                |
| flex-end          | 交叉轴的终点对齐                                |
| center            | 交叉轴的中点对齐                                |
| baseline          |项目的第一行文字的基线对齐                     |
| stretch（默认值） | 占满整个容器的高度（项目未设置高度或设为auto） |

样例：（如果显示效果有问题则为 markdown 编辑器支持不佳）

<div class="flex">
  <div>
    <div class="flex align-items flex-start">
      <div class="block">1</div>
      <div class="block xl">2</div>
      <div class="block">3</div>
      <div class="block l">4</div>
    </div>
    <p class="figure-title">flex-start</p>
  </div>
  <div>
    <div class="flex align-items flex-end">
      <div class="block">1</div>
      <div class="block xl">2</div>
      <div class="block">3</div>
      <div class="block l">4</div>
    </div>
    <p class="figure-title">flex-end</p>
  </div>
  <div>
    <div class="flex align-items center">
      <div class="block">1</div>
      <div class="block xl">2</div>
      <div class="block">3</div>
      <div class="block l">4</div>
    </div>
    <p class="figure-title">center</p>
  </div>
  <div>
    <div class="flex align-items baseline">
      <div class="block"><u>1</u></div>
      <div class="block xl sink"><u>2</u></div>
      <div class="block"><u>3</u></div>
      <div class="block xxl sink"><u>4</u></div>
    </div>
    <p class="figure-title">baseline</p>
  </div>
  <div>
    <div class="flex align-items stretch">
      <div class="block nosize">1</div>
      <div class="block nosize xl">2</div>
      <div class="block nosize">3</div>
      <div class="block nosize l">4</div>
    </div>
    <p class="figure-title">stretch</p>
  </div>
</div>

<br/>

### align-content

定义了**多根主轴线**之间的**排列分布方式**（注意与 align-items 属性的区别）。

假设交叉轴为从上到下方向：

| 值                | 对齐方式                             |
| ----------------- | ------------------------------------ |
| flex-start        | 向上靠（向交叉轴起点对齐）           |
| flex-end          | 向下靠（向交叉轴终点对齐）           |
| center            | 往中间靠（与交叉轴的中点对齐）       |
| space-between     | 与交叉轴两端对齐，轴线之间的间隔相等 |
| space-around      | 每根轴线两侧的间隔都相等             |
| stretch（默认值） | 轴线们上下拉伸占满整个交叉轴         |

注：如果项目只有一根轴线，该属性不起作用。

样例：

<div class="flex">
  <div>
    <div class="flex align-content flex-start">
      <div class="line-block l"></div>
      <div class="line-block xl"></div>
      <div class="line-block"></div>
      <div class="line-block l"></div>
      <div class="line-block xxl"></div>
      <div class="line-block xl"></div>
      <div class="line-block"></div>
      <div class="line-block l"></div>
      <div class="line-block"></div>
    </div>
    <p class="figure-title">flex-start</p>
  </div>
  <div>
    <div class="flex align-content flex-end">
      <div class="line-block l"></div>
      <div class="line-block xl"></div>
      <div class="line-block"></div>
      <div class="line-block l"></div>
      <div class="line-block xxl"></div>
      <div class="line-block xl"></div>
      <div class="line-block"></div>
      <div class="line-block l"></div>
      <div class="line-block"></div>
    </div>
    <p class="figure-title">flex-end</p>
  </div>
  <div>
    <div class="flex align-content center">
      <div class="line-block l"></div>
      <div class="line-block xl"></div>
      <div class="line-block"></div>
      <div class="line-block l"></div>
      <div class="line-block xxl"></div>
      <div class="line-block xl"></div>
      <div class="line-block"></div>
      <div class="line-block l"></div>
      <div class="line-block"></div>
    </div>
    <p class="figure-title">center</p>
  </div>
  <div>
    <div class="flex align-content space-between">
      <div class="line-block l"></div>
      <div class="line-block xl"></div>
      <div class="line-block"></div>
      <div class="line-block l"></div>
      <div class="line-block xxl"></div>
      <div class="line-block xl"></div>
      <div class="line-block"></div>
      <div class="line-block l"></div>
      <div class="line-block"></div>
    </div>
    <p class="figure-title">space-between</p>
  </div>
  <div>
    <div class="flex align-content space-around">
      <div class="line-block l"></div>
      <div class="line-block xl"></div>
      <div class="line-block"></div>
      <div class="line-block l"></div>
      <div class="line-block xxl"></div>
      <div class="line-block xl"></div>
      <div class="line-block"></div>
      <div class="line-block l"></div>
      <div class="line-block"></div>
    </div>
    <p class="figure-title">space-around</p>
  </div>
  <div>
    <div class="flex align-content stretch">
      <div class="line-block no-height l"></div>
      <div class="line-block no-height xl"></div>
      <div class="line-block no-height"></div>
      <div class="line-block no-height l"></div>
      <div class="line-block no-height xxl"></div>
      <div class="line-block no-height xl"></div>
      <div class="line-block no-height"></div>
      <div class="line-block no-height l"></div>
      <div class="line-block no-height"></div>
    </div>
    <p class="figure-title">stretch</p>
  </div>
</div>

<br/>

## item 属性

### order

类似于`z-index`，定义项目的排列顺序。数值越小，排列越靠前，默认为`0`，可为负值。

```
# example
|[-1 ] [ 0 ] [ 1 ] [ 1 ] [ 3 ]|
|[ 8 ] [999] [999]            |
```

<br/>

### flex-grow

定义项目的放大比例等级，默认值为`0`（默认如果存在剩余空间，也不放大）。

`flex-grow`作用的对象是**剩余**空间，所以当元素分配了一定宽度的时候，不同大小的`flex-grow`看起来并不按比例分配整个空间。

如果需要几个元素按照你期望的比例占据某个区域，则可以给每个元素设置`width: 0`，然后再分配`flex-grow`。

```
# example1
|[ 0 ][ 0 ][ 0 ]      |

# example2
|[  1  ][  1  ][  1  ]|

# example3
|[ 1 ][    2    ][ 1 ]|
```

<br/>

### flex-shrink

定义项目的缩小比例等级，默认值为`1`（默认如果空间不足，该项目将缩小）。

当`flex-shrink`值为`0`时，即使空间不足该项目也不会缩小。

```
# example
|[ 1 ][ 1 ][ 1 ][ 1 ]|
|[1][ 0 ][1][1][1][1]|
```

<br/>

### flex-basis

定义了在分配多余空间之前，项目占据的主轴空间。默认值为`auto`（项目的本来大小）。

浏览器根据这个属性，计算主轴是否有多余空间，来决定是否换行。

值可以是单位或者百分数。

**与`width`的区别：**

flex 布局是有弹性的，你可以设置弹性使得即使主轴空间即使小于项目们加起来的宽度也能通过压缩 width 放入同一行。

故`flex-basis`与`flex-wrap`经常一起使用：

- 当设置为`nowrap`时，`flex-basis`通常没什么作用；
- 当启用`wrap`时，你可以允许压缩一定的`width`而不超过`flex-basis`值，或者加宽`width`哪怕原本一行可以塞得下更多项目。

> 参考：<https://blog.csdn.net/lmmxxoo/article/details/83094818>

<br/>

### flex

`flex`属性是`flex-grow`、`flex-shrink`和`flex-basis`的简写。

默认值`0 1 auto`，后两个属性可选。

该属性有两个快捷值：`auto`（`1 1 auto`） 和`none`（`0 0 auto`）。

> 建议优先使用这个属性，而不是单独写三个分离的属性，因为浏览器会推算相关值。

<br/>

### align-self

`align-self`属性允许单个项目与其他项目有不一样的对齐方式，即“覆盖`align-items`属性”。

默认值`auto`，表示继承父元素的`align-items`属性。如果没有父元素，则等同于`stretch`。

```
            # example
flex-start  |[a] [bb]     [ddd]|  default
            |                  |
flex-end ---|-------> [c]      |  align-self
```

<br/>

## 其他

Webkit 内核的浏览器，必须加上`-webkit`前缀。

```css
.box {
  display: -webkit-flex; /* Safari */
  display: flex;
}
```

<br/>

## 本文参考

- [Flex 布局教程：语法篇 - 阮一峰的网络日志](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)

<!-- 本文用到的样式 -->

<head>
  <link rel="stylesheet" href="ref-css/flex.css">
</head>
