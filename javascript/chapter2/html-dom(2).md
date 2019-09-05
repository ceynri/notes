# JavaScript | HTML DOM（2）

文档对象模型 **D**ocument **O**bject **M**odel（DOM）

## 目录 <!-- omit in toc -->

- [节点](#节点)
  - [节点导航](#节点导航)
  - [节点属性](#节点属性)
- [DOM 元素](#dom-元素)
  - [查找 HTML 元素](#查找-html-元素)
  - [增删 HTML 元素](#增删-html-元素)
    - [旧方法](#旧方法)
    - [新方法](#新方法)
  - [改变 HTML 元素](#改变-html-元素)

<br>

---

<br>

## 节点

（`节点`不是`结点`，`结点`常用在数据结构与算法中）

根据 W3C HTML DOM 标准，HTML 文档中的所有事物都是节点：文档节点、元素节点、文本节点、属性节点、注释节点...

由这些节点，一篇 HTML 文档能够组成一颗节点树：

![HTML DOM 树][DOM 树]

### 节点导航

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

<h4>DOM 节点<span>例子</span></h4>
<p>DOM 节点</p>

<br>

这里的 `document.getElementById("id01")` 是 `<h4>` 元素，而 `document.getElementById("id01").firstChild` 指的是 `<h4>` 元素节点内的以 `DOM 节点` 为节点值的文本节点对象，而不是 `<span>` 元素节点，注意区分元素与节点的概念。

<br>

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

  常用值：

  | 节点         | 类型 | 例子                  |
  | ------------ | ---- | --------------------- |
  | ELEMENT_NODE | 1    | `<h1>`W3School`</h1>` |
  | TEXT_NODE    | 3    | `W3School`            |

  不常用值：

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

DOM 节点还有其他属性，具体内容则取决于它们的类。例如：`<input>` 元素（HTMLInputElement）支持 `value`、`type`，而 `<a>` 元素（HTMLAnchorElement）则支持 `href` 等。大多数标准 HTML 属性都具有相应的 DOM 属性。

<br>

## DOM 元素

注：*斜体*表示应该被对应内容替换的标记

### 查找 HTML 元素

| 方法                                            | 描述                          |
| ----------------------------------------------- | ----------------------------- |
| document.getElementById(*id*)                   | 通过 id 来查找 HTML 元素      |
| document.getElementsByTagName(*name*)           | 通过标签名来查找 HTML 元素    |
| document.getElementsByClassName(*name*)         | 通过类名来查找 HTML 元素      |
| document.querySelectorAll(*name-with-selector*) | 通过 CSS 选择器查找 HTML 元素 |

**注意getElement与getElement<u>s</u>的区别**

<br>

一些方法因为能够匹配多个 HTML 元素（带“`s`”的），返回的是 HTMLCollection 或 NodeList 对象（两者几乎相同），都具有 `length` 属性，可以通过中括号索引访问对应元素。

> HTMLCollection 与 NodeList 对象的区别：
>
> 返回值区别：
>
> - 如使用 getElementsByClassName() 方法，某些旧浏览器会返回 NodeList 对象，其他返回 HTMLCollection 对象。
> - 所有浏览器都会为 childNodes 属性返回 NodeList 对象。
> - 大多数浏览器会为 querySelectorAll() 方法返回 NodeList 对象。
>
> 结构区别：
>
> - 访问 HTMLCollection 项目可以通过它们的名称、id 或索引号。
> - 访问 NodeList 项目只能通过它们的索引号。
> - 只有 NodeList 对象能包含属性节点和文本节点。

还可以通过 HTML 对象选择器来查找 HTML 对象，如 document 的 `froms`、`images`、`links` 属性。

（带“`s`”的往往都是对象数组，注意使用中括号进行索引）

<br>

### 增删 HTML 元素

*注：首先介绍一些旧方法，下面介绍新方法。*

#### 旧方法

| 方法                                        | 描述           |
| ------------------------------------------- | -------------- |
| document.createElement(*element*)           | 创建 HTML 元素 |
| *elem*.removeChild(*child*)                 | 删除 HTML 元素 |
| *elem*.appendChild(*child*)                 | 添加 HTML 元素 |
| *elem*.insertBefore(*element*)              | 插入 HTML 元素 |
| *elem*.replaceChild(*newchild*, *oldchild*) | 替换 HTML 元素 |

<br>

如需向 HTML DOM 添加新 HTML 元素，必须首先创建这个 HTML 元素（元素节点），然后将其追加到已有 HTML 元素中。

- appendChild() 方法  
  将新元素作为当前对象的最后一个子节点。

- insertBefore() 方法  
  将新元素插入到当前对象的前面。

实例:

```html
<div id="div1">
  <p id="p1">段落1</p>
  <p id="p2">段落2</p>
</div>

<script>

  // 方法1
  var para = document.createElement("p");       // 创建元素
  var node = document.createTextNode("新文本"); // 创建文本节点
  para.appendChild(node);                       // 追加文本节点
    // 其实可以 “para.innerHTML = "新文本";” 一行搞掂

  var element = document.getElementById("div1");// 查找已有元素
  element.appendChild(para);                    // 追加新元素在最后面

  // 方法2
  para = document.createElement("p");
  node = document.createTextNode("新文本");
  para.appendChild(node);

  var child = document.getElementById("p2");    // 选中的是 p2
  element.insertBefore(para, child);            // 插在 p2 前面

</script>
```

效果：

段落1

新文本

段落2

新文本

<br>

删除 HTML 元素则使用 `removeChild()` 方法：

```html
<div id="div1">
  <p id="p1">这是一个段落。</p>
  <p id="p2">这是另一个段落。</p>
</div>

<script>

  // 普通方法
  var parent = document.getElementById("div1");
  var child = document.getElementById("p1");
  parent.removeChild(child);

  // 简便方法
  child.parentNode.removeChild(child);

</script>
```

替换 HTML 元素使用 `parent.replaceChild()` 方法：

```html
<div id="div1">
  <p id="p1">这是一个段落。</p>
  <p id="p2">这是另一个段落。</p>
</div>

<script>

  var para = document.createElement("p");
  var node = document.createTextNode("这是新文本。");
  para.appendChild(node);

  var parent = document.getElementById("div1");
  var child = document.getElementById("p1");
  parent.replaceChild(para, child);   // (替换元素, 被替换元素)

</script>
```

以上是旧方法，我们仍然能够在各种老的脚本里看到它们，所以认识它们还是有必要的。

#### 新方法

**插入文本或节点**

| 方法                 | 插入位置      |
| -------------------- | ------------- |
| *node*.before()      | node 前面     |
| *node*.prepend()     | node 内部开头 |
| *node*.append()      | node 内部末尾 |
| *node*.after()       | node 后面     |
| *node*.replaceWith() | 替换 node     |

参数：节点或字符串（支持多个参数）

<br/>

此方法可以围绕节点添加字符串或者节点，文本的所有内容会以安全的方式插入：

```html
<div id="div"></div>
<script>
  div.before('<p>Hello</p>', document.createElement('hr'));
</script>

<!-- 页面结果 -->
&lt;p&gt;Hello&lt;/p&gt;
<hr>
<div id="div"></div>
```

<br/>

如果希望标签不会被自动转换为安全文本，则可以使用以下方法直接编写 html:

**插入 html**

| 方法                                | 插入位置                 |
| ----------------------------------- | ------------------------ |
| *elem*.beforebegin(*where*, *html*) | elem 开头位置前插入 html |
| *elem*.afterbegin(*where*, *html*)  | elem 开头位置后插入 html |
| *elem*.beforeend(*where*, *html*)   | elem 结束位置前插入 html |
| *elem*.afterend(*where*, *html*)    | elem 结束位置后插入 html |

<br/>

样例：

```HTML
<div id="div"></div>
<script>
  div.insertAdjacentHTML('beforebegin', '<p>Hello</p>');
  div.insertAdjacentHTML('afterend', '<p>Bye</p>');
</script>

<!-- 页面结果 -->
<p>Hello</p>
<div id="div"></div>
<p>Bye</p>
```

<br>

### 改变 HTML 元素

| 方法                                         | 描述                 |
| -------------------------------------------- | -------------------- |
| *element*.innerHTML = *new-html-content*     | 改变元素的 innerHTML |
| *element*.*attribute* = *new-value*          | 改变元素的属性值     |
| *element*.setAttribute(*attribute*, *value*) | 改变元素的特性值     |
| *element*.style.*property* = *new style*     | 改变元素的 CSS 样式  |

其中，*element* 可以通过上面的“查找 HTML 元素”来获得对应的元素。

<br/>

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

<br>

---

<br>

## 更多内容 <!-- omit in toc -->

点击返回[个人笔记导航😊](../README.md)

<!-- 变量区 -->

[DOM 树]: https://www.w3school.com.cn/i/ct_htmltree.gif
