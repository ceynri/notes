---
title: "CSS 常见问题"
date: "2019-09-27"
---

# 一些遇到过的问题

## 目录 <!-- omit in toc -->

- [CSS](#css)
  - [Q: 在\<div>或\<a>元素中放入\<img>元素后，父元素高度比里面的\<img>高度要高 4px/5px](#q-在div或a元素中放入img元素后父元素高度比里面的img高度要高-4px5px)
  - [Q: display: none、visibility: hidden、opacity: 0 之间的区别？](#q-display-nonevisibility-hiddenopacity-0-之间的区别)
  - [Q: 内联元素之间有间隙](#q-内联元素之间有间隙)
  - [Q: 如何隐藏滚动条？](#q-如何隐藏滚动条)
  - [Q: 如何实现图片在给定宽高的容器里不变形地覆盖整个容器？](#q-如何实现图片在给定宽高的容器里不变形地覆盖整个容器)
  - [Q: more...](#q-more)

## CSS

### Q: 在\<div>或\<a>元素中放入\<img>元素后，父元素高度比里面的\<img>高度要高 4px/5px

- 原因：

    在\<a>元素或者\<div>元素下有一个匿名文本，该文本外存在一个匿名行级盒子，由于 `line-height` 存在使其有了高度。因为默认 `vertical-align` 为 `baseline` 对齐的原因，\<img>之类的`inline-block`元素会使得这个匿名盒子下沉，撑开一些距离，于是把\<a>撑高了。

- 解决办法（任选其一）：

+ 消除掉匿名盒子的高度，给\<a>设置`line-height: 0`或`font-size: 0`；

+ 给两者`vertical-align: top`，让其`top`对齐，而不是`baseline`对齐；

+ 如果\<img>元素是单独一行的话，可以给\<img>以`display: block`，让它和匿名行级盒子不在一个布局上下文中，也就不存在行级盒。\<img>是行内元素，默认`display: inline-block`，与文本的默认行为类似，下边缘是与基线对齐，而不是紧贴容器下边缘。

<br/>

### Q: display: none、visibility: hidden、opacity: 0 之间的区别？

三者都可以将元素隐藏，但存在区别如下：

| 属性                 | 解释         | 空间占据 | 子元素继承                                  | 事件绑定可否触发 | 过渡动画能否作用 |
| -------------------- | ------------ | -------- | ------------------------------------------- | ---------------- | ---------------- |
| `display: none`      | 彻底消失     | ✘        | ✘，父元素不在了，子元素也不会显示           | ✘                | ✘                |
| `visibility: hidden` | 视觉上不可见 | ✔        | ✔，如果设置子元素可见则仍然可以使子元素显示 | ✘                | ✘                |
| `opacity: 0`         | 透明度为0    | ✔        | ✔，子元素无法通过设置 `opacity` 值显示      | ✔                | ✔                |

<br/>

### Q: 内联元素之间有间隙

- 原因：

    在 HTML 中，内联元素是类似于当作文本处理的。两个内联元素的 HTML 标签之间如果有换行，则会将换行符自动转换为一个空格。

- 解决办法：

    元素标签之间不换行即可。如果你的内联元素是`inline-block`，还可以给父元素设置`font-size: 0`。

<br/>

### Q: 如何隐藏滚动条？

- 情况：

    对于一些固定尺寸的窗口需要塞入超过窗口大小的内容时，`overflow: scroll`是个不错的选择，但很多时候其产生的滚动条并不美观，于是便需要想办法将滚动条隐藏起来。

- 解决办法：

    ```css
    .scroll-area {
        overflow: scroll;
        /* IE10/Edge 去除滚动条 */
        -ms-overflow-style: none;
        /* firefox 64 隐藏滚动条 */
        scrollbar-color: transparent transparent;
        /* firefox 64 去除滚动条 */
        scrollbar-width: none;
    }

    /* Chrome 去除滚动条 */
    .scroll-area::-webkit-scrollbar {
        width: 0;
        height: 0;
    }
    ```

    其中“隐藏滚动条”代表只能将滚动条透明化，其仍然能被点击到，且占据原有的空间，只是视觉上不可见。

<br/>

### Q: 如何实现图片在给定宽高的容器里不变形地覆盖整个容器？

- 情况：

    每当使用图片时往往会采用img标签，但仅通过设置img标签往往并不能兼顾宽度自适应与高度自适应。

- 解决办法：

    用background设置图片的方式可以很容易地实现该需求。

    可以使用这样的语法：

    ```css
    /* background: <bg-image> <position>/<bg-size> <repeat-style> */
    .image {
        background: url(imgs/img.jpg) center/cover no-repeat;
    }
    ```

    其中，`background-size`只能跟在`position`后面，中间用斜杠隔开。

    `center`代表居中，`cover`代表覆盖。

    如果`background-size`使用`contain`值，则为包含，效果与`max-width: 100%; max-height: 100%;`相类似。



<br/>

### Q: more...



<br/>
