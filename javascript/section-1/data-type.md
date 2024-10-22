---
title: "数据类型"
date: "2019-08-18"
---

# JavaScript | 数据类型 <!-- omit in toc -->

关于某些数据类型进行一些特性的介绍以及常用方法介绍。

## 目录摘要 <!-- omit in toc -->

- [变量类型](#变量类型)
- [数字 Number](#数字-number)
  - [parseInt 和 parseFloat](#parseint-和-parsefloat)
  - [舍入方法](#舍入方法)
  - [常量](#常量)
- [字符串 String](#字符串-string)
  - [查找子串](#查找子串)
  - [获取子串](#获取子串)

<br>

---

<br>

## 变量类型

### 基本类型 <!-- omit in toc -->

- 是原始类型中的一种值。
- 在 JavaScript 中有 6 种基本类型：`string`、`number`、`boolean`、`symbol`、`null` 和 `undefined`。

### 对象类型 <!-- omit in toc -->

- 能够存储多个值作为属性。
- 可以使用大括号 `{}` 创建对象

### 基本类型作为对象 <!-- omit in toc -->

除了null和undefined的基本类型可以调用一些方法，此时会临时创建一个包装对象，提供额外的功能，用完即销毁。实现“轻量级”特性。

如：`str.toUpperCase()`、`num.toFixed(n)`、`num.toString(base)`

<br>

## 数字 Number

### 科学记数法简写 <!-- omit in toc -->

`10000`可以写作`1e4`

### 其他进制 <!-- omit in toc -->

十六进制`0x`、八进制`0o`、二进制`0b`，其他进制使用parseInt转化为十进制。

### parseInt 和 parseFloat

对于日常情况，我们经常遇到非纯数字的字符串，为了优雅地从中提取数字，可以使用 `parseInt` 和 `parseFloat` 函数

```js
alert( parseInt('100px') );     // 100
alert( parseFloat('12.5em') );  // 12.5

alert( parseInt('12.3') );      // 12     读取整数部分
alert( parseFloat('12.3.4') );  // 12.3   读取到第二个小数点前
```

`parseInt` 支持不同进制的读取，这在很多时候（解析十六进制、二进制字符串）非常方便。

```js
parseInt(str, radix)
```

例子：

```js
alert( parseInt('0xff', 16) );  // 255
alert( parseInt('ff', 16) );    // 255
alert( parseInt('2n9c', 36) );  // 123456
```

### 舍入方法

| 方法       | 描述                     |
| ---------- | ------------------------ |
| Math.floor | 向下舍入                 |
| Math.ceil  | 向上舍入                 |
| Math.round | 四舍五入                 |
| Math.trunc | 只取整数部分（IE不支持） |

这些函数都是取整，如需要保留n位小数，则使用 `toFixed(precision)` 方法，或者先乘10<sup>n</sup>，舍完再除10<sup>n</sup>

| 方法          | 描述（都有一个可选的长度参数）               |
| ------------- | -------------------------------------------- |
| toExponential | 返回已被四舍五入并使用指数计数法的数字字符串 |
| toFixed       | 返回指定位小数位数的数字字符串               |
| toPrecision   | 返回指定长度的数字字符串                     |



### 常量

Number带有一些常用的数值属性，使用 `Number.XXXX` 进行访问。

| 属性              | 描述                           |
| ----------------- | ------------------------------ |
| MAX_VALUE         | 返回 JavaScript 中可能的最大数 |
| MIN_VALUE         | 返回 JavaScript 中可能的最小数 |
| NEGATIVE_INFINITY | 表示负的无穷大（溢出返回）     |
| NaN               | 表示非数字值（"Not-a-Number"） |
| POSITIVE_INFINITY | 表示无穷大（溢出返回）         |

### 其他函数 <!-- omit in toc -->

- `isFinite` 和 `isNaN`
- `Math.random()`
- `Math.max(a, b, c...)` 和 `Math.min(a, b, c...)`

<br>

## 字符串 String

### 引号 <!-- omit in toc -->

反引号内的内容大部分无需转义，且支持多行字符串。

### 转义字符 <!-- omit in toc -->

| 字符                        | 描述                                    |
| --------------------------- | --------------------------------------- |
| \\n                         | 换行                                    |
| \\r                         | 回车：不单独使用                        |
|                             | Windows文本文件使用 \r\n 组合表示换行符 |
| \\', \\"                    | 引号                                    |
| \\\                         | 反斜线                                  |
| \\t                         | 制表符                                  |
| \\xXX                       | 十六进制的 unicode XX                   |
| \\uXXXX                     | UTF-16 编码的十六进制 unicode 符号      |
| \\u{X…XXXXXX}（1到6个字符） | UTF-32 编码的十六进制 unicode 符号      |

### 查找子串

| 方法                           | 描述                                    |
| ------------------------------ | --------------------------------------- |
| `str.indexOf(substr, pos)`     | 顺序查找子串并返回位置                  |
| `str.lastIndexOf(subStr, pos)` | 从末尾（pos）开始倒着查找子串并返回位置 |
| `str.includes(substr, pos)`    | 是否包含子串并返回boolean值             |
| `str.startsWith(str)`          | 是否按某字符串开始                      |
| `str.endsWith(str)`            | 是否按某字符串结束                      |

### 获取子串

| 方法                           | 描述                         |
| ------------------------------ | ---------------------------- |
| `str.slice(start [, end])`     | 支持负值                     |
| `str.substring(start [, end])` | 不支持负值，支持start大于end |
| `str.substr(start [, length])` | 指定字符串长度而非结束位置   |

推荐使用slice方法。

### 其他 <!-- omit in toc -->

- `string`具有`length`属性（注意不是`length()`方法）
- 使用方括号获得字符串特定位置字符（或者`charAt(pos)`方法）
- `toLowerCase()` 和 `toUpperCase()` 实现大小写转换
- `str.localeCompare(str2)` 可以根据语言比较字符串而非字符代码大小
- `str.trim()` 删除字符串前后的空格
- `str.repeat(n)` 重复字符串n次
