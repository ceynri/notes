---
title: "JavaScript与浏览器"
date: "2019-08-23"
---

# JavaScript | 基础介绍与应用

根据 W3school 的 JavaScript 教程进行整理，需要 HTML 基础。

## 目录摘要 <!-- omit in toc -->

- [在 HTML 中嵌入 JavaScript](#在-html-中嵌入-javascript)
  - [嵌入位置](#嵌入位置)
    - [\<head\>](#head)
    - [\<body\>](#body)
    - [外部引用](#外部引用)
    - [非常少用的示例](#非常少用的示例)
    - [区别](#区别)
- [输出](#输出)

<br>

---

<br>

## 在 HTML 中嵌入 JavaScript

亦如茴香豆有四种写法，在 HTML 文档中嵌入 JavaScript 代码的方法也有四种：

1. 直接嵌入：将 JS 代码放置在 `<script>` 和 `</script>` 标签之间；
2. 外部引入：放置在带有 `src` 属性的 `<script>` 标签所指定的外部文件中；
3. 事件触发：放置自 HTML 事件处理程序中，该事件处理程序由 `onclick` 或 `onmouseover` 这样的 HTML 属性值指定；
4. 放在一个 URL 里，这个 URL 使用特殊的 “javascript协议”。

其中，第一种与第二种较为多见，第三种较少使用（事件触发一般是调用第一第二种方法定义的函数而不是直接接脚本代码），第四种很难见到。

> “茴”的四种写法：上面是`艹`，下面分别是`回`、`囘`、`囬`、`廻`。

### 嵌入位置

#### \<head\>

在 `<head>` 标签之间可以嵌入 JavaScript 代码，并在 `<body>` 标签内调用。

在下面的例子，JS 代码定义的函数会被按钮被点击时调用：

```html
<!DOCTYPE html>
<html>
<head>
<script>
function myFunction() {
    document.getElementById("demo").innerHTML = "段落被更改。";
}
</script>
</head>

<body>

<h1>一张网页</h1>
<p id="demo">一个段落</p>
<button type="button" onclick="myFunction()">试一试</button>

</body>
</html>
```

#### \<body\>

在 `<body>` 标签之间也可以嵌入 JS 代码，且推荐将脚本放在 `<body>` 元素的底部，避免代码编译影响网页的显示速度。

实例：

```html
<!DOCTYPE html>
<html>
<body>

<h1>A Web Page</h1>
<p id="demo">一个段落</p>
<button type="button" onclick="myFunction()">试一试</button>

<script>
function myFunction() {
   document.getElementById("demo").innerHTML = "段落被更改。";
}
</script>

</body>
</html>
```

其中 `<button>` 元素通过点击事件运行脚本代码。

常见的 HTML 事件：

| 事件        | 描述                         |
| ----------- | ---------------------------- |
| onchange    | HTML 元素已被改变            |
| onclick     | 用户点击了 HTML 元素         |
| onmouseover | 用户把鼠标移动到 HTML 元素上 |
| onmouseout  | 用户把鼠标移开 HTML 元素     |
| onkeydown   | 用户按下键盘按键             |
| onload      | 浏览器已经完成页面加载       |

#### 外部引用

如想要从外部引用脚本，可以为 JavaScript 标签添加 `src` 属性并指定脚本位置（url）：

```html
<script src="/js/myScript.js"></script>
<script src="https://www.w3school.com.cn/js/myScript1.js"></script>
```

在外部文件中放置脚本有如下优势：

- 分离了 HTML 和代码
- 使 HTML 和 JavaScript 更易于阅读和维护
- 已缓存的 JavaScript 文件可加速页面加载

外部脚本直接编写 JavaScript 脚本代码即可，不能添加 `<script>` 标签。

#### 非常少用的示例

使用JavaScript协议：

```html
<a href="javascript:new Date().toLocaleTimeString();" rel="external nofollow">What time is it?</a>
```

#### 区别

`<head>` 中的脚本：需调用才执行的脚本 或 事件触发执行的脚本。当你把脚本放在HEAD部分中时，可以保证脚本在任何调用之前被加载。

`<body>` 中的脚本：当页面被加载时立即执行的脚本。通常被用来生成页面的内容。

如果直接运行的脚本放在 `<head>` 中，会因为页面未加载完全，使用到的元素未出现而报错。可以在 `<head>` 使用 `window.onload = function() {...}` 的方法使页面加载完后运行该部分代码。

## 输出

JavaScript 能够以不同方式“显示”数据：

- 使用 `document.write()` 写入 HTML 输出
- 使用 `innerHTML` 写入 HTML 元素
- 使用 `window.alert()` 写入警告框
- 使用 `console.log()` 写入浏览器控制台

使用 **innerHTML** 的实例：

```html
<!DOCTYPE html>
<html>
<body>

<h1>我的第一张网页</h1>
<p>我的第一个段落</p>
<p id="demo"></p>

<script>
 document.getElementById("demo").innerHTML = 5 + 6;
</script>

</body>
</html>
```

其中，`document.getElementById(id)` 用于获得 DOM 元素，然后再修改它的 `innerHTML` 属性。

如果是出于测试目的，使用 **document.write()** 比较方便：

```html
<!DOCTYPE html>
<html>
<body>

<h1>我的第一张网页</h1>
<p>我的第一个段落</p>

<script>
document.write(5 + 6);
</script>

</body>
</html>
```

但是在 HTML 文档完全加载后使用 `document.write()` 将删除所有已有的 HTML，故仅建议将其用于测试。

实例：

```html
<!DOCTYPE html>
<html>
<body>

<h1>我的第一张网页</h1>

<p>我的第一个段落</p>

<button onclick="document.write(5 + 6)">试一试</button>

</body>
</html>
```

`window.alert()` 能够使用弹出警告框来显示数据；`console.log()` 方法能够在浏览器控制台显示数据。（略）
