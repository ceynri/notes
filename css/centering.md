---
title: "CSS 居中专项讲解"
date: "2019/10/04"
---

# CSS 居中专项讲解

对于 CSS 新手来说，**居中效果**绝对是能排上前几的新手常见难题。

对于不同类型的元素的性质认识不够深刻，又常常在搜索解决方法时没能准确描述自己想要居中的元素的类型，导致出现诸如文本对齐的方法用在块元素上的错误。

关于居中的属性实在不算少，故分清不同情况来设置不同的属性是非常重要的一步。

## 内容预览 <!-- omit in toc -->

按情景分类：

- [水平居中](#水平居中)
  - [内联元素](#内联元素)
  - [块元素](#块元素)
  - [多个内联块元素](#多个内联块元素)
- [垂直居中](#垂直居中)
  - [内联元素](#内联元素-1)
  - [块元素](#块元素-1)
  - [多个元素](#多个元素)
  - [在行中](#在行中)
- [水平垂直居中](#水平垂直居中)

按方法分类：

- 水平居中
  - text-align
  - auto-margin
  - [flex] justify-content
- 垂直居中
  - padding
  - line-height
  - absolute & -margin | transform
  - [flex] & auto-margin
  - [flex] align-item
  - [flex] flex-direction & justify-content
  - [flex] align-content (wrap)
  - [table-cell] vertical-align: middle
- 水平垂直居中
  - [grid] auto margin

<br/>

> **关于显示问题**😥
>
> 一些对于在 markdown 内嵌 HTML 支持较差的编辑器（如 github）会影响本文示例的正常显示，建议[点击此处](https://ceynri.github.io/notes/css/centering.html)阅读本文。

> ⚠ 文中所列出的 CSS 样式并非效果的所有样式，如发现实现的效果有出入可以直接<kbd>右键</kbd>查看本页面对应示例的源码（示例的样式全部内嵌于HTML标签中）。

## 水平居中

### 内联元素

文本、inline-block、inline-table 等等都可以使用`text-align: center`的方法居中。

```css
.center-text {
    text-align: center;
}
```

效果：
<div style="border: 1px dotted">
    <p style="text-align: center;">centered text</p>
</div>
<br/>

### 块元素

通过 margin 设置左右外边距为`auto`，浏览器会自动均分左右剩余的空间给元素的左右外边距，从而很好的解决有固定`width`的块元素的居中问题。

```css
.center-block {
    margin: 0 auto;
}
```

效果：
<div style="border: 1px dotted">
<div style="
    width: 120px;
    height: 60px;
    background: #fa0;
    color: #000;
    margin: 0 auto;
    "></div>
</div>

<br/>

### 多个内联块元素

将他们用\<div>包裹起来，然后设置如下对齐方式（二选一）：

```css
/* 内联块方法 */
.inline-block-center {
    text-align: center;
}

.inline-block-center div {
    display: inline-block;
    text-align: left;
}

/* Flex盒子方法 */
.flex-center {
    display: flex;
    justify-content: center;
}
```

效果：
<div style="border: 1px dotted">
    <div style="text-align: center; font-size: 0;">
        <div style="
            display: inline-block;
            text-align: left;
            width: 60px;
            height: 60px;
            margin: 4px;
            background: #fa0;
            "></div>
        <div style="
            display: inline-block;
            text-align: left;
            width: 60px;
            height: 80px;
            margin: 4px;
            background: #fa0;
            "></div>
        <div style="
            display: inline-block;
            text-align: left;
            width: 60px;
            height: 70px;
            margin: 4px;
            background: #fa0;
            "></div>
    </div>
</div>
<p style="text-align: center; margin: 0 0 24px;">inline block</p>

<div style="border: 1px dotted">
    <div style="display: flex; justify-content: center;">
        <div style="
            width: 60px;
            height: 80px;
            margin: 4px;
            background: #fa0;
            "></div>
        <div style="
            width: 60px;
            height: 80px;
            margin: 4px;
            background: #fa0;
            "></div>
        <div style="
            width: 60px;
            height: 80px;
            margin: 4px;
            background: #fa0;
            "></div>
    </div>
</div>
<p style="text-align: center; margin: 0 0 24px;">flexbox（默认自动拉伸）</p>

<br/>

## 垂直居中

### 内联元素

- 如果父元素没有设置固定宽高，则父元素设置相同上下`padding`即可；
- 稍微“trick”一点的，可以设置父元素的行高属性`line-height`与`height`相同（如果父元素没有`height`的话就不用设置了）。

```css
/* padding */
.link {
    padding: 40px 0;
}

/* line-height */
.center-text-trick {
    line-height: 110px; 
    /* 设置nowarp避免尺寸问题导致换行破坏样式 */
    white-space: nowrap;
    overflow: hidden;
}
```

效果：

<div style="
    padding: 40px 12px;
    border: 1px dotted;
    ">
    <span>用padding来撑起垂直居中</span>
</div>

<br/>

<div style="
    line-height: 110px;
    padding: 0 12px;
    white-space: nowrap;
    overflow: hidden;
    border: 1px dotted;
    ">
    <span>用line-height的方法垂直居中</span>
</div>

line-height 方法存在的小问题就是用鼠标去划取选中文字时能够看到不太正常的行高，但有的时候（比如一个\<a>链接按钮）能够提供更大的选中范围，利于操作。

<br/>

### 块元素

如果不想使用 flexbox 的方法，可以用**定位+移位**的方法实现垂直居中：

```css
/* 
 * 父元素需要设置为relative是因为子元素的absolute定位
 * 是相对于最亲的非static定位的父元素来进行定位的
 */
.parent {
    position: relative;
}

.child {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
}
```

效果：
<div style="height: 120px; border: 1px dotted; position: relative;">
    <div style="height: 40px; width: 60px; background: #fa0; position: absolute; top: 50%; transform: translateY(-50%);"></div>
</div>

<br/>

如果你知道子元素的高度，可以直接使用设置**负值margin**的方法。（可能会牺牲普适性提高一点点渲染速度吧）

```css
child {
    height: 100px;
    padding: 20px;
    position: absolute;
    top: 50%;
    margin: -70px 0 0;
}
```

效果就不演示了🐟

<br/>

配合 **flex 布局**设置`margin: auto`实现（垂直）居中也是一种非常简单有效的方法。

```css
.parent {
    display: flex;
}

.margin-center {
    margin: auto 0;
}
```

效果：
<div style="height: 120px; border: 1px dotted; display: flex;">
    <div style="height: 40px; width: 60px; background: #fa0; margin: auto 0;">
    </div>
</div>

<br/>

当然，下面 [多个元素](#多个元素) 小节介绍的方法大多也可以应用于单个块元素上。

> 还有一种利用 CSS table-cell 的 trick，可以使用`vertical-align: center`垂直居中。介于不太符合一般情况下的语义环境故不介绍了。

<br/>

### 多个元素

对于多个内联元素来说，设置相同的上下`padding`仍然是个不错的办法，但如果不合适或者是块元素的话，可以试试使用 flexbox。

多个（区块）元素**垂直方向堆积**的方法：

```css
.flex-center-vertically {
    display: flex;
    /* 设置主轴为竖向 */
    flex-direction: column;
    /* 主轴方向居中 */
    justify-content: center;
}
```

效果：（每个元素被点框框起来以易于区分）
<div style="
    height: 300px;
    max-width: 1000px;
    padding: 12px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    background: #21252b;
    color: #ccc;
    ">
    <span style="border: 1px dotted #ccc; background: #282c34;">one</span>
    <span style="border: 1px dotted #ccc; background: #282c34;">two</span>
    <span style="border: 1px dotted #ccc; background: #282c34;">three</span>
    <span style="border: 1px dotted #ccc; background: #282c34;">Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</span>
    <span style="border: 1px dotted #ccc; background: #282c34;"> Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. </span>
    <span style="border: 1px dotted #ccc; background: #282c34;">Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.</span>
</div>

<br/>

多个元素时往**水平堆积**的方法：

```css
.flex-center-vertically {
    display: flex;
    /* 交叉轴方向（垂直方向）居中 */
    align-item: center;
}
```

<div style="
    height: 300px;
    max-width: 1000px;
    padding: 12px;
    display: flex;
    align-items: center;
    background: #21252b;
    color: #ccc;
    ">
    <span style="border: 1px dotted #ccc; background: #282c34;">one</span>
    <span style="border: 1px dotted #ccc; background: #282c34;">two</span>
    <span style="border: 1px dotted #ccc; background: #282c34;">three</span>
    <span style="border: 1px dotted #ccc; background: #282c34;">Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</span>
    <span style="border: 1px dotted #ccc; background: #282c34;"> Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. </span>
    <span style="border: 1px dotted #ccc; background: #282c34;">Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.</span>
</div>

<br/>

此外，对于多个内联元素，如果其拥有多个主轴线（**多行**），那么可以使用`align-content`来垂直居中：

```css
.flex-center-vertically {
    display: flex;
    align-content: center;
    flex-wrap: wrap;
}
```

<div style="
    height: 300px;
    max-width: 1000px;
    padding: 12px;
    display: flex;
    align-content: center;
    flex-wrap: wrap;
    background: #21252b;
    color: #ccc;
    ">
    <span style="border: 1px dotted #ccc; background: #282c34;">one</span>
    <span style="border: 1px dotted #ccc; background: #282c34;">two</span>
    <span style="border: 1px dotted #ccc; background: #282c34;">three</span>
    <span style="border: 1px dotted #ccc; background: #282c34;">Lorem ipsum dolor sit amet,</span>
    <span style="border: 1px dotted #ccc; background: #282c34;">consectetur adipisicing elit,</span>
    <span style="border: 1px dotted #ccc; background: #282c34;">sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</span>
    <span style="border: 1px dotted #ccc; background: #282c34;">Ut enim ad minim veniam,</span>
    <span style="border: 1px dotted #ccc; background: #282c34;">quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.</span>
    <span style="border: 1px dotted #ccc; background: #282c34;">Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.</span>
</div>

<br/>

### 在行中

`vertical-align`属性虽然也是关于内联元素的垂直居中的属性，但`vertical-align: middle;`的作用效果是“该元素在它所在的那一行以垂直中间为基准对齐”。

```css
span {
    display: inline-block;
    vertical-align: middle;
}
```

效果：
<div style="border: 1px dotted;">
    <p>
        这是一个位于段落中的<span style="display: inline-block; vertical-align: middle;background: #fa0; width:40px; height: 40px;"></span>橙色方块。
    </p>
</div>
<br/>

由此可以引申出关于在父元素内垂直居中还有一种奇淫技巧——“ghost element”（了解即可）

```css
.ghost-center {
    position: relative;
}

/* 创建一个看不见的、与父元素登高的垂直居中元素 */
.ghost-center::before {
    content: "";
    display: inline-block;
    height: 100%;
    vertical-align: middle;
}

.ghost-center p {
    display: inline-block;
    vertical-align: middle;
    /* 需要设置 width */
}
```

效果：

<div style="position: relative; background: #21252b; color: #ccc; height: 160px; max-width:1000px;">
    <div style="
        height: 100%;
        width: 0px;
        display: inline-block;
        vertical-align: middle;
    "></div><p style="
        display: inline-block;
        vertical-align: middle;
        max-width: 1000px;
        border: 1px dotted #ccc;
        background: #282c34;
        ">Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
    </p>
</div>

<br/>

## 水平垂直居中

这就可以将前面两节的内容配合起来使用了，根据不同的情况、语境还有个人习惯选择不同的方法。

例如对于这个例子：

```css
.parent {
    position: relative;
}

.child {
    width: 300px;
    height: 100px;
    padding: 20px;
}
```

可以...

```css
/* 负margin方法 */
.child {
    position: absolute;
    top: 50%;
    left: 50%;
    margin: -70px 0 0 -170px;
}

/* transform方法 */
.child {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}

/* flexbox方法 */
.parent {
    display: flex;
    justify-content: center;
    align-items: center;
}

/* flex + margin方法（仅对于单元素） */
.parent {
    display: flex;
}
.child {
    margin: auto;
}
```

还有一种非常好用的布局方法 —— **Grid 布局**，在“二维布局”的情况下要比“一维”的 Flex 布局要更加好用：

```css
.parent {
    display: grid;
}

.child {
    margin: auto;
}
```

样例：

```html
<style>
.parent {
    display: grid;
    height: 200px;
    width: 300px;
    background: #21252b;
}

.child {
    margin: auto;
}

.marked {
    border: 1px dotted #ccc;
    background: #282c34;
}
</style>

<div class="parent">
    <div class="child">
        <span class="marked">I'm centered!</span>
        <span class="marked">I'm centered!</span>
        <p class="marked">I'm centered!</p>
  </div>
</div>
```

效果：
<div style="display: grid; height: 200px; background: #21252b; color: #ccc;">
    <div style="margin: auto;">
        <span style="border: 1px dotted #ccc; background: #282c34;">I'm centered!</span>
        <span style="border: 1px dotted #ccc; background: #282c34;">I'm centered!</span>
        <p style="border: 1px dotted #ccc; background: #282c34;">I'm centered block!</p>
  </div>
</div>

<br/>

## 总结 <!-- omit in toc -->

由此可见，居中这件事儿交给 CSS 来做是没有什么大问题的。最后再过一下本文介绍的居中方法：

- 水平居中
  - text-align
  - auto-margin
  - [flex] justify-content
- 垂直居中
  - padding
  - line-height
  - absolute & -margin | transform
  - [flex] & auto-margin
  - [flex] align-item
  - [flex] flex-direction & justify-content
  - [flex] align-content (wrap)
  - [table-cell] vertical-align: middle
- 水平垂直居中
  - [grid] auto margin

<br/>

## 本文参考 <!-- omit in toc -->

- [Centering in CSS: A Complete Guide | CSS-Tricks](https://css-tricks.com/centering-css-complete-guide/)

<br/>
