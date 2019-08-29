# JavaScript | HTML DOM (1)

文档对象模型 **D**ocument **O**bject **M**odel

HTML DOM模型被结构化为对象树：
![HTML DOM树](https://www.w3school.com.cn/i/ct_htmltree.gif)

## 目录 <!-- omit in toc -->

- [什么是 HTML DOM？](#什么是-html-dom)
- [HTML DOM模型能做什么](#html-dom模型能做什么)
- [例子](#例子)
- [document 对象](#document-对象)
- [常用方法](#常用方法)
  - [查找 HTML 元素](#查找-html-元素)
  - [改变 HTML 元素](#改变-html-元素)
  - [添加和删除元素](#添加和删除元素)
- [DOM 动画](#dom-动画)
- [DOM 事件](#dom-事件)
  - [代码调用方式](#代码调用方式)
  - [分配事件方式](#分配事件方式)
  - [事件种类](#事件种类)
  - [事件监听器](#事件监听器)
  - [事件冒泡 / 事件捕获](#事件冒泡--事件捕获)
- [节点](#节点)
  - [节点导航属性](#节点导航属性)
  - [节点属性](#节点属性)
- [*以下未整理*](#以下未整理)
- [Attributes and properties](#attributes-and-properties)
- [样式和类](#样式和类)
- [元素的尺寸与滚动](#元素的尺寸与滚动)
- [Window 的尺寸与滚动](#window-的尺寸与滚动)

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

<br>

## HTML DOM模型能做什么

- 改变页面中的所有 HTML 元素、HTML 属性、CSS 样式
- 删除已有的或添加新的 HTML 元素和属性
- 对页面中所有已有的 HTML 事件作出反应
- 在页面中创建新的 HTML 事件

<br>

## 例子

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

## 常用方法

已收录于[方法索引表](../方法索引表#DOM)

### 查找 HTML 元素

| 方法                                            | 描述                          |
| ----------------------------------------------- | ----------------------------- |
| document.getElementById(*id*)                   | 通过 id 来查找 HTML 元素      |
| document.getElementsByTagName(*name*)           | 通过标签名来查找 HTML 元素    |
| document.getElementsByClassName(*name*)         | 通过类名来查找 HTML 元素      |
| document.querySelectorAll(*name-with-selector*) | 通过 CSS 选择器查找 HTML 元素 |

还可以通过 HTML 对象选择器来查找 HTML 对象，如 document 的 froms、images、links 属性。

例子：

```js
var x = document.forms["frm1"];
var text = "";
 var i;
for (i = 0; i < x.length; i++) {
    text += x.elements[i].value + "<br>";
}
document.getElementById("demo").innerHTML = text;
```

### 改变 HTML 元素

| 方法                                         | 描述                 |
| -------------------------------------------- | -------------------- |
| *element*.innerHTML = *new-html-content*     | 改变元素的 innerHTML |
| *element*.*attribute* = *new-value*          | 改变元素的属性值     |
| *element*.setAttribute(*attribute*, *value*) | 改变元素的属性值     |
| *element*.style.*property* = *new style*     | 改变元素的 CSS 样式  |

其中，*element* 可以通过上面的“查找 HTML 元素”来获得对应的元素。

例子：

```HTML
<!DOCTYPE html>
<html>
<body>

<img id="myImage" src="smiley.gif">

<script>
document.getElementById("myImage").src = "landscape.jpg";
</script>

</body>
</html>
```

### 添加和删除元素

| 方法                              | 描述             |
| --------------------------------- | ---------------- |
| document.createElement(*element*) | 创建元素         |
| document.removeChild(*element*)   | 删除元素         |
| document.appendChild(*element*)   | 添加元素         |
| document.replaceChild(*element*)  | 替换元素         |
| document.write(*text*)            | 写入 HTML 输出流 |

注：*斜体*表示应该被对应内容替换的标记

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

在 `addEventListener(event, function[, useCapture])` 方法中可以通过使用 `useCapture` 参数来规定传播类型：默认值是 `false`，将使用冒泡传播，如果该值设置为 `true`，则事件使用捕获传播。  

<br>

## 节点

（`节点`不是`结点`，`结点`常用在数据结构与算法中）

根据 W3C HTML DOM 标准，HTML 文档中的所有事物都是节点：文档节点、元素节点、文本节点、属性节点、注释节点...

由这些节点，一篇 HTML 文档能够组成一颗节点树：

![HTML DOM 树](https://www.w3school.com.cn/i/ct_htmltree.gif)

### 节点导航属性

使用以下节点属性可以实现在节点之间的导航：

| 节点属性               | 描述                   |
| ---------------------- | ---------------------- |
| parentNode             | 父节点                 |
| childNodes[nodeNumber] | 第 nodeNumber 位子节点 |
| firstChild             | 首个子节点             |
| lastChild              | 最后一个子节点         |
| nextSibling            | 同一层级的后一个节点   |
| previousSibling        | 同一层级的前一个节点   |

注意：在编写 HTML 时，缩进之类的空白文本也会被算成文本节点，所以对于未压缩过的 HTML 文档在使用 childNodes[] 时需要注意。

例子：

```html
<html>
<body>

<h4 id="id01">DOM 节点<span>例子</span></h4>
<p id="id02">Hello!</p>

<script>
  document.getElementById("id02").innerHTML = document.getElementById("id01").firstChild.nodeValue;
</script>

</body>
</html>
```

显示效果：

<h4> DOM 节点<span>例子</span></h4>
<p>DOM 节点</p>

<br>

这里的 `document.getElementById("id01")` 是 `<h4>` 元素，而 `document.getElementById("id01").firstChild` 指的是 `<h4>` 元素节点内的以 `DOM 节点` 为节点值的文本节点对象，而不是 `<span>` 元素节点，注意区分元素与节点的概念。


### 节点属性

DOM 节点的属性主要有：

- innerHTML  
  HTML 元素的内容（可写）

- outerHTML  
  完整的 HTML 元素（可写）

  区别：
  
  ```js
  <body>
    <p>你好</p>
    <div id="test"><h5>就是喜欢你</h5></div>
    <script>
      var inner = document.getElementById("test").innerHTML;
      var outer = document.getElementById("test").outerHTML;
      alert(inner);
      alert(outer);
    </script>
  </body>

  // 输出结果：
  
  // inner
  <h5>就是喜欢你</h5>
  
  // outer
  <div id="test"><h5>就是喜欢你</h5></div>
  ```

  修改 innerHTML 只会改变元素的内容，修改 outerHTML 会产生新的元素覆盖掉旧的元素。

  <br>

  DOM 根节点：

- document.body  
  文档的 body 对象

- document.documentElement  
  完整的文档对象

  <br>

- nodeName  
  节点的名称（只读）

  | 类型     | 对应名称    |
  | -------- | ----------- |
  | 元素节点 | 大写标签名  |
  | 属性节点 | 属性名称    |
  | 文本节点 | `#text`     |
  | 文档节点 | `#document` |

  tagName 类似，但智能用在元素节点上。

  <br>

- nodeValue / data  
  节点的值（可写）

  | 类型     | 对应值      |
  | -------- | ----------- |
  | 元素节点 | `undefined` |
  | 文本节点 | 文本文本    |
  | 属性节点 | 属性值      |

  <br>

- nodeType  
  返回一个数字，查看它是什么类型的节点（只读）

  | 节点         | 类型 | 例子                  |
  | ------------ | ---- | --------------------- |
  | ELEMENT_NODE | 1    | `<h1>`W3School`</h1>` |
  | TEXT_NODE    | 3    | `W3School`            |

  <br>

  不常用：

  | 节点               | 类型 | 例子                                              |
  | ------------------ | ---- | ------------------------------------------------- |
  | ATTRIBUTE_NODE     | 2    | `class = "heading"` （HTML DOM 弃用，仅 XML DOM） |
  | COMMENT_NODE       | 8    | `<!-- 这是注释 -->`                               |
  | DOCUMENT_NODE      | 9    | HTML 文档本身（`<html>` 的父节点）                |
  | DOCUMENT_TYPE_NODE | 10   | `<!Doctype html>`                                 |

  <br>

  其他：

- textContent  
  元素中的文本，基本上是 HTML 减去所有 `<tags>`。
  
  将文本写入元素中，并把所有特殊字符和标记完全视为文本。可以安全地插入用户生成的文本，防止不必要的 HTML 插入。

- hidden  
  当设置为 `true` 时，执行与 CSS `display: none` 相同的操作。

一些 DOM 节点还有其他属性，具体内容则取决于它们的类。例如：`<input>` 元素（HTMLInputElement）支持 `value`、`type`，而 `<a>` 元素（HTMLAnchorElement）则支持 `href` 等。大多数标准 HTML 属性都具有相应的 DOM 属性。

<br>




<br>

## *以下未整理*


## Attributes and properties

特性 —— 写在 `HTML` 中。

属性 —— 是一个 `DOM` 对象。

对比：
|      | 属性                                     | 特性             |
| ---- | ---------------------------------------- | ---------------- |
| 类型 | 一些值，标准化的属性值在规范中有类型描述 | 字符串           |
| 名字 | 键名大小写敏感                           | 键名大小写不敏感 |

操作特性的一些方法：

- elem.hasAttribute(name) —— 检查是否存在这个特性
- elem.getAttribute(name) —— 获取这个特性
- elem.setAttribute(name, value) —— 把这个特性设置为 name 值
- elem.removeAttribute(name) —— 移除这个特性
- elem.attributes —— 所有特性的集合

对于大多数需求，`DOM` 属性已经可以给予很好的支持。应当在 `DOM` 属性实在无法满足开发需求的情况下才使用特性，比如以下情况：

- 我们需要一个非标准化的特性。但是如果我们用 `data-` 来设置特性值，那就要使用 `dataset` 来获取属性值。
- 我们想要读取到 `HTML` 的展示内容。比如 `href` 属性总是一个绝对路径，但是我们只想要相对路径。

<br>

## 样式和类

在管理 class 时，有两个 DOM 属性：

- className —— 字符串值可以很好地管理整个类集合。
- classList —— 拥有 add/remove/toggle/contains 方法的对象可以很好地支持单独的类。

改变样式：

- style 属性是一个带有 camelCased 样式的对象。对它的读取和修改 "style" 属性中的单个属性等价。要留意如果应用 important 和其他稀有内容 —— 在 MDN 上有一个方法列表。
- style.cssText 属性对应于整个“样式”属性，即完整的样式字符串。

获取已经解析的样式（对应于所有类，在应用所有 CSS 并计算最终值   后）：

- getComputedStyle(elem[, pseudo]) 返回与 style 对象类似且包含了所有类的对象，是只读的。

<br>

## 元素的尺寸与滚动

元素具有以下几何属性：

- offsetParent — 是最近的有定位属性的祖先元素，或者是 td、th、table、body。
- offsetLeft/offsetTop — 是相对于 offsetParent 的左上角边缘坐标。
- offsetWidth/offsetHeight — 元素的“外部”宽/高 ，边框尺寸计算在内。
- clientLeft/clientTop — 从元素左上角外部到内部的距离，对于从左到右渲染元素的操作系统，它始终是左/顶部边界的宽度，而对于从右到左的操作系统，垂直滚动条在左边，所以 clientLeft 也包括滚动条的宽度。
- clientWidth/clientHeight — 内容的宽度/高度，包括内间距，但没有滚动条。
- scrollWidth/scrollHeight — 内容的宽度/高度，包括可滚动的可视区域外的尺寸，也包括内间距，但不包括滚动条。
- scrollLeft/scrollTop — 从左上角开始的元素的滚动部分的宽度/高度。

除了 scrollLeft/scrollTop 之外，所有属性都是只读的。如果更改，浏览器会使元素滚动。

## Window 的尺寸与滚动

几何：

- 文档可视范围的宽度/高度（内容区域的宽高）：`document.documentElement.clientWidth/Height`

整个文档的宽度/高度，包括滚动区域外的部分：

```js
let scrollHeight = Math.max(
  document.body.scrollHeight, document.documentElement.scrollHeight,
  document.body.offsetHeight, document.documentElement.offsetHeight,
  document.body.clientHeight, document.documentElement.clientHeight
);
```

滚动：

- 读取当前的滚动：`window.pageYOffset/pageXOffset`

- 改变当前的滚动：
  - `window.scrollTo(pageX,pageY)` — 绝对定位
  - `window.scrollBy(x,y)` — 相对当前位置的滚动
  - `elem.scrollIntoView(top)` — 滚动到正好elem可视的位置（elem 与窗口的顶部/底部对齐）
