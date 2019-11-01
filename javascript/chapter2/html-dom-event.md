---
title: "HTML DOM 事件"
date: "2019-08-24"
---

# JavaScript | HTML DOM 事件

交互性是互联网应用非常重要的一部分，而事件是交互的关键。

## 目录 <!-- omit in toc -->

- [HTML 事件](#html-事件)
- [事件种类](#事件种类)
- [创建监听](#创建监听)
  - [代码插入/代码调用](#代码插入代码调用)
  - [分配事件](#分配事件)
  - [事件监听器](#事件监听器)
- [输入框事件监听](#输入框事件监听)
- [其他概念](#其他概念)
  - [事件对象](#事件对象)
  - [事件冒泡 / 事件捕获](#事件冒泡--事件捕获)

<br>

---

## HTML 事件

HTML 的事件有许多例子：

- 点击鼠标时
- 用户敲击按键时
- 鼠标移至元素上时
- 输入字段被改变时
- HTML 表单被提交时
- 网页加载后
- 图像加载后

通过 HTML DOM，我们可以编写 JavaScript 代码对 HTML 事件作出反应。

<br/>

## 事件种类

| 事件名                   | 描述                                             |
| ------------------------ | ------------------------------------------------ |
| onload / onunload        | 进入/离开 页面时                                 |
| onchange                 | 内容 被改变 时                                   |
| onmouseover / onmouseout | 移入/移出 某个元素的上方时                       |
| onmousedown / onmouseup  | 鼠标按钮 按下/抬起时                             |
| onclick                  | 鼠标按钮点击后（按下与抬起动作都在元素上方完成） |

<br/>

## 创建监听

### 代码插入/代码调用

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

但这是一种不好的方式，非常不利于后期维护，且不利于收索引擎理解页面。不建议使用该方法添加 DOM 事件。

<br/>

### 分配事件

除了直接在标签中添加事件属性，也可以使用 JavaScript 代码向 HTML 元素分配事件：

```html
<!DOCTYPE html>
<html>
<body>

<button id="my_btn">按我</button>

<script>
  document.getElementById("my_btn").onclick = displayDate;
</script>

</body>
</html>
```

使用 js 代码直接为 DOM 元素的事件属性虽然方便，但是也存在一些缺点，例如后面添加的值会覆盖前面的值，从而无法更好的管理多个事件触发器。

<br/>

### 事件监听器

使用 `addEventListener()` 方法可以为 HTML 元素（或 DOM 对象）指定事件处理程序。这也是最推荐的添加事件监听的方式。

语法：

```js
// 参数类型 | 被调用的函数 | 布尔值（指定事件冒泡/事件捕获，后讲）
element.addEventListener(event, function[, useCapture]);
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

<br/>

## 输入框事件监听

输入框作为一个常用的表单控件，其拥有好几种事件如`focus`、`keydown`、`keyup`、`input`、`change`、`blur`，但这些事件的应用时机与场景有着不小的差异。

最先被激活的往往是`focus`事件。这是一个不少元素都具有的事件属性，当“焦点”聚集在输入框元素时，该事件便会激活。

“焦点”聚集的方法可以是使用Tab键控制焦点切换到输入框上，或者直接用鼠标点击一下输入框（注意和`click`并不等价），被激活后输入框一般都会有光标闪烁提醒你正在输入字符。

其次，进行一次按键的点击，会按时间顺序产生`keydown`、`input`、`keyup`三种事件，只有它们三个能够察觉到用户每次键盘输入的变化。

`keydown`和`keyup`很好理解，即为按键按下和抬起的动作瞬间触发。而`input`事件虽然很像`keydown`，但是他从语义上讲更加偏重于“有输入的事件发生”而不同于“有按键被按下”，导致了`input`无法获取到当前输入的`keyCode`值而`key`、`keydown`可以。

最后当输入框失去焦点时，会触发`change`和`blur`事件。这两个事件的区别点在于：`change`在输入框内容的最终值与原值相同时不会触发，即便进行过删除与输入操作；而`blur`则仅监控失去焦点这个事件，不管怎样都会触发。

故按照时间顺序可以这样排序：`focus`->`keydown`->`input`->`keyup`->`change`->`blur`

<br>

## 其他概念

一下内容为关于 DOM 事件的高级概念，阅读它们可以有助于理解一些其他的代码模式。

### 事件对象

addEventListener所回调的函数可以附带一个参数（常常被命名为 e/evt/event），它被称为事件对象。事件对象具有一个`target`属性，永远表示触发事件发生的元素的引用。通过使用事件对象，我们可以不用使用复杂的选择去获得被点击的元素（如果你对许多元素添加了相同的监听）。

一个例子：

```js
function bgChange(e) {
  // 获得随机颜色
  var rndCol = 'rgb(' + random(255) + ',' + random(255) + ',' + random(255) + ')';
  // 将触发事件的元素的背景颜色设置为一个随机的颜色
  e.target.style.backgroundColor = rndCol;
  console.log(e);
}
```

<br/>

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

<br/>

<!-- 变量区 -->

[DOM 树]: https://www.w3school.com.cn/i/ct_htmltree.gif
