---
title: "JSON 类型"
date: "2020-02-12"
---

# JSON 类型 <!-- omit in toc -->

介绍一种非常流行的通用数据格式——JSON（**J**ava**S**cript **O**bject **N**otation）

## 目录 <!-- omit in toc -->

- [JSON 概念](#json-概念)
- [与 JavaScript 的区别](#与-javascript-的区别)
- [JSON.stringify](#jsonstringify)
  - [参数 replacer](#参数-replacer)
  - [参数 spacer](#参数-spacer)
  - [toJSON 方法](#tojson-方法)
- [JSON.parse](#jsonparse)
  - [参数 reviver](#参数-reviver)

<br>

---

<br>

## JSON 概念

JSON 是一种表示值和对象的通用格式，虽然名字里带着 JavaScript，但这种格式被广泛接受并应用在其他的语言领域中。使用 JSON 来进行数据交换十分方便。下面是一个简单的例子：

```js
// js 对象
let student = {
  name: 'John',
  age: 30,
  isAdmin: false,
  courses: ['html', 'css', 'js'],
  wife: null
};

// 对应的 JSON 格式对象
{
  "name": "John",
  "age": 30,
  "isAdmin": false,
  "courses": ["html", "css", "js"],
  "wife": null
}
```

<br>

## 与 JavaScript 的区别

相对于 JavaScript 而言，JSON 的格式显得更加严格，类型上也非常的简单，这主要是为了使应用起来能够创造更加的高效可靠的解析算法。

- JSON 的对象属性必须是**双**引号括起来的字符串
- 对象和数组的最后一个属性后不能有逗号
- 数值不允许前导零，小数点后至少跟着一位数字
- 字符串必须使用**双**引号括起来
- JSON 不支持注释，请不要在 JSON 中添加注释
- 某些特殊的字符会被转义
- 禁止某些控制字符

明白了这些规则，手写 JSON 也不是不能做到的事情（虽然某些细节容易犯错），但是当需要转换为 JSON 的文本越来越大，手写显得尤为复杂。

所幸 JavaScript 已经内置了 JSON 对象，提供了`parse()`与`stringify()`方法，让这件事变得简单起来。

<br>

## JSON.stringify

`JSON.stringify()`方法允许将 JavaScript 对象、数组和一些基本类型（字符串、数值等）转换为 JSON 格式的字符串。

```js
let student = { ... };
let json = JSON.stringify(student);
alert(typeof json); // string
```

因为 JSON 是一种跨语言的纯数据规范，所以一些 JavaScript 的特定对象属性会被`JSON.stringify()`所跳过。

例如：

- 函数属性（方法）
- Symbolic 属性
- 存储`undefined`的属性

注意：

- 嵌套的对象也会被自动转换，这很方便，没有类似于“浅拷贝”的问题。
- 对于循环引用（A 引用了 B，B 中也引用了 A），`JSON.stringify()`会报错。

`JSON.stringify`的完整语法是：

```js
JSON.stringify(value[, replacer, space]);
```
- value  
  要编码的值
- replacer  
  要编码的属性数组或者是映射函数
- space  
  为JSON字符串添加缩进、空格和换行符

### 参数 replacer

当我们只想指定某些属性导出为 JSON 时（比如某些属性存在循环引用问题），可以创建一个包含需要的属性的数组作为`replacer`的值。

```js
let room = {
  number: 23
};

let meetup = {
  title: "Conference",
  participants: [{name: "John"}, {name: "Alice"}],
  place: room // meetup 引用 room
};

room.occupiedBy = meetup; // room 引用 meetup

alert( JSON.stringify(meetup, ['title', 'participants']) );
// {"title":"Conference","participants":[{},{}]}
```

这里由于没有写上`name`属性，所以即便是嵌套在`participants`里也被省略掉了。

除了数组，我们也可以使用一个函数作为`replacer`，该函数将调用每个`(key, value)`对，然后使用返回值替代`value`。

所以上面的例子如果只想要避免循环引用的问题，也可以改写为如下形式：

```js
// ...

let json = JSON.stringify(meetup, function (key, value) {
  return (key == 'occupiedBy') ? undefined : value;
});
```

### 参数 spacer

`spacer`接受一个数值，用来指定转换后的 JSON 是否包含额外的缩进、空格与换行，如果没有指定，一般会被压缩成不好阅读的一行常常的字符串；指定后则便于直接输出而无需手动格式化。

### toJSON 方法

`JSON.stringify`会自动调用对象的`toJSON`方法（如果存在的话），比如一个`Date`对象，其本身是一个对象，但在转换为 JSON 后自动会替换为一个字符串：

```js
let meetup = {
  title: 'Conference',
  date: new Date(Date.UTC(2017, 0, 1))
};

alert( JSON.stringify(meetup) );
/*
{
  "title":"Conference",
  "date":"2017-01-01T00:00:00.000Z"
}
*/
```

所以我们也可以为对象写一个`toJSON`方法，指定转换为 JSON 时变成的内容。

<br>

## JSON.parse

想要解码 JSON 字符串，可以使用`JSON.parse`方法。

语法：

```js
let value = JSON.parse(str[, reviver]);
```

- str  
  要解析的 JSON 字符串
- reviver  
  为每个 (key,value) 对调用该`reviver`函数进行转换

str 参数需要严格遵守 JSON 格式规范，否则会产生错误（这常见于手写 JSON 的情况）。

### 参数 reviver

`reviver`相当于`JSON.stringify`的`replacer`的逆过程。它接受一对 (key, value)，然后处理它并返回新的`value`。

```js
let str = '{"title":"Conference","date":"2017-11-30T12:00:00.000Z"}';

let meetup = JSON.parse(str, function(key, value) {
  if (key == 'date') return new Date(value);
  return value;
});

alert( meetup.date.getDate() );
```

<br>
