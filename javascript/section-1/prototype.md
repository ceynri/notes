---
title: '原型'
date: 2020-07-27
---

# JavaScript | 原型

原型可谓是 JavaScript 区别于其他语言的非常重要的特性了，作为 JSer 不懂原型可能不一定会在做业务的时候遇到问题，但它仍然是每个学习 JS 的人的必修课，甚至可以用来判断一个人是否有真正系统地学习过 JavaScript。

这篇文章不深入讲解原型的细枝末节的语法特性，但求能理清原型的概念，与我们常见的基于类的面向对象语言进行一个对比与区分。

<br>

## 基本概念

原型，即 `prototype`，在 JavaScript 中任何的对象都有原型。

我们知道，对象可以由构造函数通过 new 进行创建，比如：

```js
function Person() {
  // ...
}
const lee = new Person();
```

`Person` 作为一个比较抽象的“模板”，实例化了一个具体的“人”。在这里，我们称 `lee` 具有原型，该原型就是 `[[prototype]]`，它来自 `Person.prototype`，`lee` 就是通过该原型而诞生的。

不过，当我们想要获取一个对象的原型时，`[[prototype]]` 是一个隐藏属性，而通过该对象的构造函数来访问 `prototype` 属性也并不方便，故浏览器为生成的对象们提供了 `__proto__` 的非正式属性，可以通过 `lee.__proto__` 去访问对象的 `[[prototype]]`。

> 虽然 `__proto__` 不是标准内的属性，但所有的浏览器都提供了它，所以我们一般仍使用它进行原型的概念讲解
>
> ES6 中已经出现 `Object.getPrototypeOf()` 与 `Reflect.getPrototypeOf()`，但本文并不讨论 `__proto__` 的相关问题

我们理清关系：

- 对象由构造器通过 `new` 得到，其原型来自于构造器的 `prototype`
- **构造器**的 `prototype` 属性是其生成的对象的`原型`
- **对象**通过 `__proto__` 属性访问自己的`原型`（`lee.__proto__ === Person.prototype`）

随着内容的增加，我们比较容易弄混 `__proto__` 与 `prototype`，所以一开始我们就要区分好：

- `prototype` 属于函数（构造器）的属性，它为每个实例化的对象指明了对应的原型。
- `__proto__` 属于对象的属性，通过它我们能够访问对象的原型。

## 为什么要有原型

我们先不讲原型链继承，也不讲类与原型的区别，首先我们要明白的，为什么要有“原型”这个概念。

我们知道，在写构造函数时，我们可以给 new 的对象直接添加方法属性：

```js
function Person() {
  this.say = function() {
    console.log('hi');
  };
}
new Person().say(); // hi
```

这时候

_TODO 以下未完成_
