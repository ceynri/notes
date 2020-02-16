---
title: "Objects 对象类型（3）"
date: "2019-08-21"
---

# JavaScript | Objects 对象类型（3） <!-- omit in toc -->

针对对象类型某些部分进行一些深入了解。

## 目录摘要 <!-- omit in toc -->

- [Symbol 类型](#symbol-类型)
  - [全局 Symbol](#全局-symbol)
  - [系统 Symbol](#系统-symbol)
- [对象的迭代](#对象的迭代)
- [解构赋值](#解构赋值)
  - [数组解构](#数组解构)
  - [对象解构](#对象解构)
  - [智能函数参数](#智能函数参数)

<br>

---

<br>

## Symbol 类型

> 注：个人感觉平时很少在实际项目中见到 Symbol 类型，故可选读本小节。

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

#### 反向调用 <!-- omit in toc -->

`Symbol.for(key)`使用名称返回一个symbol变量。
`Symbol.keyFor(sym)`使用symbol变量返回一个名称。

### 系统 Symbol

JavaScript 内部还留有一些系统Symbol，我们可以使用它们来微调对象的各个方面。

// 暂略

<br>

## 对象的迭代

对象也支持获得key与value，区别:

|          | Map        | Object           |
| -------- | ---------- | ---------------- |
| 调用语法 | map.keys() | Object.keys(obj) |
| 返回值   | 可迭代项   | 数组             |

注意是 `Object.keys(obj)` 而不是 `obj.keys()`，原因是支持用户自己编写keys()方法的同时也可以调用自带的Object.keys()方法。

*`Object.keys/values/entries` 会忽略 `Symbol` 类型的属性，如果想要获得 `Symbol` 类型的键，使用`Object.getOwnPropertySymbols()` 会返回一个只包含 `Symbol` 类型的键的数组；`Reflect.ownKeys(obj)` 方法会返回所有键。*

<br>

## 解构赋值

[解构赋值语法]是一种 Javascript 表达式。通过解构赋值, 可以将属性/值从对象/数组中取出,赋值给其他变量。

### 数组解构

```js
let arr = ["Ilya", "Kantor"]
let [firstName, surname] = arr;
// 等价于
// let firstName = arr[0];
// let surname = arr[1];

alert(firstName); // Ilya
alert(surname);  // Kantor
```

不要的元素可以用逗号丢弃：

```js
// 不需要第一个和第二个元素
let [, , title] = ["Julius", "Caesar", "Consul", "of the Roman Republic"];

alert( title ); // Consul
```

使用 `...变量名` 可以接收多余的元素：

```js
let [name1, name2, ...rest] = ["Julius", "Caesar", "Consul", "of the Roman Republic"];

alert(rest[0]); // Consul
alert(rest[1]); // of the Roman Republic
alert(rest.length); // 2
```

允许提供默认值：

```js
let [name = "Guest", surname = "Anonymous"] = ["Julius"];

alert(name);    // Julius (来自数组的值)
alert(surname); // Anonymous (默认值被使用了)
```

#### 简单用法 <!-- omit in toc -->

变量交换：

```js
let a = 1;
let b = 2;
[a, b] = [b, a];
```

接收多个返回值：

```js
function f() {
    return [1, 2, 3, 4, 5];
}

let a, b;
[a, , , b] = f();
```

### 对象解构

语法：

```js
let {var1, var2} = {
    var1: ...,
    var2: ...
}
```

例子：

```js
let options = {
  title: "Menu",
  width: 100,
  height: 200
};

let {title, width, height} = options;

alert(title);  // Menu
alert(width);  // 100
alert(height); // 200
```

这时变量顺序不重要，但变量名是对应的。

可以使用冒号（`:`）将属性赋给不同的变量名：

```js
let options = {
  title: "Menu",
  width: 100,
  height: 200
};

// { 原属性：目标变量 }
let {width: w, height: h, title} = options;

// width -> w
// height -> h
// title -> title

alert(title);  // Menu
alert(w);      // 100
alert(h);      // 200
```

对象解构同样支持使用等号（`=`）指定默认值。

剩余操作符（`...`）目前还未完全受到支持。<font size="1" color="grey">（当前时间：2019年8月）</font>

支持嵌套解构：

![嵌套结构图]

该例子最终会得到 width、height、item1、item2 和具有默认值的 title 变量。

### 智能函数参数

使用该方法可以略写采用默认值的函数参数，且无需注意参数顺序：

```js
let options = {
    title: Menu,
    width: 150
};

function showMenu({ title = "Default", width = 100, height = 200 } = {}) {
  alert( `${title} ${width} ${height}` );
}

showMenu(options); // Menu 150 200
```

<!-- 变量区 -->

[解构赋值语法]: https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment

[嵌套结构图]: https://i.loli.net/2019/09/08/yAnEmKp2fJkNg7l.jpg
