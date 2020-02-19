---
title: "Symbol 类型"
date: "2019-08-21"
---

# JavaScript | Symbol 类型

个人感觉平时很少在实际项目中见到 Symbol 类型，但如果想深入学习原理，Symbol 类型的理解必不可少。

## 目录 <!-- omit in toc -->

- [Symbol 类型](#symbol-类型)
  - [全局 Symbol](#全局-symbol)
    - [反向调用](#反向调用)
  - [系统 Symbol](#系统-symbol)

<br>

---

<br>

## Symbol 类型


“Symbol”值是一种表示唯一的标识符，用于创建对象的“隐藏”属性，防止他人编写代码引用自己的脚本时产生无意的冲突，导致访问或者重写这些属性。

```js
let id = Symbol();      // id是Symbol的一个实例化对象
let id1 = Symbol("id"); // Symobol()内可以添加对对象的描述
let id2 = Symbol("id"); // 与id1一样，描述都为”id“

alert(id1 == id2);      // false
```

如果想要打印描述，不能直接使用变量名，而需要显式调用`toString()`方法。

想要在object字面量中使用Symbol，需要使用方括号。

```js
let id = Symbol("ID");

let user = {
  name: "John",
  [id]: 123
};
```

Symbol 在 for...in 中会被跳过，在 Object.assgin 中会被复制。

*Symbol 不是完全隐藏的，有内置方法可以获取。*

### 全局 Symbol

JavaScript ES6 提出的 Symbol 存在一个全局 symbol 注册表。使用 `Symbol.for(key)` 可以在注册表中创建或读取 Symbol。

该调用会检查全局注册表，如果有一个描述为 `key` 的 Symbol，则返回该 Symbol，否则将创建一个新 Symbol（`Symbol(key)`），并通过给定的 `key` 将其存储在注册表中。

```js
let id = Symbol.for("id");      // 如该 Symbol 不存在，则创建它

let idAgain = Symbol.for("id"); // 再次读取

alert( id === idAgain );        // 两者相同
```

#### 反向调用

`Symbol.for(key)`使用名称返回一个symbol变量。
`Symbol.keyFor(sym)`使用symbol变量返回一个名称。

### 系统 Symbol

JavaScript 内部还留有一些系统Symbol，我们可以使用它们来微调对象的各个方面。

// 暂略

<br>
