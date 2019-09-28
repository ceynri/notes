---
title: "命名规范"
date: "2019-09-24"
---

# 命名规范

个人为统一代码等行文风格所规定的一些命名规范。

## 常见命名法

- camelCase 驼峰命名法  
  单词连在一起，第一个词首字母小写、其他词首字母大写

- PascalCase 帕斯卡命名法  
  单词连在一起，每个单词首字母都大写

- underscore_case 下划线命名法  
  每个单词用下划线（`_`）连接起来

- kebab-case 短横线命名法  
  作为变量名的连字符（`-`）在很多编程语言里不被支持，但作为 HTML 属性/特性名或者文件名常用

- UPPER_CASE 全部大写  
  一般来说常量表示基本都用这个方式，单词之间用下划线连接

- hungarian 匈牙利命名法  
  变量名=属性+类型+对象描述，每一部分的名称都要求有明确含义。放在最后面存粹是我不喜欢+过时

<br/>

## 变量

| 语言       | 变量            | 常量       | 函数/方法                       | 类/对象    |
| ---------- | --------------- | ---------- | ------------------------------- | ---------- |
| Java       | camelCase       | UPPER_CASE | camelCase                       | PascalCase |
| C          | underscore_case | UPPER_CASE | camelCase（有的人函数用Pascal） | PascalCase |
| JavaScript | camelCase       | UPPER_CASE | camelCase                       | PascalCase |

<br/>

## 前端

### id / class

- `class` 采用连字符连接 `class-name`
- `id` 采用 camelCase `idName`

理由：

- `class` 常用于样式，`id` 则专门配给 JavaScript 为佳。故 class 按照 css 属性命名风格使用连字符，id 按照 JavaScript 风格使用 camelCase。
- `class-name` 也可以是 `class_name`，依个人喜好而定。

<br/>

### 属性

HTML 属性名不加引号，属性值都加双引号。

原因：

- 属性值不加引号也能运行但并不规范（是被自动检测补全的）
- 使用双引号的原因是便于其他编程语言（如 PHP、JavaScript）在写 HTML 文本时无需转义引号（如果你在这些语言中使用单引号包裹字符串的话）。

<br/>

### 如何选择 `-` 与 `_`：

- 在大部分编辑器中，`-` 可以作为分词符而 `_` 不会分词，主要体现在双击某个单词时是否会选中整个变量名。
- 对于由 `-` 连接的变量如果想要快速选中整个变量名，可以双击其中一个单词后拖动。
- `_` 需要按住 <kbd>Shift</kbd> 而 `-` 不用。（在这一点上，camelCase甚至不用多打一个字符，所以更爽）
- 有些规范（包括某些大厂）为了专门区分 CSS 属性（`-` 连接）与变量名，使用 `_` 作为词的连接符。
- 对于可读性，`-` 比 `_` 更显眼，不会那么容易被误认为空格。

<br/>

### 其他注意点

- 在 JavaScript 中，连字符连接的词组无法作为变量名/属性名，所以某些情况使用 javacript 操纵 HTML 时需要注意。
- 在 HTML DOM 与 JavaScript 之间的某些操作，会出现 JavaScript 定义的 camelCase 自动转换为 kebab-case，反之类同。

::: tip 大小写敏感性问题

- HTML 自己不区分大小写
- CSS 对 HTML 的 id、class 区分大小写；标签选择器、属性名、属性值不区分大小写
- JavaScript 对 HTML 的 Id、ClassName 大小写敏感，对 TagName 不敏感

所以 HTML 文档内容编写要规范😿

:::

<br/>

## 文件

文件名使用连字符连接

<br/>

## 项目

项目名使用 PascalCase

也可以使用 kebab-case，各有所好。

<br/>

## 文档

全角字符与半角字符之间一定要用空格，如 English word 与中文之间。

参见 [盘古之白](https://github.com/vinta/pangu.js)

![pangu.png](https://i.loli.net/2019/09/25/U9SFcQgHMPv7Z8I.png)

<br/>
