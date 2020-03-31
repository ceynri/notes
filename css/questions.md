---
title: "CSS 常见问题"
date: "2019-09-27"
---

# 一些遇到过的问题

## 目录 <!-- omit in toc -->

- [CSS](#css)
  - [Q: 如何更直观更方便地调试元素的尺寸与布局？](#q-如何更直观更方便地调试元素的尺寸与布局)
  - [Q: 在父元素中单独放入\<img>元素后，\<img>底部或后面有空白怎么办？](#q-在父元素中单独放入img元素后img底部或后面有空白怎么办)
  - [Q: display: none、visibility: hidden、opacity: 0 之间的区别？](#q-display-nonevisibility-hiddenopacity-0-之间的区别)
  - [Q: 内联元素之间有间隙](#q-内联元素之间有间隙)
  - [Q: 如何隐藏滚动条？](#q-如何隐藏滚动条)
  - [Q: 如何实现图片在给定宽高的容器里不变形地覆盖整个容器？](#q-如何实现图片在给定宽高的容器里不变形地覆盖整个容器)
  - [Q: hover 某元素使另一元素遮挡住该元素而导致闪烁怎么办？](#q-hover-某元素使另一元素遮挡住该元素而导致闪烁怎么办)
- [JavaScript](#javascript)
  - [Q: 将内容复制到用户的剪贴板上？](#q-将内容复制到用户的剪贴板上)
  - [Q: JavaScript 获取不到 CSS 设置的属性值？](#q-javascript-获取不到-css-设置的属性值)
  - [Q: JavaScript 设置的样式覆盖不了 CSS 样式？](#q-javascript-设置的样式覆盖不了-css-样式)
  - [Q: more...](#q-more)

## CSS

### Q: 如何更直观更方便地调试元素的尺寸与布局？

- 情况：
  
    有许多的元素（例如布局元素`div`或者`span`），我们一般不能直观地看到它们的大小、位置，只能通过`F12`去手动检查。

- 技巧：

    给所有元素或者某些元素（如`div`）画上一个框，这样就能够清晰地看出每个元素的情况了。

    ```css
    * {
        outline: red solid 1px;
        /* 使用border效果类似，但outline不会增加元素大小，而border会 */
    }
    ```

<br>

### Q: 在父元素中单独放入\<img>元素后，\<img>底部或后面有空白怎么办？

- 原因：

    1. 在\<a>元素或者\<div>等元素下有一个匿名文本，该文本外存在一个匿名行级盒子，由于 `line-height` 存在使其有了高度。
    
        因为默认 `vertical-align` 为 `baseline` 对齐的原因，\<img>之类的`inline-block`元素会使得这个匿名盒子下沉，撑开一些距离，于是把父元素撑高了。

    2. HTML 文档中，换行或者空格会被翻译成一个空白的文本节点（`#text`），导致会出现一个空格跟在\<img>后面的情况。

- 解决办法（任选其一）：

    + 消除掉匿名盒子的高度，给\<a>设置`line-height: 0`或`font-size: 0`；
    + 给两者`vertical-align: top`，让其`top`对齐，而不是`baseline`对齐；
    + 如果\<img>元素是单独一行的话，可以给\<img>以`display: block`或者`float: left`，让它和匿名行级盒子不在一个布局上下文中，也就不存在行级盒。\<img>是行内元素，默认为 inline-block，与文本的默认行为类似，下边缘是与基线对齐，而不是紧贴容器下边缘。
    + 对于多个`inline-block`元素之间的空格，可以使用`letter-spacing: -4px`（字符之间的间距）或`word-spacing: -4px`（单词之间的间距）。

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

### Q: hover 某元素使另一元素遮挡住该元素而导致闪烁怎么办？

- 情况：
  
    有时候我们需要实现鼠标悬停在某元素上时，该元素变为另外一个元素的效果，但另外一个元素如歌出现在该元素的上面，则相当于将鼠标与该元素隔开，使得该效果失效。

- 解决方法：

    使用 JavaScript 是一种思路，但更好的方法是直接使用 CSS3 相应的属性`pointer-events`。
    
    语法：

    ```
    pointer-events: auto（默认值） | none;
    // 以下值仅对SVG元素有效
    pointer-events: visiblepainted | visiblefill | visiblestroke | visible | painted | fill | stroke | all
    ```

    像 mouseover 这样的效果，都是由光标产生的事件，如果不想让新出现的元素遮挡住旧元素，可以设置：
    
    ```css
    .new-element {
        pointer-events: none;
    }
    ```

    当值为`none`时，该元素就会不再与鼠标产生任何交互，鼠标悬停的判定会穿透该元素至下层。

<br>

## JavaScript

> 不小心就归到了 CSS 部分中来了，先暂时放在这边叭

### Q: 将内容复制到用户的剪贴板上？

- 情况：
    
    想要实现用户点击按钮即可复制文本的效果。

- 实现方法：
    
    js 提供了`execCommand`方法，它允许使用命令来操纵可编辑区域的内容。
    
    虽然表面上和我们想要达到的效果并没有直接关系，但该方法有一个参数——`copy`，可以让我们对可编辑区域中已经选中的文本内容执行复制操作。

    如果想要实现的效果不是从编辑区域中获取要复制的文本，则可以构造一个带有我们想要的文本的`input`元素添加到页面中，选中并复制完后立即移除该元素即可。

    代码如下：

    ```js
    const btn = document.querySelector('#btn');
    btn.addEventListener('click',() => {
        // 创建可编辑区域
        const input = document.createElement('input');
        document.body.appendChild(input);
        // 设置输入框的内容（会被复制）
        input.setAttribute('value', '复制的内容');
        // 设置输入框为只读属性，避免唤起手机键盘
        input.setAttribute('readonly', 'readonly');
        // 选中输入框内容
        input.select();
        // 如遇 input.select() 未选择到文本内容的情况，试下下面的代码
        // input.setSelectionRange(0, 9999);
        // 执行复制操作
        if (document.execCommand('copy')) {
            document.execCommand('copy');
            console.log('复制成功');
        }
        // 移除该元素
        document.body.removeChild(input);
    })
    ```

    > 还有第三方库方法：clipboard.js，这里不做赘述。

<br>

### Q: JavaScript 获取不到 CSS 设置的属性值？
### Q: JavaScript 设置的样式覆盖不了 CSS 样式？

- 情况：

    问题1：在 javascript 中访问`elem.style.<attr>`，得到的属性返回空；

    问题2：在 javascript 中使用`elem.style.<attr> = <val>`为样式规则赋值，样式没有应用上。

- 原因：

    问题1：在 javascript 中访问元素的样式属性，虽然它是可读可写的，但它不能获得在其他地方（如 CSS）中设置的样式值。（联想到在 HTML 标签的 style 属性中设置样式与使用 CSS 引入样式的差别）
    
    问题2：虽然 javascript 代码没有编写错，但 CSS 那边对相同的样式规则应用了不同的属性值，使得将 js 设置的样式给覆盖掉了。

- 解决方法：

    1. 可以将 CSS 的样式转移到 JavaScript 代码中来设置，这样就便于管理相关的值了。
    2. 使用以下语句计算获得当前元素的样式并取得目标样式规则的值：
    
        ```js
        getComputedStyle(<elem>, null).getPropertyValue(<prop-name>);
        ```

        > 旧 IE 使用 elem.currentStyle.getAttribute('style'); 

        但第2种方法不能设置样式属性值。


<br>

### Q: more...

<br/>
