---
title: "Objects 对象基础（2）"
date: "2019-08-16"
---

# JavaScript | Objects 对象基础（2）

介绍`JavaScript`中的`Objects`对象的语法及相关特性。

> 本篇内容对于新手而言可能相对较为难以理解，建议日后在实践中加深关于本篇内容的理解

## 目录 <!-- omit in toc -->

- [对象方法](#对象方法)
- [“this”](#this)
- [构造函数](#构造函数)
  - [定义规则](#定义规则)
  - [构造函数的 return 规则](#构造函数的-return-规则)
  - [new 操作符](#new-操作符)
  - [其他](#其他)
- [回调函数中的 this](#回调函数中的-this)

<br>

---

<br>

## 对象方法

我们经常称定义于对象中的函数为“方法”，这是出于这个函数在这个对象中所扮演的角色的的称呼，而“函数”则是它的性质。

比如对于一个“人”（对象），“走路”是它的一种行为，而定义“如何走路”便是“走路”这个行为所定义的方法：双腿交替迈开（函数内的代码）。

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

在讲构造函数创建对象之前，我们先简单介绍一下`this`。

如果有学过其他编程语言，你可能会察觉到 JavaScript 中的“`this`”关键字与其他大多数编程语言不太相同。

比如，JavaScript 的`this`可以用于任何函数而不会报语法错误。

```js
function sayHi() {
  alert( this.name );
}
```

这是因为，JavaScript 的`this`在运行时才求值，其值由调用该函数的“.”**点之前的对象**决定。

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

但如果在没有任何对象调用该函数，严格模式下的`this`等于`undefined`，这时候如果访问属性则会出错；非严格模式下的`this`将会是全局对象，即`window`。

我们不应该在没有对象的情况下调用`this`，这一般是错误的。

<br>

## 构造函数


JavaScript 早期时候虽然没有“类”的概念，但我们可以借助**构造函数**来达到我们相似的效果，实现对象结构的复用。

*在现代 JavaScript 中已经有 class 语法了，其本质仍然是一种特殊的函数。*

### 定义规则

构造函数在技术上与一般的函数没有区别，但我们约定：

1. 大写字母开头
2. 只能使用`new`操作符执行

例子：

```js
function User(name) {
    // this = {};（隐式创建）
    this.name = name;
    this.isAdmin = false;
    this.sayHi = function() {
        alert("Hello");
    };
    // return this;（隐式返回）
}
let Haze = new User("Haze");

// 结构等价于
let user = {
    name: "Haze",
    isAdmin: false,
    sayHi: function() {
        alert("hello");
    }
};
```

### 构造函数的 return 规则

一般来说都让它隐式返回`this`，如果显式`return`，则有以下规则：

- 如果返回一个对象，则返回该对象，不返回`this`
- 如果返回其他东西，则忽略，仍然返回`this`

### new 操作符

上面的例子中，隐式创建空对象与隐式返回`this`都是`new`的作用。

> 使用`new`操作符调用函数，会自动执行以下步骤：
> 
> 1. 创建一个全新的对象
> 2. 这个对象会被执行`[[Prototype]]`链接，将原型实例化（不懂可先忽略该行）
> 3. 生成的新对象会绑定到函数调用的`this`上
> 4. 如果函数没有返回对象类型，那么`new`表达式中的函数调用会自动返回这个新的对象

在函数内部，我们可以使用`new.target`属性来检查该函数被调用时是否使用了`new`操作符：

- 带 `new`，返回该函数（即 `function Func { ... }`）
- 不带 `new`，则返回 `undefined`

这样做使得构造函数的调用变得安全，不会被误调用为普通函数。

### 其他

- 由`new.target`的特性，我们还可以延伸出一个小 trick。

  当调用时没有使用`new`操作符，自动帮忙补上：

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

  但该方法非常不推荐使用，因为不利于阅读。

- 对于以下对象，我们可以使用其他方法代替使用 `new` 创建对象：

  | 符号          | 替代           |
  | ------------- | -------------- |
  | {}            | new Object()   |
  | ""            | new String()   |
  | 0             | new Number()   |
  | false         | new Boolean()  |
  | []            | new Array()    |
  | /()/          | new RegExp()   |
  | function (){} | new Function() |

- JavaScript 为我们内置了许多常用的对象的构造函数，如日期`Date`、集合`Set`以及数组`Array`。

- 当构造函数没有参数时，语法上是支持省略括号的：

  ```js
  let user = new User;  // 等价于 new User();
  ```

  但从代码风格角度上并不推荐这么做。

<br>

## 回调函数中的 this

对于一个对象而言，我们很可能经常需要使用回调函数去改变自身的某个属性。下面看一个例子：

```js
function Num() {
    this.value = 42;
    this.delayOutput = function() {
        setTimeout(function () {      // 回调函数
            console.log(this.value);  // 这里有没有错误？
        }, 1000);
    }
}

let num = new Num();
num.delayOutput();
```

按照直观上的感觉，我们的`setTimeout`对一个匿名函数进行了1秒定时的回调，回调函数中会输出`this`所指向的也就是`Num`对象的`value`值，所以一秒之后控制台会输出`42`。

但这是不对的。按照这么执行的结果，我们会得到一个`undefined`。这是为什么呢？

这是因为，`this`在匿名函数/箭头函数中有不同的表现：

- **匿名函数 `function() {...}` 的命名空间处于全局对象上**，所以匿名函数的`this`会等于`undefined`（严格模式下）或者`window`（非严格模式下）
- 箭头函数 `() => {}` 自身没有`this`，在**箭头函数内访问`this`会取得来自外部上下文中的`this`值**

从这一点出发，上面的例子中的回调函数中的`this`实际上指向的是`window`全局对象，因为`window`上没有`value`属性，所以输出`undefined`。

所以在需要使用`this`的情况下，请不要使用匿名函数。

而在这一点上，使用箭头函数作为对象的方法需要用到的回调函数则非常合适，因为它正好指向了箭头函数所处上下文的对象。在上面的例子中，匿名函数的外部上下文就是`Num`中，实例化后就是`num`对象。所以上例将匿名函数改为箭头函数，即可正常运行：

```js
function Num() {
    this.value = 42;
    this.delayOutput = function() {
        setTimeout(() => console.log(this.value), 1000);  // 箭头函数
    }
}

let num = new Num();
num.delayOutput();

// 一秒后：
// 42
```

不过，因为箭头函数没有自己的`this`的问题，我们并不适合使用箭头函数定义需要使用到`this`的对象方法（这里的对象是指不是使用`new`操作符创建的对象，而是使用字面量创建的对象），因为这个时候，`this`不会指向对象本身，而是指向调用者的“上一级”比如`window`。

```js
const num = {
    value: 42,
    output: () => console.log(this.value)
};

num.output();  // undefined
// output()中的this没有指向"."之前的num
```

如果是使用`new`操作符创建的对象，因为前面讲到的：`new`操作符会将新生成的对象绑定到函数的`this`上，所以在构造函数中使用箭头函数定义对象方法是没有问题的。

总结一下：

- 匿名函数的`this`为`undefined`或者`window`
- 箭头函数的`this`来自箭头函数的外部的上下文
- 如果要使用`this`，请使用箭头函数

另附`this`的完整规则流程图，以便日后查阅：

![this 规则.jpg](https://i.loli.net/2020/02/19/mD6cStKphJBVCzy.jpg)
