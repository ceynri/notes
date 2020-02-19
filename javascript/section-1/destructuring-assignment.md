---
title: "解构赋值"
date: "2019-08-21"
---

# JavaScript | 解构赋值

没有解构赋值也可以写代码，但既然你都给了，那我就只好真香。

## 目录 <!-- omit in toc -->

- [解构赋值](#解构赋值)
  - [数组解构](#数组解构)
  - [对象解构](#对象解构)
  - [智能函数参数](#智能函数参数)

<br>

---

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
