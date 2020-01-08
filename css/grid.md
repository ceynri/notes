---
title: "Grid 布局教程"
date: "2020-01-08"
---

# Grid 布局教程

CSS Grid 布局系统是一个比较新的布局方式，它借鉴了表格布局的思想，将网页划分为不同的网格，实现网页的**二维布局**效果。它和 Flex 布局有点像，但较为明显的区别是，Flex 布局往往应用于一维层次的布局（轴线布局），没有 Grid 那么强的灵活性。

<img width="100%" src="https://www.wangbase.com/blogimg/asset/201903/1_bg2019032501.png">

这样的特性决定了 Grid 布局往往被应用于网页的大框架的划分而 Flex 布局更适合应用于小部件的排列，两者并不会有太大的地位冲突，应该结合起来使用。

Grid 布局更加贴近设计稿中的布局规划，它的出现得以使前端从各式各样的 hack 与 trick 中解放出来，使代码更加明确而简洁。

越来越多的页面将会使用 Grid 布局，哪怕旧浏览器上不的支持度较低，它也会随着时间逐渐发展成为 CSS 布局主流。

<br/>

## 属性速览

- **容器**
  - [grid](#grid) 网格
    - [grid-template](#grid-template) 定义网格、区域
      - [grid-template-rows](#grid-template-rows) 网格行高
      - [grid-template-columns](#grid-template-columns) 网格列宽
      - [grid-template-areas](#grid-template-areas) 区域
    - [grid-gap](#grid-gap) 单元格间距
      - [grid-row-gap](#grid-row-gap) 行间距
      - [grid-column-gap](#grid-column-gap) 列间距
    - [grid-auto-rows](#grid-auto-rows) 默认行高
    - [grid-auto-columns](#grid-auto-columns) 默认列宽
    - [grid-auto-flow](#grid-auto-flow) 流动方式
  - [place-items](#place-items) 对齐方式
    - [justify-items](#justify-items) 水平对齐
    - [align-items](#align-items) 垂直对齐
  - [place-content](#place-content) 分布方式
    - [justify-content](#justify-content) 水平分布
    - [align-content](#align-content) 垂直分布

- **项目**
  - [grid-area](#grid-area) 所在网格区域
    - [grid-column](#grid-column) 列定位
      - [grid-column-start](#grid-column-start) 列起始网格线
      - [grid-column-end](#grid-column-end) 列结束网格线
    - [grid-row](#grid-row) 行定位
      - [grid-row-start](#grid-row-start) 行起始网格线
      - [grid-row-end](#grid-row-end) 行结束网格线
  - [place-self](#place-self) 单独设置对齐方式
    - [justify-self](#justify-self) 单独设置水平对齐方式
    - [align-self](#align-self) 单独设置垂直对齐方式

- 其他
  - [fr](#fr) 相对单位
  - [repeat()](#repeat) 简写重复参数
    - [auto-fill 关键字](#auto-fill-关键字) 自动扩充单元格
  - [minmax()](#minmax) 区间限制
  - [span 关键字](#span-关键字) 跨越单元格

<br/>

## 基本概念

与 Flex 布局类似的，Grid 布局也有“**容器**”（container）和“**项目**”（item）的概念，以便于我们称呼被排版的元素们。

使用`display: grid;`语句，可以为指定容器应用 Grid 布局。

同样的，grid 默认为块级元素。指定为`inline-grid`属性，容器自身会表现为内联元素（并不影响项目的布局）。

外层的容器相当于框架，可以使用**网格线**（grid line）将其划分出多个**行**（row）与**列**（column），被划分出来的网格被称为**单元格**（cell）。

项目可以放在一个单元格里，也可以占有多个单元格。

<br/>

## 容器属性

### grid-template-rows
### grid-template-columns

这两个属性分别用于定义：每一行的高度、每一列的宽度。

#### px 单位

```css
.container {
  display: grid;    /* 以下代码示例省略该行 */
  grid-template-rows: 120px 60px;
  grid-template-columns: 60px 60px 60px;
}
```

以上代码创建了一个两行三列的网格。

```example
-------------
|   |   |   |
|   |   |   |
-------------
|   |   |   |
-------------
```

<br/>

#### % 单位

如果容器定义了 width 与 height，可以使用百分比作为行与列的宽度。

```css
.container {
  width: 192px;
  height: 192px;
  grid-template-rows: 66.7% 33.3%;
  grid-template-columns: 33.3% 33.3% 33.3%;
}
```

<br/>

#### auto 关键字

在设置长度时使用`auto`关键字，代表让浏览器决定该值，它会尽可能地取得不小于`min-width`的最大值。

```css
.container {
  grid-template-columns: 60px auto 60px;
}
```

<br/>

#### fr

`fr`关键字意为“片段”（fraction），是一种相对单位，比如`2fr`是`1fr`的两倍。

```css
.container {
  grid-template-rows: 2fr 1fr;
}
```

也可以和绝对单位进行混用，实现更多的布局效果。

<br/>

#### repeat()

使用`repeat()`函数，可以简化重复值。

```css
.container {
  grid-template-rows: 66.7% 33.3%;
  grid-template-columns: repeat(3, 33.33%);
}
```

<br/>

#### auto-fill 关键字

当单元格大小确定而容器大小不确定时，可以在`repeat()`中使用`auto-fill`关键字，使自动填充尽可能多的单元格。

```css
.container {
  grid-template-rows: 66.7% 33.3%;
  grid-template-columns: repeat(auto-fill, 60px);
}
```

<br/>

#### minmax()

生成一个区间，将长度限制在这个范围中。

```css
.container {
  grid-template-columns: 1fr 1fr minmax(30px, 1fr);
}
```

<br/>

#### 为网格线取名

如果后面需要以网格线为准进行引用，可以在`grid-template-rows`和`grid-template-columns`属性内使用方括号为网格线命名。

```css
.container {
  grid-template-rows: [r1] 120px [r2] auto [r3];
  grid-template-columns: [c1] 60px [c2] 60px [c3] auto [c4];
}
```

```example
    c1  c2  c3  c4
r1  -------------
    |   |   |   |
    |   |   |   |
r2  -------------
    |   |   |   |
r3  -------------
```

<br/>

### grid-template-areas

和定义网格线类似的，Grid 布局支持定义单元格组成的区域，属于同一区域的单元格设置相同的名字。

```css
.container {
  grid-template-columns: 60px 60px 60px;
  grid-template-rows: 60px 60px 60px;
  grid-template-areas: 'a a b'
                       'a a b'
                       'c d e';
}
```

则有类似下面的布局：

```example
-------------
|   a   | b |
|       |   |
-------------
| c | d | e |
-------------
```

如果有某区域不需要，则用点（`.`）表示。

> **⚠ 注意**：区域的命名会影响到网格线的名称。每个区域的起始网格线，会自动命名为`区域名-start`，终止网格线自动命名为`区域名-end`。

<br/>

---

### grid-row-gap
### grid-column-gap

`grid-row-gap`属性设置行与行的间隔（行间距），`grid-column-gap`属性设置列与列的间隔（列间距）。

```css
.container {
  grid-row-gap: 16px;
  grid-column-gap: 8px;
}
```

<br/>

### grid-gap

`grid-gap`属性为`grid-column-gap`和`grid-row-gap`的合并简写形式，其语法如下：

```grammar
grid-gap: <grid-row-gap>[ <grid-column-gap>];
```

省略第二个值时，默认都等于第一个值。（后面出现的双值可省略一值的情况都是这种处理方式）

> 最新标准中，`gap`相关属性去掉了`grid-`前缀，可以使用`row-gap`代替`grid-row-gap`。为了兼容性，仍然支持使用`grid-`前缀作为属性名。

<br/>

---

### grid-auto-flow

类似于 Flex 布局里的`flex-flow`，设置项目在网格中的放置顺序与方式。

```grammar
grid-auto-flow: (row | column) [dense];
```

默认值为`row`，即横向优先顺序填充。设置为`column`，则变成竖向优先顺序填充。

但如果排在前面的项目较大而后面的项目较小，可能会出现以下情况：

<div align="center">
  <img height="200px" src="https://www.wangbase.com/blogimg/asset/201903/bg2019032513.png" />
</div>

如果加上`dense`，则会采用尽量填满所有空单元格的方案。

<div align="center">
  <img height="200px" src="https://www.wangbase.com/blogimg/asset/201903/bg2019032514.png" />
</div>

<br/>

---

### grid-auto-rows
### grid-auto-columns

虽然使用 Grid 布局时，我们会规定好行列数，但如果想要添加更多行或列，或添加元素到超出规定的行列区域之外的区域时，Grid 会自动为我们生成新的行与列，而行高与列宽则通过`grid-auto-rows`和`grid-auto-columns`进行设置。

[例子](https://jsbin.com/sayuric/edit?css,output)：

```css
.container {
  grid-template-columns: 60px 60px 60px;
  grid-template-rows: 60px 60px 60px;
  grid-auto-rows: 30px; 
}
```

令8和9元素插入到网格之外，得到效果如下：

<div align="center">
  <img height="200px" src="https://www.wangbase.com/blogimg/asset/201903/bg2019032525.png" />
</div>

<br/>

---

### justify-items
### align-items

设置项目在容器区域内**水平对齐**与**垂直对齐**的方式，可以取四个值：

| 值                | 对齐方式                   |
| ----------------- | -------------------------- |
| start             | 对齐单元格的起始边缘       |
| end               | 对齐单元格的结束边缘       |
| center            | 单元格内部居中             |
| stretch（默认值） | 拉伸，占满单元格的整个宽度 |

<br/>

举个左对齐的例子：

```css
.container {
  justify-items: start;
}
```

<div align="center">
  <img width="400px" src="https://www.wangbase.com/blogimg/asset/201903/bg2019032516.png" />
</div>

### place-items

`place-items`即`justify-items`和`align-items`属性的合并简写属性。

```grammar
place-items: <align-items>[ <justify-items>];
```

<br/>

### justify-content
### align-content

`justify-content`属性设置按列分隔的内容区域在容器内的水平（左中右）排列分布方式。

`align-content`属性设置按行分隔的内容区域在容器内的垂直（上中下）排列分布方式。

两种属性都可取名字相同的七种值（下以`justify-content`为例）：

| 值              | 分布方式                               |
| --------------- | -------------------------------------- |
| start（默认值） | 靠左对齐                               |
| end             | 靠右对齐                               |
| center          | 居中                                   |
| stretch         | 拉伸占据整个网格容器                   |
| space-between   | 两端对齐，项目之间间隔相等             |
| space-around    | 每个项目两侧的间隔相等                 |
| space-evenly    | 项目与项目、项目与容器边框之间间隔相等 |

<br/>

每个值的效果如下：

<div align="center" 
     style="display: flex;
            flex-wrap: wrap;
            justify-content: space-around;
    ">
  <div>
    <img width="200px" src="https://www.wangbase.com/blogimg/asset/201903/bg2019032519.png" />
    <div>start</div><br/>
  </div>
  <div>
    <img width="200px" src="https://www.wangbase.com/blogimg/asset/201903/bg2019032518.png" />
    <div>end</div><br/>
  </div>
  <div>
    <img width="200px" src="https://www.wangbase.com/blogimg/asset/201903/bg2019032520.png" />
    <div>center</div><br/>
  </div>
  <div>
    <img width="200px" src="https://www.wangbase.com/blogimg/asset/201903/bg2019032521.png" />
    <div>stretch</div><br/>
  </div>
  <div>
    <img width="200px" src="https://www.wangbase.com/blogimg/asset/201903/bg2019032523.png" />
    <div>space-between</div><br/>
  </div>
  <div>
    <img width="200px" src="https://www.wangbase.com/blogimg/asset/201903/bg2019032522.png" />
    <div>space-around</div><br/>
  </div>
  <div>
    <img width="200px" src="https://www.wangbase.com/blogimg/asset/201903/bg2019032524.png" />
    <div>space-evenly</div><br/>
  </div>
</div>

### place-content

`place-content`属性是`align-content`属性和`justify-content`属性的合并简写形式。

```grammar
place-content: <align-content>[ <justify-content>];
```

<br/>

---

> **⚠注意**：以下合并简写属性合并过多的属性值，故不推荐使用，以提高可读性，便于记忆。

### grid-template

`grid-template`属性是：

- `grid-template-columns`
- `grid-template-rows`
- `grid-template-areas`

这三个属性的合并简写形式。

<br/>

### grid

`grid`属性是：

- `grid-template-rows`
- `grid-template-columns`
- `grid-template-areas`
- ` grid-auto-rows`
- `grid-auto-columns`
- `grid-auto-flow`

这六个属性的合并简写形式。

<br/>

<br/>

## 项目属性

### grid-column-start
### grid-column-end
### grid-row-start
### grid-row-end

这四个属性用于指定项目的边框应该定位到哪一条网格线上。

| 属性              | 对应网格线             |
| ----------------- | ---------------------- |
| grid-column-start | 左边框所在的垂直网格线 |
| grid-column-end   | 右边框所在的垂直网格线 |
| grid-row-start    | 上边框所在的水平网格线 |
| grid-row-end      | 下边框所在的水平网格线 |

<br/>

[例子](https://jsbin.com/yukobuf/edit?css,output)：

```css
.item-1 {
  grid-column-start: 2;
  grid-column-end: 4;
}
```

<div align="center">
  <img height="200px" src="https://www.wangbase.com/blogimg/asset/201903/bg2019032526.png" />
</div>

<br/>

#### `grid-row`与`grid-column`的不同之处

虽然由于没有设置`grid-auto-flow: dense;`，所以2排在1的后面，但如果对项目1指定了`grid-row`的话，则会使得项目1表现得类似`float`之于内联元素那样，离开了“网格流”，使得后面的元素会尝试填充项目1前面的单元格的空间。

[例子1](https://jsbin.com/celikuyuce/3/edit?html,css,output)：

```css
.item-1 {
  grid-column-start: 2;
  grid-column-end: 4;
  grid-row-start: 1;
  grid-row-end: 3;
}
```

<div align="center">
  <img height="200px" src="https://i.loli.net/2020/01/08/bFNzcaeLdVHnyTm.png" />
</div>

<br/>

[例子2](https://jsbin.com/celikuyuce/4/edit?html,css,output)：

```css
.item-5 {
  grid-column-start: 1;
}
```

<div align="center">
  <img height="200px" src="https://i.loli.net/2020/01/08/GNf6VlCvMIuT8Zw.png" />
</div>

<br/>

形象地说：

- 例子1中，`grid-row`可以顶掉他想定位到的网格的其他内容，而其他内容会绕着他像水流一样接着排列；
- 例子2中，如果只单独设置了`grid-column`，则会考虑先后顺序问题，不会超前于前面的元素，也不会让后面的元素排到自己的前面。

<br/>

#### 网格线名

另外，前面如果有给网格线取名，则可以使用网格线的名字来指定。

```css
.item-1 {
  grid-column-start: header-start;
  grid-column-end: header-end;
}
```

<br/>

#### span 关键字

`span`表示“跨越"，即左右边框（上下边框）之间跨越多少个网格。

```css
.item-1 {
  grid-column-end: span 2;
}
```

当没有指定其他时，等价于下面的写法：

```css
.item-1 {
  grid-column-start: span 2;
}
```

这两种写法都会让项目1占据单元格1和单元格2，它们的基准都是从start网格边往end方向跨越两格。

而下面这种写法比较容易看出区别：

```css
/* 以start边为基准跨越两格，占据单元格1、2 */
.item-1 {
  grid-column-start: 1;
  grid-column-end: span 2;
}

/* 以end边为基准反向跨越两格，占据单元格2、3 */
.item-1 {
  grid-column-start: span 2;
  grid-column-end: 4;
}
```

<br/>

### grid-column
### grid-row

- `grid-column`属性是`grid-column-start`和`grid-column-end`的合并简写形式
- `grid-row`属性是`grid-row-start`属性和`grid-row-end`的合并简写形式。

语法：

```grammar
grid-row: <row-start> / <row-end>;
grid-column: <column-start> / <column-end>;
```

其中第二个值是可选的，默认只跨越一个单元格。

<br/>

例子：

```css
.item-1 {
  grid-column: 1 / 3;
  grid-row: 1 / 2;
}
/* 等同于 */
.item-1 {
  grid-column-start: 1;
  grid-column-end: 3;
  grid-row-start: 1;
  grid-row-end: 2;
}
```

<br/>

### grid-area

`grid-area`属性指定项目放在哪一个区域。

```css
.item-1 {
  grid-area: header;
}
```

也可以当作`grid-row-start`、`grid-column-start`、`grid-row-end`、`grid-column-end`的合并简写属性：

```grammar
grid-area: <row-start> / <column-start> / <row-end> / <column-end>;
grid-area: <row-start> / <column-start> / <row-end>;
grid-area: <row-start> / <row-end>;
grid-area: <row-start>;
```

省略参数的表现形式类似于[边距的值复制](cheat-sheet.md#边距的值复制)，只不过参数顺序为顺时针。

<br/>

---

### justify-self
### align-self

为某一个项目单独设置水平/垂直对齐方式，即`justify-items`/`align-items`的单独版。

```css
.item {
  justify-self: start | end | center | stretch;
  align-self: start | end | center | stretch;
}
```

### place-self

`place-self`属性是`align-self`属性和`justify-self`属性的合并简写形式。

```grammar
place-self: <align-self>[ <justify-self>];
```

<br/>

<br/>

## 本文参考

> CSS Grid 网格布局教程 - 阮一峰 <http://www.ruanyifeng.com/blog/2019/03/grid-layout-tutorial.html>

<br/>
