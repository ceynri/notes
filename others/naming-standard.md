---
title: 命名规范
date: 2019-09-24
sidebar: true
---

# 命名规范

个人为统一代码等行文风格所规定的一些命名规范。

## 常见命名法

- camelCase 驼峰命名法  
  单词连在一起，第一个词首字母小写、其他词首字母大写

- PascalCase 帕斯卡命名法  
  单词连在一起，每个单词首字母都大写（又称大驼峰命名法）

- underscore_case 下划线命名法  
  每个单词用下划线（`_`）连接起来

- kebab-case 短横线命名法  
  作为变量名的连字符（`-`）在很多编程语言里不被支持，但作为 HTML 属性/特性名或者文件名常用

- UPPER_CASE 全部大写  
  一般来说常量表示基本都用这个方式，单词之间用下划线连接

- hungarian 匈牙利命名法  
  变量名=属性+类型+对象描述，每一部分的名称都要求有明确含义。放在最后面存粹是我不喜欢+过时

<br/>

## 字段

| 语言       | 变量            | 常量       | 函数/方法       | 类/对象    |
| ---------- | --------------- | ---------- | --------------- | ---------- |
| Java       | camelCase       | UPPER_CASE | camelCase       | PascalCase |
| C          | underscore_case | UPPER_CASE | camelCase       | PascalCase |
| JavaScript | camelCase       | UPPER_CASE | camelCase       | PascalCase |
| Python     | underscore_case | UPPER_CASE | underscore_case | PascalCase |

> 注：在 JavaScript 中，因为定义一个常量只需使用 const 写起来很简单，我个人习惯对于不会改变的量都会用 const 代替 let，从而避免误修改。
> 
> 但我仍然使用 camelCase 命名这些 const 变量，因为它们大多数都不会被反复使用，只是一个中间变量。
> 
> 而对于会被反复使用的、用来代替某字面量的“常量”，我会使用绝大部分语言都通用的 UPPER_CASE 进行命名，这非常直观。
<br/>

## 前端

### id / class

- `class` 采用连字符连接 `.class-name`
- `id` 采用驼峰命名法 `#idName`

理由：

- `class` 常用于样式，`id` 则专门配给 JavaScript 为佳。故 class 按照 css 属性命名风格使用连字符，id 按照 JavaScript 风格使用 camelCase。
- `class-name` 也可以是 `class_name`，依个人喜好而定。

<br/>

### 引号

- HTML 属性名不加引号，属性值都加双引号。

    属性值不加引号有些时候也能运行但并不规范（是被自动检测补全的），而且如果一个属性有多个值则必须加引号。

    使用双引号而非单引号是因为便于其他编程语言（如 PHP、JavaScript）在写 HTML 文本时无需转义引号（如果你在这些语言中使用单引号包裹字符串的话）。

- CSS 字符串用双引号。

- JavaScript（等编程语言）字符串用单引号。

<br/>

### 其他注意点

- 在 JavaScript 中，连字符连接的词组无法作为变量名/属性名，所以某些情况使用 javacript 操纵 HTML 时需要注意。
- 在 HTML DOM 与 JavaScript 之间的某些操作，会出现 JavaScript 定义的 camelCase 自动转换为 kebab-case，反之类同。

> ❓**大小写敏感性问题**
>
> - HTML 自己不区分大小写
> - CSS 对 HTML 的 id、class 区分大小写；标签选择器、属性名、属性值不区分大小写
> - JavaScript 对 HTML 的 Id、ClassName 大小写敏感，对 TagName 不敏感
>
> 所以 HTML 文档内容编写要规范😿

<br/>

## 文件 / 文件夹

文件名使用连字符连接。

很多公司在这方面并没有统一，首字母大小写混用、或者用空格分隔词也常见。

<br/>

### 分词符

如何选择`-`与`_`：

- 断词：在大部分编辑器中，`-`可以作为分词符，而`_`不会分词，将几个词看成一个整体。主要体现在双击某个单词时是否会选中整个变量名。
- 快速选中：对于由`-`连接的变量如果想要快速选中整个变量名，可以双击其中一个单词后拖动。
- 输入效率：键入`_`需要按住<kbd>Shift</kbd>而`-`不用。（在这一点上，camelCase 甚至不用多打一个字符，所以个人觉得更爽）
- 【此条存疑】有些规范为了专门区分 CSS 属性（`-`连接）与变量名，使用`_`作为词的连接符。
- 可读性：`-`比`_`更显眼，不会那么容易被误认为空格。
- SEO：由于`-`能分隔词的特性，被断开的词都可以作为关键词，这在 SEO 表现上会比`_`更好。
- 语法：对于许多编程语言（如 Java、Python）来说，变量名不允许用`-`连接，故如果有需要的情况可以考虑在文件命名等方面统一选择`_`作为断词符。

<br/>

### 常用文件夹命名

| 名字              | 简写               | 存放内容                              |
| ----------------- | ------------------ | ------------------------------------- |
| src               | source             | 源代码                                |
| lib/dep           | library/dependence | 引入的第三方库（jquery）              |
| bin               | binary             | 二进制文件                            |
| docs              | document           | 需求文档，开发文档                    |
| dist/build        | distribution/build | 最终发布的代码（或软件）              |
| examples/demo     |                    | 实例                                  |
| asset             |                    | 资源（图片、音乐）                    |
| static            |                    | 静态资源（html、js、css、图片、音乐） |
| common/public     |                    | 公共资源（公共图片，公共音乐，公共）  |
| tpl               | template           | 模板文件（jade、ftl）                 |
| conf              | config             | 配置文件（xml、json）                 |
| util/tools        |                    | 工具（工具类库）                      |
| logs              |                    | 日志文件                              |
| temp/tmp          | temporary          | 临时文件（缓存文件）                  |
| test/\_\_test\_\_ |                    | 单元测试文件                          |
| client            |                    | 前端源代码                            |
| server            |                    | 后端端源代码                          |

<br/>

### 项目

项目名使用 PascalCase。

但在发布时（如存储到 github 公开仓库），推荐使用 kebab-case，有利于 SEO。

<br/>

### 文档

全角字符与半角字符之间一定要用空格，如 English word 与中文之间。

参见 [盘古之白](https://github.com/vinta/pangu.js)

![pangu.png](https://i.loli.net/2019/09/25/U9SFcQgHMPv7Z8I.png)

<br/>

### 语义化版本

使用语义版本号来管理代码：语义版本号分为 X.Y.Z 三位，分别代表主版本号、次版本号和补丁版本号。当代码变更时，版本号按以下原则更新：

- 如果只是修复bug，需要更新Z位
- 如果是新增了功能，但是向下兼容，需要更新Y位
- 如果有大变动，向下不兼容，需要更新X位

除此以外还可以添加诸如 Alpha、Beta 等测试版本标识。

> 详细规定：<https://semver.org/lang/zh-CN/>

<br/>
