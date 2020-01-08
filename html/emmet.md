---
title: "Emmet 入门教程"
date: "2019-11-09"
---

# Emmet | HTML快速开发神器

HTML 作为一种随互联网诞生而不断发展的标记语言，其已经发展到 HTML5 版本并展示了强大的可用性。但 HTML 文档代码可不算是一种非常简洁的语言，复杂的标签记号往往使得网页编写者需要借助大量的自动补全才能在编写时不那么觉得枯燥无聊。

但今天介绍一个神器——Emmet，它的前身是 Zen coding，作为插件被广泛程序员使用。它利用了类 CSS 代码的编写方式能够快速地生成对应的 HTML 代码，进一步提升编写 HTML 的效率。

当然，生产力越高往往学习成本也越高，Emmet 类似于 Markdown，也需要你在使用前熟悉一下相关的简写语法，好消息是它的语法对于写过 CSS 的人来说非常熟悉，故门槛可以说是很低的。阅读完本篇教程，希望你能够初步上手 Emmet 并加以实践。

<br/>

## 基本操作

**注意：**

- 一般而言使用 Emmet 往往是“输入一段简写代码”+<kbd>Tab</kbd>的形式，出于方便本文默认省略<kbd>Tab</kbd>，请自行加上~ ☺
- 常用的文本编辑器如 VS Code 都内置了 Emmet 无需重新安装插件，这十分方便。

> ⚠**注意**
>
> 在新版本的 VS Code 中默认不启用 Emmet 自动补全，故需要在首选项配置中将`emmet.triggerExpansionOnTab`设置为`true` 。其他文本编辑器也要注意是否有类似的设置。

<br/>

### HTML 初始化

在刚刚新建一个 HTML 文档时，面对空白的内容，只需要输入一个感叹号并进行补全，Emmet 便会自动为你补全标准的 HTML5 文档常用结构代码。

**例子**

```html
!
```

**效果**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    
</body>
</html>
```

一个字符加上一个<kbd>Tab</kbd>便可以代替那么多行代码，是否体验到 Emmet 的强大之处了呢？

<br/>

### 标签

这是 Emmet 一个最简单的应用：对一个单词直接按<kbd>Tab</kbd>补全，Emmet 可以帮你自动补全尖括号与结尾的结束标签。

**例子**

```html
span
```

**效果**

```html
<span></span>
```

但是 Emmet 并不会检测该单词是否为合法的 HTML 标签，所以要注意自己的拼写。

还有某些标签的常见的属性支持使用`:`连接以自动补全，长标签名支持缩写。这些虽然方便但是数量比较多且比较零散，待 Emmet 使用熟练后可以去查找有多少支持这样的写法（如果编辑器支持 Emmet 提示则更好）。

**例子**（每一行都是独立的）

```html
script:src
link
link:css
a:link
inp
input
input:password
btn
btn:s
```

**效果**

```html
<script src=""></script>
<link rel="stylesheet" href="">
<link rel="stylesheet" href="style.css">
<a href="http://"></a>
<input type="text" name="" id="">
<input type="text">
<input type="password" name="" id="">
<button></button>
<button type="submit"></button>
```

<br/>

### 类 / id / 属性

使用类似于 CSS 的语法，能够快速生成带有类、id、属性的标签。

- `.foo` | 类
- `#foo` | id
- `[attr='foo']` | 属性

**例子**

```html
a.link#id[href='#']
```

注意编写 Emmet 时，除了设置多个属性时在`[]`中用空格分隔不同的属性以外，不要在其他地方穿插空格（下文类同），否则很容易不会补全。

**效果**

```html
<a href="#" class="link" id="id"></a>
```

<br/>

### 文本

使用花括号`{}`包裹一段文本，可以使其变成元素的文本节点。

**例子**

```html
span{some text}
```

**效果**

```html
<span>some text</span>
```

<br/>

### 嵌套

嵌套语法允许你在一行以内也能生成多级嵌套标签的 HTML 结构。

- `>` | 子级

- `+` | 同级

- `^` | 父级（符号后的元素提升为“符号前的元素的父元素”的同级元素）

**例子**

```html
div+div>span^a[href='#']
```

**效果**

```html
<div></div>
<div><span></span></div>
<a href="#"></a>
```

<br/>

### 分组

对于多层的标签嵌套，使用`^`符号来提升标签等级既不方便、可读性也不好。使用括号`(`、`)`包裹可以对标签进行分组，从而更好地创建多级标签结构。

**例子**

```html
(div.foo>span+a[href='#'])+(div.bar>h1>h2+h2)
```

**效果**

```html
<div class="foo"><span></span><a href="#"></a></div>
<div class="bar">
    <h1>
        <h2></h2>
        <h2></h2>
    </h1>
</div>
```

<br/>

### 隐式标签

在默认情况下，如果不写标签名而直接写类名或id，一般会自动认为该元素为`div`标签。

**例子**

```html
.foo#bar
```

**效果**

```html
<div class="foo" id="bar"></div>
```

<br/>

但如果在某些特定的父元素内省略标签名，则会根据该父元素自动补全相应的以下标签：

- `li` | `ul`、`ol`
- `tr` | `table`、`tbody`、`thead`和`tfoot`
- `td` | `tr`
- `option` | `select`、`optgroup`

**例子**

```html
table>.row>.elem+.elem
```

**效果**

```html
<table>
    <tr class="row">
        <td class="elem"></td>
        <td class="elem"></td>
    </tr>
</table>
```

<br/>

### 定义多个相同元素

使用`*`乘法符号，有助于你同时定义多个相同的同级元素。

**例子**

```html
ul>li*2
```

**效果**

```html
<ul>
    <li></li>
    <li></li>
</ul>
```

<br/>

## 高阶用法

### 自动计数

在使用`*`时，如果需要生成对应序数的类名/id，可以使用`$`符号，它会在补全时被替换为序号值。

**例子**

```html
ul>li.item$*3
```

**效果**

```html
<ul>
    <li class="item1"></li>
    <li class="item2"></li>
    <li class="item3"></li>
</ul>
```

> `$`符号并不一定要紧贴在`*`前面。

<br/>

如果想要生成多位数，可以使用多个`$`（需要连在一起）。

**例子**

```html
ul>li.item$$*3
```

**效果**

```html
<ul>
    <li class="item01"></li>
    <li class="item02"></li>
    <li class="item03"></li>
</ul>
```

<br/>

对于文本同样也能使用`$`。

**例子**

```html
ul>li.item${text$$}*3
```

**效果**

```html
<ul>
    <li class="item1">text01</li>
    <li class="item2">text02</li>
    <li class="item3">text03</li>
</ul>
```

<br/>

当然，升序降序、基数也可以被指定。在`$`之后添加`@`修饰符，可以指定它们。

- `@+` | 升序
- `@-` | 降序
- `@N` | 基数为N（如果有`@+`/`@-`，则跟在`+`/`-`后面）

（注：个人使用 VS Code 测试时发现并未支持`@+`、`@-`）

**例子**

```html
ul>li.item$@6*3
```

**效果**

```html
<ul>
    <li class="item6"></li>
    <li class="item7"></li>
    <li class="item8"></li>
</ul>
```

<br/>

### 包装文本

该功能需要编辑器的支持。

包装文本就是在文本已有的情况下，将这些文本填充入我们指定的 HTML 结构中。

举个例子，产品经理给了一个文本：

```html
首页
产品介绍
相关案例
关于我们
联系我们
```

而我们想要的效果：

```
<nav>
    <ul>
        <li>首页</li>
        <li>产品介绍</li>
        <li>相关案例</li>
        <li>关于我们</li>
        <li>联系我们</li>
    </ul>
</nav>
```

以 VS Code 为例，我们可以这样操作：

1. 选中文本，按下<kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>P</kbd>打开命令窗口，输入ewrap找到指令`Emmet: Wrap individual Lines with Abbreviation`并确认。

2. 输入缩写字符`nav>ul>li*`并确认，即可包装该文本（VS Code支持边输入缩写边预览效果）。

![emmet-wrap.gif](https://i.loli.net/2019/11/09/URN7TKuj3GpILHZ.gif)

注意缩写中的星号`*`，这指定了文本插入的等级。如果循环生成的标签不止一级（如下）：

```html
<nav>
    <ul>
        <li>
            <a href="#">首页</a>
        </li>
        <li>
            <a href="#">产品介绍</a>
        </li>
        <li>
            <a href="#">相关案例</a>
        </li>
        <li>
            <a href="#">关于我们</a>
        </li>
        <li>
            <a href="#">联系我们</a>
        </li>
    </ul>
</nav>
```

则对应的包装文本的缩写（注意理解`*`的位置）：

```html
nav>ul>li*>a[href="#"]
```

如果没有需要按行分开文本，则直接使用指令`Emmet: Wrap with Abbreviation`即可。

<br/>

## 其他

### 生成 Lorem ipsum 文本

Lorem ipsum 是一种常用于排版设计领域的拉丁文“占位文本”，便于测试文字在当前样式下的显示效果。Emmet 支持对 lorem 或 ipsum 进行<kbd>Tab</kbd>补全，它会帮你补全一段 Lorem ipsum 文本。

**例子**

```html
lorem
```

**效果**

```html
Lorem ipsum dolor sit amet consectetur adipisicing elit. Velit omnis quidem a aperiam cupiditate cum laudantium rerum, laborum tempora itaque at quae quibusdam quos odio incidunt nostrum porro ducimus praesentium!
```

<br/>

还可以指定文字的个数，比如 lorem8、lorem16。

**例子**

```html
lorem16
```

**效果**

```html
Lorem ipsum dolor sit amet consectetur adipisicing elit. Consectetur at deserunt, aliquam nulla eligendi reiciendis nam!
```

<br/>

### Emmet in CSS

Emmet 同样支持 CSS 代码的自动补全，具体语法不在本文介绍，但对于编写 CSS 来说同样实用，只是由于 CSS 的属性较多，需要记忆的缩写较多，感兴趣可以自行查找相关教程继续阅读。

**例子1**（以下代码每一行都是独立的，都可以用`+`连接）

```css
body {
	w12r+h10r
    m8
    t50p+l50p
    ovh
}
```

**效果**

```css
body {
	width: 12rem;
    height: 10rem;
    margin: 8px;
    top: 50%;
    left: 50%;
    overflow: hidden;
}
```

**例子2**

```css
body {
    -trf
}
```

**效果**（每个`:`后都会出现一个光标）

```css
body {
    -webkit-transform: ;
    -moz-transform: ;
    -ms-transform: ;
    -o-transform: ;
}
```

<br/>

## 最后

代码很难看看就会，学习 Emmet 亦是如此。

赶快动手尝试跟着教程试验一遍，在平时敲代码中试验一下，相信 Emmet 能为你的撸码效率提高一个层次！

<br/>