---
title: "Objects 对象基础（2）"
date: "2019-08-16"
---

# JavaScript | Objects 对象基础（2）

介绍`JavaScript`中的`Objects`对象的语法及相关特性。

## 目录 <!-- omit in toc -->

- [对象方法](#对象方法)
- [“this”](#this)
- [原始值转换](#原始值转换)
- [构造函数](#构造函数)
  - [new 操作符](#new-操作符)
  - [构造函数 return 规则](#构造函数-return-规则)

<br>

---

<br>

## 对象方法

创建对象方法的几种方式：

```js
// 1. 直接赋值
user.sayHi = function() {
  alert("Hello!");
};

// 2. 先声明后赋值
function sayHi() {
  alert("Hello!");
};

user.sayHi = sayHi;

// 3. 对象内赋值
let user = {
  sayHi: function() {
    alert("Hello");
  }
};

// 4. 方法简写
let user = {
  sayHi() {
    alert("Hello");
  }
};
```

一般来说3与4较为正常，而4在绝大部分情况下都与3没有区别。故推荐使用第4种方法。

<br>

## “this”

JavaScript中的“`this`”关键字与其他大多数编程语言不太相同。

this可以用于任何函数而不会报语法错误。

```js
function sayHi() {
  alert( this.name );
}
```

因为`this`在运行时才求值，其值由调用该函数的“.”**点之前的对象**决定。

```js
let user = { name: "John" };
let admin = { name: "Admin" };

function sayHi() {
  alert( this.name );
}

user.f = sayHi;
admin.f = sayHi;
// 函数在两个对象之间共用

user.f();     // John  (this == user)
admin.f();    // Admin  (this == admin)

admin['f'](); // Admin（使用方括号亦可）
```

在没有任何对象的情况下，严格模式的`this`等于`undefined`，这时候如果访问属性则会出错；非严格模式的`this`将会是全局对象，即浏览器窗口。

我们不应该在没有对象的情况下调用`this`，这一般是错误的。

::: warning `this`在匿名函数/箭头函数中有不同的表现：

匿名函数的`this`表现得像是没有依附对象的`this`，会等于`undefined`或者`window`。所以在需要使用`this`的情况下，请不要使用匿名函数。

箭头函数自身没有`this`，在箭头函数内访问`this`会取得来自外部的`this`值，所以不适合使用箭头函数定义对象方法（`this`不会指向调用者本身，而是指向调用者的“上一级”比如`window`）。

但在一般情况下，使用箭头函数作为对象的方法需要用到的**回调函数**则非常合适，因为它正好指向了该对象本身，而不是调用者（调用该回调函数的方法所属的对象）。

当然，如果你并不期望这样的结果，就不应该在这种情况下使用箭头函数了。

:::

<br>

## 原始值转换

本小节以下内容从原文摘抄。（因为我不知道用不用的上）

> 对象到原始值的转换，是由许多内置函数和操作符自动调用的，这些函数使用一个原始值作为返回值的。
>
> 它有三种类型（暗示）：
>
> - "`string`"（对于 alert 和其他字符串转换）
> - "`number`"（对于 maths）
> - "`default`"（少数操作）
>
> 规范明确描述了哪个操作符使用哪个暗示。极少数操作者“不知道期望什么”并使用 "`default`" 暗示。通常对于内置对象，"`default`" 暗示的处理方式与 "`number`" 相同，因此在实践中最后两个通常合并在一起。

> 转换算法：
>
> 1. 调用 `obj[Symbol.toPrimitive](hint)` 如果这个方法存在的话，
> 2. 否则如果暗示是 "`string`"
>     - 尝试 `obj.toString()` 和 `obj.valueOf()`，无论哪个存在。
>     - 否则，如果暗示 "number" 或者 "default"
> 尝试 `obj.valueOf()` 和 `obj.toString()`，无论哪个存在。
>
> **在实践中，为了记录或调试目的，仅实现 `obj.toString()` 作为“全捕获”方法通常就够了，这样所有转换都能返回一种“人类可读”的对象表达形式。**

<br>

## 构造函数

`JavaScript`早期时候虽然没有“类”的概念，但我们可以借助**构造函数**来达到我们相似的效果，实现对象结构的复用。

*在现代JavaScript中已经有class语法了，其本质仍然是一种函数。*

构造函数在技术上与一般的函数没有区别，但我们约定：

1. 大写字母开头
2. 只能使用`new`操作符执行

例子：

```js
function User(name) {
  // this = {};（隐式创建）
  this.name = name;
  this.isAdmin = false;
  this.sayHi = new function() {
    alert("Hello");
  };  // <-- 不要漏了这个分号
  // return this;（隐式返回）
}
let Haze = new User("Haze");

// 结构等价于
let user = {
  name: "Haze",
  isAdmin: false,
  sayHi: new function() {
    alert("hello");
  }
};
```

### new 操作符

上面的例子中，隐式创建空对象与隐式返回`this`都是`new`的作用。

在函数内部，我们可以使用`new.target`属性来检查该函数被调用时是否使用了`new`操作符：

- 带 `new`，返回该函数（即 `function Func { ... }`）
- 不带 `new`，则返回 `undefined`

由此可以延伸出一个小trick（但不推荐使用，因为不利于阅读）：

```js
function User(name) {
  if (!new.target) {          // 如果没有运行 new
    return new User(name);    // 自动补上 new
  }
  this.name = name;
}

let john = User("John");
let john = new User("John");  // 相同
```

对于以下对象，我们建议使用其他方法代替使用 `new` 创建对象：

| 符号          | 替代           |
| ------------- | -------------- |
| {}            | new Object()   |
| ""            | new String()   |
| 0             | new Number()   |
| false         | new Boolean()  |
| []            | new Array()    |
| /()/          | new RegExp()   |
| function (){} | new Function() |


### 构造函数 return 规则

一般来说都让它隐式返回`this`，如果显式`return`，则有以下规则：

- 如果返回一个对象，则返回该对象，不返回this
- 如果返回其他东西，则忽略，仍然返回this

### 其他 <!-- omit in toc -->

- JavaScript 为我们内置了许多常用的对象的构造函数，如日期`Date`、集合`Set`以及数组`Array`。
- 当构造函数没有参数时，语法上是支持省略括号的：

  ```js
  let user = new User;  // 等价于 new User();
  ```

  但从代码风格角度上并不推荐这么做。
