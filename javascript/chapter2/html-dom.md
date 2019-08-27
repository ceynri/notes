# JavaScript | HTML DOM

文档对象模型 **D**ocument **O**bject **M**odel

HTML DOM模型被结构化为对象树：
![HTML DOM树](https://www.w3school.com.cn/i/ct_htmltree.gif)

## 目录 <!-- omit in toc -->

- [什么是 HTML DOM？](#什么是-html-dom)
- [HTML DOM模型能做什么](#html-dom模型能做什么)
- [例子](#例子)
- [document 对象](#document-对象)
  - [常用方法](#常用方法)
- [属性](#属性)
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

## HTML DOM模型能做什么

- 改变页面中的所有 HTML 元素、HTML 属性、CSS 样式
- 删除已有的或添加新的 HTML 元素和属性
- 对页面中所有已有的 HTML 事件作出反应
- 在页面中创建新的 HTML 事件

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

## document 对象

HTML DOM 文档对象（document）代表了你的网页，是网页中所有其他对象的拥有者。

### 常用方法

已收录于[方法索引表](../方法索引表#DOM)

#### 查找 HTML 元素 <!-- omit in toc -->

| 方法                                    | 描述                   |
| --------------------------------------- | ---------------------- |
| document.getElementById(*id*)           | 通过元素 id 来查找元素 |
| document.getElementsByTagName(*name*)   | 通过标签名来查找元素   |
| document.getElementsByClassName(*name*) | 通过类名来查找元素     |

#### 改变 HTML 元素 <!-- omit in toc -->

| 方法                                         | 描述                 |
| -------------------------------------------- | -------------------- |
| *element*.innerHTML = *new-html-content*     | 改变元素的 innerHTML |
| *element*.*attribute* = *new-value*          | 改变元素的属性值     |
| *element*.setAttribute(*attribute*, *value*) | 改变元素的属性值     |
| *element*.style.*property* = *new style*     | 改变元素的样式       |

#### 添加和删除元素 <!-- omit in toc -->

| 方法                              | 描述             |
| --------------------------------- | ---------------- |
| document.createElement(*element*) | 创建元素         |
| document.removeChild(*element*)   | 删除元素         |
| document.appendChild(*element*)   | 添加元素         |
| document.replaceChild(*element*)  | 替换元素         |
| document.write(*text*)            | 写入 HTML 输出流 |

注：*斜体*表示应该被对应内容替换的标记



















## 属性

每个 DOM 节点都属于某个类。这些类形成层次结构。完整的属性和方法集是继承的结果。

DOM 节点的属性主要有：

- nodeType  
  我们可以从 DOM 对象类中获取 nodeType，但我们通常只需要查看它是文本节点还是元素节点。nodeType 属性就可以我们的需求。它有数值，最重要的是：1 —— 是元素，3 —— 是文本。只读。

- nodeName/tagName  
  对于元素来说，标记名（除了 XML 模式外都要大写）。对于非元素节点，nodeName 则描述了它是什么。只读。

- innerHTML  
  HTML 的元素内容。可以被修改。

- outerHTML  
  元素的完整 HTML。写入 elem.outerHTML 的操作不会涉及 elem 自身。相反，它会在外部上下文中被替换成新的 HTML。

- nodeValue/data  
  非元素节点（文本、注释）内容。两者几乎一样，我们通常使用 data。允许被修改。

- textContent  
  元素中的文本，基本上是 HTML 减去所有 <tags>。将文本写入元素中，并把所有特殊字符和标记完全视为文本。可以安全地插入用户生成的文本，防止不必要的 HTML 插入。

- hidden  
  当设置为 true 时，执行与 CSS display:none 相同的操作。

DOM 节点还具有其他属性，具体内容则取决于它们的类。例如，\<input\>元素（HTMLInputElement）支持 value、type，而 \<a\> 元素（HTMLAnchorElement）则支持 href 等。大多数标准 HTML 属性都具有相应的 DOM 属性。

<br>

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