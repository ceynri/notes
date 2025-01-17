---
title: "JavaScript 入门基础"
date: "2019-08-12"
---

# JavaScript | 入门基础

从 C、Java 语言到 JavaScript 语言的过渡笔记，以非零基础角度对JavaScript的基础语法内容及其特性进行适当的精炼所记录下的笔记，会省略或快速带过与Java和C语言相类似的部分内容。

## 目录 <!-- omit in toc -->

- [在网页中插入 JavaScript 代码](#在网页中插入-javascript-代码)
- [定义变量](#定义变量)
- [现代模式 / 严格模式](#现代模式--严格模式)
- [模态窗交互](#模态窗交互)
- [数据类型](#数据类型)
  - [1. number 类型](#1-number-类型)
  - [2. string 类型](#2-string-类型)
  - [3. boolean 类型](#3-boolean-类型)
  - [4. “null” 值](#4-null-值)
  - [5. “undefined” 值](#5-undefined-值)
  - [6. object 类型](#6-object-类型)
  - [7. symbol 类型](#7-symbol-类型)
- [类型转换](#类型转换)
  - [转换为 string](#转换为-string)
  - [转换为 number](#转换为-number)
  - [转换为 boolean](#转换为-boolean)
- [值的比较](#值的比较)
  - [字符串比较](#字符串比较)
  - [不同类型比较](#不同类型比较)
  - [严格相等](#严格相等)
  - [特殊值](#特殊值)

<br>

---

<br>

## 在网页中插入 JavaScript 代码

在HTML文档中，可以使用`<script>`标签包裹javaScript代码，可选src属性。

```html
<html>
<head>
    <script src="xxx"></script>
    <script>
        // 脚本代码
    </script>
</head>
<body>
    <!-- 网页内容 -->
</body>
</html>
```

更多内容会在第二章节介绍。

<br>

## 定义变量

我们可以通过使用 `var`、`let` 或者 `const` 来声明变量来存储数据。

- `let` – 新的变量声明方式。Chrome（V8）中代码必须开启严格模式才能使用。
- `var` – 旧的变量声明方式。很多相对不够新的教程、书籍仍然使用`var`声明变量。
- `const` – 声明常量。

JavaScript 的变量命名有两个限制：

1. 变量名称必须仅包含字母，数字，符号 `$` 和 `_`。
2. 首字符必须非数字。

::: tip

`var`声明的变量没有块级作用域，它会在整个函数/全局可见，所以后来会被`let`所取代。

详细可见：[旧时的“var”](https://zh.javascript.info/var)

:::

<br>

## 现代模式 / 严格模式

使用"use strict"使得编写的脚本文件以现代模式进行工作。

```js
"use strict";

// 脚本代码...

```

确保`"use strict"`出现在整个脚本或者某个函数内容的最顶部。

`use strict`模式无法取消。

本笔记绝大部分代码均以严格模式为准。

<br>

## 模态窗交互

**alert(message)**

浏览器会弹出一段信息并暂停脚本，直到用户点击了“确定”。

弹出的小窗口被称为**模态窗**。

**prompt(title[, default])**

显示信息要求用户输入文本。点击确定返回文本，点击取消或按下 <kbd>Esc</kbd> 键返回 `null`。

| 参数      | 作用                            |
| --------- | ------------------------------- |
| `title`   | 显示给用户的文本                |
| `default` | 可选参数，指定 input 框的初始值 |

`prompt` 返回输入的文本；如果取消输入就返回 `null`。

建议始终提供`default`以兼容IE，否则他会无聊地提供一个`undefined`。

```js
let test = prompt("Test", ''); // <-- for IE
```

**confirm(question)**

显示信息等待用户点击确定或取消。点击确定返回 `true`，点击取消或 <kbd>Esc</kbd> 键返回 `false`。

<br>

## 数据类型

JavaScript 一共有**七种**基本数据类型。

- number 用于任何类型的数字：整数或者浮点数。
- string 用于字符串。一个字符串可以包含一个或多个字符，所以没有单独的单字符类型。
- boolean 用于 true 和 false。
- null 用于未知的值 —— 只有一个 null 值的独立类型。
- undefined 用于未定义的值 —— 只有一个 undefined 值的独立类型。
- object 用于更复杂的数据结构。
- symbol 用于唯一的标识符。

其中，object 不属于原始类型，所以原始类型目前只有六种。

> 大多数语言都具有的`Array`数组，在JavaScript中属于对象类型，放在[以后的章节](./array.md)介绍。

### 1. number 类型

特殊值：`Infinity`、`-Infinity`、`NaN`

javaScript 是算术安全的。

### 2. string 类型

1. 双引号： `"Hello"`
2. 单引号： `'Hello'`
3. 反引号： <code>\`Hello\`</code>

双引号和单引号都是简单引用，在 JavaScript 中两者没有差别。

推荐使用 `'` 而不是 `"`，因为不用按 `Shift`。

HTML 文档则使用 `"`，使得在 js 文件中以字符串形式编写 HTML 而无需对引号进行转义。

引号换行需要在最后添加`反斜杠`（`\`），但某些浏览器可能不支持，建议使用`数组`或 `+` 连接字符串：

```js
let str = "这是一个\
        换行的字符串";

let str2 = "这是一个" +
        "换行的字符串";

let str3 = [
    "这是一个",
    "换行的字符串";
].join('');

// 结果："这是一个换行的字符串"
```

反引号是功能扩展的引用，允许通过 `${…}`，将变量和表达式嵌入到字符串中。例如：

```js
let name = "Haze";

// 嵌入变量
alert( `hello, ${name}!` ); // 输出：“hello, Haze!”

// 嵌入表达式
alert( `结果为 ${1 + 2}` ); // 输出“结果为 3”
```

反引号支持多行字符串，且会保留换行符：
```js
let paragraph =
`Dear Haze:

How r u?
I m 5.

        Yours,
        Ceynri`

alert(paragraph);

/* 输出结果：
Dear Haze:

How r u?
I m 5.

        Yours,
        Ceynri
*/
```

### 3. boolean 类型

`true` 和 `false`。

### 4. “null” 值

“无”、“空”、“值未知”的特殊值。

### 5. “undefined” 值

未被赋值。

### 6. object 类型

对象类型。

其中，Array 对象便是我们经常使用到的对象类型。

### 7. symbol 类型

创建对象的唯一标识符。（symbol 是一个比较底层的类型，可以稍微晚一点再了解）

### typeof 运算符 <!-- omit in toc -->

`typeof` 运算符返回参数的类型。

它支持两种语法形式：

1. 作为运算符：`typeof x`
2. 函数形式：`typeof(x)`

例子：

```js
typeof undefined    // "undefined"

typeof 0            // "number"

typeof true         // "boolean"

typeof "foo"        // "string"

typeof Symbol("id") // "symbol"

typeof Math         // "object"

typeof null         // "object"

typeof alert        // "function"
```

最后三行的额外说明：  

> - Math 是一个提供数学运算的内建对象，此处作为一个对象的例子。  
> - typeof null 的结果是 "object"是官方在 typeof 方面承认的错误。  
> - typeof alert 的结果是 "function"，但在语言中没有一个特别的 “function” 类型，函数实际上隶属于 object 类型，只不过 typeof 会对函数区分对待。这不正确，但在实践中非常方便。

<br>

## 类型转换

### 转换为 string

```js
num + '';  // 性能最好
String(value);
value.toString();
```

// TODO

### 转换为 number

在算术函数和表达式中，会自动进行 number 类型转换。

```js
alert("6" / "2");   // 3
```

注：加号‘+’是例外，其中一个运算元为字符串时，会将另外的运算元也转换为字符串然后连接起来（被称为“级联”）。

```js run
alert(1 + "2"); // "12"
alert(1 - "2"); // -1
```

如果只有单独一个字符串前面加上一个“`+`”，那么该字符串会转换为数字。

```js
alert(+"123"); // 123
```

也可以使用 Number(value) 显式地转换为 number 类型（但更推荐使用 `+` 的做法，性能更好）。

```js
let num = Number("123");
```

如果字符串不是一个有效的数字，转换的结果会是 `NaN`。

其他原始类型对 number 类型的转换表：

| 输入                    | 输出                              |
| ----------------------- | --------------------------------- |
| undefined               | NaN                               |
| null                    | 0                                 |
| true 和 false           | 1 and 0                          |
| string 纯数字           | 对应数字 （输入的首尾可以有空格） |
| string 纯空格、空字符串 | 0                                 |
| string 不是纯数字       | NaN                               |

string 例子：

```js
alert( Number("   123   ") );   // 123
alert( Number(" "));            // 0
alert( Number("1 2 3") );       // NaN
alert( Number("123z") );        // NaN
alert( Number("+123") );        // 123
alert( Number("-123") );        // -123
```

### 转换为 boolean

可以使用 `!!`

```js
let num = 3.14;
!!num;

// 或者显式转换
Boolean(num);
```

在比较时，其他类型会自动转换为 boolean 类型。

| 值                                            | 结果    |
| --------------------------------------------- | ------- |
| 假值（`0`、`""`、`null`、`undefined`和`NaN`） | `false` |
| 其他                                          | `true`  |

> 注意，`"0"`字符串也是`true`。

<br>

## 值的比较

### 字符串比较

判定规则：

> 1. 比较两个字符串的首位字符大小。
> 2. 两个字符串中的字符相等则继续取出各自的后一位字符进行比较。
> 3. 重复上述步骤进行比较，直到某字符串率先用完所有字符。
> 4. 如果两个字符串同时用完字符，那么它们被判定为相等，否则未结束（还有未比较的字符）的字符串更大。

简单的说就是先依次比较高位字符大小，再比较字符串长度。

例子：

```js
alert( "Za" > "Az" );       // true
alert( "Glow" > "Glee" );   // true
alert( "Bee" > "Be" );      // true
```

### 不同类型比较

string与boolean类型自动转换为number类型。

### 严格相等

普通的相等性检查 `==` 会自动转换类型。（如 `0 == false` 为 `true`）

**严格相等操作符 `===` 在进行比较时不会做任何的类型转换。**

对应的不等号为 `!==`

### 特殊值

对于特殊值null与undefined，`==` 与其他比较方法（ `> < >= <=` ）有不同的判断机制。

```js
alert( null > 0 );  // false
alert( null == 0 ); // false
alert( null >= 0 ); // true
```

`undefined` 和 `null` 只会互等，不等于其他值。

```js
alert( null === undefined ); // false
alert( null == undefined ); // true
```

<br>

## 运算符 <!-- omit in toc -->

注意幂运算符 `**`，其他类同。

*略*

<br>

## switch 语句 <!-- omit in toc -->

与`java`不同，`javaScript`的`switch`语句的`case`语句支持表达式、变量。

*略*
