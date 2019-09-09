---
title: "HTML DOM（1）"
date: "2019-08-24"
---

# JavaScript | HTML DOM（1）

文档对象模型 **D**ocument **O**bject **M**odel（DOM）

## 目录 <!-- omit in toc -->

- [什么是 HTML DOM？](#什么是-html-dom)
- [HTML DOM模型能做什么](#html-dom模型能做什么)
- [document 对象](#document-对象)
- [DOM 动画](#dom-动画)
- [DOM 事件](#dom-事件)
  - [代码调用方式](#代码调用方式)
  - [分配事件方式](#分配事件方式)
  - [事件种类](#事件种类)
  - [事件监听器](#事件监听器)
  - [事件冒泡 / 事件捕获](#事件冒泡--事件捕获)

<br>

---

<br>

## 什么是 HTML DOM？

HTML DOM 是 HTML 的标准对象模型和编程接口，是关于如何获取、更改、添加或删除 HTML 元素的标准。

它定义了：

- 作为对象的 HTML 元素
- 所有 HTML 元素的属性
- 访问所有 HTML 元素的方法
- 所有 HTML 元素的事件


HTML DOM模型可以被结构化为对象树：

![HTML DOM树][DOM 树]

<br>

## HTML DOM模型能做什么

- 改变页面中的所有 HTML 元素、HTML 属性、CSS 样式
- 删除已有的或添加新的 HTML 元素和属性
- 对页面中所有已有的 HTML 事件作出反应
- 在页面中创建新的 HTML 事件

<br>

例子：

```html
<html>
<body>

<p id="demo"></p>

<script>
  document.getElementById("demo").innerHTML = "Hello World!";
</script>

</body>
</html>
```

- `getElementById` 方法  
  在上例中使用 `id="demo"` 来查找元素。

- `innerHTML` 属性  
  可用于获取或改变任何 HTML 元素，包括 `<html>` 和 `<body>`。

<br>

## document 对象

HTML DOM 文档对象（document）代表了你的网页，是网页中所有其他对象的拥有者。

想要访问 HTML 页面中的其他元素，往往就是从访问 document 对象开始的。

<br>

## DOM 动画

JavaScript 提供了一个定时器 `setInterval()` 的方法，可以用来制作简易的动画。

**注意**：本段的 DOM 动画 Demo 仅用来加深对 JavaScript 与 DOM 的理解，实际情况下直接修改 DOM 会产生很大的性能问题，故**不推荐使用此方法**制作动画。

<br>

首先，创建一个 HTML 页面，使用一层 div 作为容器元素包裹 div 动画元素。

```html
<!DOCTYPE html>
<html>
<body>

<h1>我的第一部 JavaScript 动画</h1>

<div id ="container">
  <div id="animation">我的动画在这里。</div>
</div>

</body>
</html>
```

然后添加样式：

```css
#container {
  width: 400px;
  height: 400px;
  position: relative;
  background: gray;
}
#animate {
  width: 50px;
  height: 50px;
  position: absolute;
  background: orange;
}
```

然后使用 JavaScript，思路是借助定时器，每隔一段时间执行一次移动任务，当间隔时间足够短时动画看起来便足够连贯。

setInterval 的语法：

```js
setInterval(code,millisec[,"lang"])
```

`code` 为每次执行的代码串（函数），`millisec` 为执行 `code` 的时间周期（毫秒单位）。

常用的解构如下：

```js
var id = setInterval(frame, 5);

function frame() {
    if (/* 测试是否完成 */) {
        clearInterval(id);    // 调用后，停止 id 计时器
    } else {
         /* 改变元素样式的代码 */
    }
}
```

最后完成的动画 Demo 如下：

```html
<!DOCTYPE html>
<html>
<style>
#container {
  width: 400px;
  height: 400px;
  position: relative;
  background: gray;
}
#animate {
  width: 50px;
  height: 50px;
  position: absolute;
  background: orange;
}
</style>
<body>

<p><button onclick="myMove()">单击此处</button></p>

<div id ="container">
  <div id ="animate"></div>
</div>

<script>
function myMove() {
  var elem = document.getElementById("animate");
  var pos = 0;
  var id = setInterval(frame, 5);
  function frame() {
    if (pos == 350) {
      clearInterval(id);
    } else {
      pos++;
      elem.style.top = pos + "px";
      elem.style.left = pos + "px";
    }
  }
}
</script>

</body>
</html>
```

<br>

## DOM 事件

HTML 事件有许多例子：

- 点击鼠标时
- 用户敲击按键时
- 鼠标移至元素上时
- 输入字段被改变时
- HTML 表单被提交时
- 网页加载后
- 图像加载后

通过 HTML DOM，我们可以编写 JavaScript 代码对 HTML 事件作出反应。

### 代码调用方式

我们可以直接插入 JS 代码，或者通过调用 JS 函数的方式执行代码：

```html
<!DOCTYPE html>
<html>
<body>

<!-- 方法 1 -->
<h1 onclick="this.innerHTML = 'Hello~'">点我</h1>

<!-- 方法 2 -->
<h1 onclick="changeText(this)">点我我</h1>

<script>
function changeText(id) {
    id.innerHTML = "Hello :)";
}
</script>

</body>
</html>
```

### 分配事件方式

除了直接在标签中添加事件属性，也可以使用 JavaScript 代码向 HTML 元素分配事件：

```html
<!DOCTYPE html>
<html>
<body>

<button onclick="displayDate()">试一试</button>

<button id="my_btn">再试试</button>

<script>
  document.getElementById("my_btn").onclick = displayDate;
</script>

</body>
</html>
```

### 事件种类

| 事件名                   | 描述                                             |
| ------------------------ | ------------------------------------------------ |
| onload / onunload        | 进入/离开 页面时                                 |
| onchange                 | 内容 被改变 时                                   |
| onmouseover / onmouseout | 移入/移出 某个元素的上方时                       |
| onmousedown / onmouseup  | 鼠标按钮 按下/抬起时                             |
| onclick                  | 鼠标按钮点击后（按下与抬起动作都在元素上方完成） |

### 事件监听器

使用 `addEventListener()` 方法可以为 HTML 元素（或 DOM 对象）指定事件处理程序。

语法：

```js
element.addEventListener(event, function[, useCapture]);
//                    参数类型，被调用的函数，布尔值（指定事件冒泡/事件捕获，后讲）
```

由于该方法不会覆盖已有的事件处理程序，我们可以给一个元素添加多个相同或不相同类型的事件处理程序。

使用该方法添加事件监听，达到了代码分离的效果，只用在 JavaScript 文件中修改代码而无需跳转至 HTML 文档。

在旧浏览器版本下可以使用 `attachEvent()`方法。

添加监听器所对应的移除方法是 `removeEventListener()`。

监听器例子：

```js
element.addEventListener("click", function(){
  alert("Hello World!");
});

element.addEventListener("click", function(){
  console.log("Hello World!");
}); //并不会和第一个冲突或覆盖
```

DOM 对象（如 `window`）也支持添加事件监听器：

```js
// 添加当用户调整窗口大小时触发的事件监听器
window.addEventListener("resize", function(){
    document.getElementById("demo").innerHTML = sometext;
});
```

如果需要给函数传递参数，请写成调用指定函数的匿名函数的形式：

```js
element.addEventListener("click", function(){ myFunction(p1, p2); });
```

### 事件冒泡 / 事件捕获

在 HTML DOM 中有两种事件传播的方法：冒泡和捕获。

事件传播是一种定义当发生事件时元素次序的方法，确定次序的方式区别：在冒泡中，最先处理内侧元素的事件，然后是外层元素；捕获则反之。

> 假如 `<div>` 元素内有一个 `<p>`，然后用户点击了这个 `<p>` 元素：
>
> - 冒泡：首先处理 `<p>` 元素的点击事件，然后是 `<div>` 元素的点击事件。
>
> - 捕获：首先处理 `<div>` 元素的点击事件，然后是 `<p>` 元素的点击事件。

在 `addEventListener(event, function[, useCapture])` 方法中可以通过使用 `useCapture` 参数来规定传播类型：

| 布尔值            | 传播方式 |
| ----------------- | -------- |
| `false`（默认值） | 冒泡     |
| `true`            | 捕获     |

由于 IE 的 attachEvent 仅支持冒泡，为了统一性，一般使用默认值。

<!-- 变量区 -->

[DOM 树]: https://www.w3school.com.cn/i/ct_htmltree.gif
