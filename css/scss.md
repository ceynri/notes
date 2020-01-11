---
title: "Sass 速览教程"
date: "2020-01-11"
---

# Sass 速览教程

自己刷了一些 Sass 的教程，顺手记录一下，本文的意义是尽可能精简内容合例子，删除没有太多意义的废话，使得能够更加高效地上手 Sass。

> SCSS 为 Sass 的新版本语法，原本 Sass 语法可以专指旧版本语法，目前看来也可以通称 SCSS 为 Sass（即：使用 SCSS 语法的 Sass）。
> 
> 本篇文章提及的 Sass 均遵循 SCSS 语法规范。

<br>

## 安装

选择以下其中一种方式：

- NPM

```
npm install -g sass
```

- Windows（Chocolatey）

```
choco install sass
```

- Mac OS X（Homebrew）

```
brew install sass/sass/sass
```

测试安装是否成功：

```
sass -v
```

<br>

## 编译

```bash
sass input.scss output.css
```

<br>

## 变量

### 变量名

以`$`符号作为开头。

Sass 代码：

```scss
$myWidth: 680px;

#container {
  width: $myWidth;
}
```

转换后：

```css
#container {
  width: 680px;
}
```

<br>

### 作用域

变量有作用域的设定，故需要注意上下文顺序，嵌套层级等。

使用`!global`关键词可以提升变量为全局变量。

```scss
$myColor: red;

h1 {
  $myColor: green !global;  // 全局作用域
  color: $myColor;
}

p {
  color: $myColor;
}
```

输出的颜色全都会变成绿色。

> 👍 所有的全局变量我们一般定义在同一个文件，如：_globals.scss，然后我们使用 @include 来包含该文件。

<br>

## 算术运算符

Sass 提供了标准的算术运算符，例如+、-、*、/、%。
```scss
.container { width: 100%; }

article[role="main"] {
  float: left;
  width: 600px / 960px * 100%;
}

aside[role="complementary"] {
  float: right;
  width: 300px / 960px * 100%;
}
```

导出的 CSS 代码为计算好的数值。

> ⚠ **注意**，动态的值是不能被提前计算的，比如`100px + 50%`，存在单位问题。

<br>

## 嵌套

### 层级嵌套

Sass 代码：

```scss
nav {
  ul {
    list-style: none;
  }
  li {
    display: inline-block;
  }
}
```

转换的 CSS：

```css
nav ul {
  list-style: none;
}

nav li {
  display: inline-block;
}
```

<br>

### 属性嵌套

我们称带有相同前缀（`prefix-`）的属性为处以同一命名空间下，如`font-size`、`font-weight`都位于`font`命名空间下。

SCSS 语法中，属性具有命名空间，在冒号（`:`）后面可以嵌套子属性。

Sass 代码：

```scss
font: {
  family: 'MircoSoft YaHei';
  size: 18px;
  weight: bold;
}
```

转换为 CSS：

```css
font-family: 'MircoSoft YaHei';
font-size: 18px;
font-weight: bold;
```

也可以先设置一般规则，然后嵌套例外规则：

```scss
font: 18px 'MircoSoft YaHei' {
  weight: bold;
}
```

和上面的代码等价。

<br>

### & 父级选择器

在嵌套中使用`&`，会被替换为按照父级选择器级联替换。

添加伪类是一种用法：

```scss
#main {
  color: black;

  a {
    font-weight: bold;

    &:hover { 
      color: red; 
    }
  }
}
```

对应 CSS：

```CSS
#main {
  color: black; 
}

#main a {
  font-weight: bold; 
}

#main a:hover {
  color: red; 
}
```

也可以用来取一个系列的名：

```scss
/*===== SCSS =====*/
#content {
  color: black;
  
  &-sidebar {
    border: 1px solid;
  }

  &-footer {
    background-color: #ccc;
  }
}
```

效果：

```css
#content {
  color: black;
}

#content-sidebar {
  border: 1px solid; 
}

#content-footer {
  background-color: #ccc;
}
```

<br>

### 其他选择器

标准的 CSS 选择器也可以在嵌套中使用：

```scss
article {
  ~ article { border-top: 1px dashed #ccc }
  > section { background: #eee }
  dl > {
    dt { color: #333 }
    dd { color: #555 }
  }
  nav + & { margin-top: 0 }
}
```

```css
article ~ article { border-top: 1px dashed #ccc }
article > footer { background: #eee }
article dl > dt { color: #333 }
article dl > dd { color: #555 }
nav + article { margin-top: 0 }
```

<br>

## @import 导入

### @import

我们可以创建一些文件，将 CSS 代码模块化。

然后再对于不同的页面，创建一个 scss 文件，将需要的模块 import 进来。

Sass 编译会自动整合 import 的代码插入到该文件对应的位置中。

语法：

```scss
@import filename;
```

> ⚠**注意**：filename 不包含`.scss`后缀。

<br>

### Partials

你可以在文件名的开头添加一个下划线（`_`），这将告诉 Sass 不要将其编译为一个 CSS 文件。

开头带有下划线的文件可以被 import，但不会被单独编译。

导入该文件时，文件名前面不需要加下划线。

> ⚠**注意**：请不要将带下划线与不带下划线的同名文件放置在同一个目录下，比如，_colors.scss 和 colors.scss 不能同时存在于同一个目录下，否则带下划线的文件将会被忽略

<br>

### 原生 CSS 导入

`.scss`文件可以将多个`.css`文件经过编译后生成一个`.css`文件，这减少了浏览器请求次数，提高了加载效率。

但如果在`.scss`文件中 import 的是一个`.css`结尾的文件，SCSS 会调用 CSS 原本就自带的`@import`语句（在 SCSS 中为`CSS@import`），造成额外的浏览器下载请求。

由于 SCSS 可以直接兼容 CSS，故将文件/url 后缀更改为`.scss`即可。

<br>

## 静默注释

```scss
body {
  color: #333; // 这种注释内容不会出现在生成的css文件中
  padding: 0; /* 这种注释内容会出现在生成的css文件中 */
}
```

## @mixin 混合宏

### @mixin

`@mixin`指令允许我们定义一个可以在整个样式表中重复使用的样式。

语法：

```scss
@mixin minin-name { 
  property: value; 
  property: value;
  ...
}
```

> mixin 有多种翻译：混合宏、混合器、混合、混入......皆是指 mixin。

<br>

### @include

`@include`指令可以将混合宏引入到文档中。

语法：

```scss
selector {
  @include mixin-name;
}
```

Sass 代码：

```scss
@mixin important-text {
  color: red;
  font-weight: bold;
}

.danger {
  @include important-text;
  background-color: green;
}
```

转换效果：

```css
.danger {
  color: red;
  font-weight: bold;
  background-color: green;
}
```

混合宏中可以 include 其他的混合宏。

```scss
@mixin special-text {
  @include important-text;
  @include special-border;
}
```

<br>

### 参数输入

混合宏接受参数输入：

```scss
@mixin bordered($color, $width) {
  border: $width solid $color;
}

// 省略参数名，按顺序输入
.article {
  @include bordered(blue, 1px);
}

// 指定参数名，无需顺序输入
.card {
  @include bordered(
    $width: 1px,
    $color: blue
  );
}
```

<br>

### 参数默认值

参数支持设置默认值：

```scss
@mixin bordered($color: blue, $width: 1px) {
  border: $width solid $color;
}
```

<br>

### 常见用途

**对浏览器前缀使用混合宏**是一个常见的使用方式，比如`transform`：

```scss
@mixin transform($property) {
  -webkit-transform: $property;
  -ms-transform: $property;
  transform: $property;
}

.myBox {
  @include transform(rotate(20deg));
}
```

或者是一个圆角效果：

```scss
@mixin border-radius($radius) {
    -webkit-border-radius: $radius;
    -moz-border-radius: $radius;
    border-radius: $radius;
}

.element1 {
    @include border-radius(5px);
}

.element2 {
    @include border-radius(10px);
}
```

<br>

### 可变参数

当输入的参数个数不确定时，使用`...`可以用来设置可变参数。

例子：

```scss
@mixin box-shadow($shadows...) {
      box-shadow: $shadows;
}

.shadows {
  @include box-shadow(0px 4px 5px #666, 2px 6px 10px #999);
}
```

转换结果：

```css
.shadows {
  box-shadow: 0px 4px 5px #666, 2px 6px 10px #999;
}
```

<br>

## @extend 继承

```scss
.btn {
  border: none;
  text-align: center;
  cursor: pointer;
}

.btn-report {
  @extend .btn;
  background-color: red;
}

.btn-submit {
  @extend .btn;
  background-color: green;
}
```

结果：

```css
.btn,
.btn-report,
.btn-submit {
  border: none;
  text-align: center;
  cursor: pointer;
}

.btn-report {
  background-color: red;
}

.btn-submit {
  background-color: green;
}
```

使用 @extend 后，我们在 HTML 按钮标签中就不需要指定多个类 `class="btn btn-report"`，只需要设置 `class="btn-report"`就好了。

> ⭕ **Tips**: 
> 
> 相比于混合宏，继承实现了代码复用（混合宏则产生了代码冗余），这是一个优秀的特性。
> 
> 但混合宏能够传递参数，这点要优于继承。

<br>

### % 占位符

`%`开头的命名只能被继承，不会单独存在。

```scss
%btn {
  border: none;
  text-align: center;
  cursor: pointer;
}

%unused {
  padding: 4px;
}

.btn-report {
  @extend %btn;
  background-color: red;
}

.btn-submit {
  @extend %btn;
  background-color: green;
}
```

转换后：

```css
.btn-report,
.btn-submit {
  border: none;
  text-align: center;
  cursor: pointer;
}

.btn-report {
  background-color: red;
}

.btn-submit {
  background-color: green;
}
```


<br>

## 函数

暂略

> https://www.runoob.com/sass/sass-functions.html

<br><br>

---

## 本文参考

- Sass 教程 | 菜鸟教程 <https://www.runoob.com/sass/sass-tutorial.html>
- Sass 快速入门 | Sass 中文网 <https://www.sass.hk/guide/>
- SCSS 教程 - 简书 <https://www.jianshu.com/p/a99764ff3c41>
