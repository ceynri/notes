---
title: "Array 类型"
date: "2019-08-19"
---

# JavaScript | Array 类型

介绍 Array 类型的特性及其常用方法。

## 目录摘要 <!-- omit in toc -->

- [数组](#数组)
  - [声明](#声明)
  - [模拟队列与栈](#模拟队列与栈)
  - [遍历数组](#遍历数组)
  - [length属性](#length属性)
- [数组方法](#数组方法)
  - [添加/删除元素](#添加删除元素)
  - [查询元素](#查询元素)
  - [数组转换](#数组转换)
  - [迭代元素](#迭代元素)

<br>

---

<br>


## 数组

数组是一种储存有序集合的数据结构。

作为对象，在JavaScript中对其进行了特殊的优化，使其在内存中连续且比普通对象性能更好。

### 声明

创建方法：

```js
let arr = new Array();
let arr = [];
```

一般使用第二种方式创建数组更好。

注意其使用的是方括号而非C、Java使用的花括号作为数组创建的符号。

许多行为与Java相类似：

```js
let fruits = ["Apple", "Orange", "Plum"];   // 创建数组
alert( fruits[0] );                         // 获取元素
fruits[2] = 'Pear';                         // 替换元素
fruits[3] = 'Lemon';                        // 添加元素
alert( fruits.length );                     // 数组元素个数
```

JavaScript的Array数组支持混合值：

```js
let arr = [ 'Apple', { name: 'Haze' }, true, function() { alert('hello'); } ];
```

和对象类似，支持换行且支持冗余逗号结尾：

```js
let fruits = [
  "Apple",
  "Orange",
  "Plum",       // 注意逗号
];
```

### 模拟队列与栈

数组对象提供`pop`、`push`、`shift`、`unshift`方法。

- 模拟队列使用`push`方法在队尾加入元素，使用`shift`方法在队首移除元素；
- 模拟栈使用`push`方法在栈顶压入元素，是哦你`pop`方法在栈顶弹出元素。

### 遍历数组

遍历数组推荐使用`for`循环语句或`for...of`语句而非`for...in`语句：

```js
let fruits = ["Apple", "Orange", "Plum"];

// for循环遍历数组元素
for (let i = 0; i < arr.length; i++) {
  alert( arr[i] );
}
// 迭代数组元素
for (let fruit of fruits) {
  alert( fruit );
}
```

`for...in`语句会迭代数组所有的属性，出现我们可能并不需要的属性及方法，且没有对array进行速度优化。

### length属性

数组的length属性存储的是`数组所有元素中最大索引值+1`。

length属性是可写的，长度缩短时会发生截断，丢弃溢出的元素，故可以使用`arr.length = 0`来清空数组。

### 其他 <!-- omit in toc -->

- 支持多维数组

```js
let matrix = [
[1, 2, 3],
[4, 5, 6],
[7, 8, 9]
];

alert( matrix[1][1] ); // 5
```

- toString()方法会给每个元素之间添加逗号（`,`）

<br>

## 数组方法

内容较多，个人认为了解一下，需用时勤于搜索、用熟后记住常见的方法即可。

以下摘录并整理自[原文总结部分][数组方法]：

### 添加/删除元素

| 方法                               | 描述                                                                                           |
| ---------------------------------- | ---------------------------------------------------------------------------------------------- |
| push(...items)                     | 从结尾添加元素                                                                                 |
| pop()                              | 从结尾提取元素                                                                                 |
| shift()                            | 从开头提取元素                                                                                 |
| unshift(...items)                  | 从开头添加元素                                                                                 |
| splice(pos, deleteCount, ...items) | 从 pos 开始删除 deleteCount 个元素并在当前位置插入元素。                                       |
| slice(start, end)                  | 它从所有元素的开始索引 start 复制到 end （不包括end）返回一个新的数组                          |
| concat(...items)                   | 返回一个新数组：复制当前数组的所有成员并向其中添加 items，若某 item 为数组则添加该 item 的元素 |

### 查询元素

| 方法                           | 描述                                                                                   |
| ------------------------------ | -------------------------------------------------------------------------------------- |
| indexOf/lastIndexOf(item, pos) | 从 pos 找到 item 则返回索引，否则返回 -1                                               |
| includes(value)                | 数组有 value 则返回 true，否则返回 false                                               |
| find/filter(func)              | 通过函数过滤元素：find 函数返回符合func条件的第一个值；filter 函数符合func条件的全部值 |

findIndex 和 find 类似，但返回索引而不是值。

### 数组转换

| 方法                  | 描述                                                               |
| --------------------- | ------------------------------------------------------------------ |
| map(func)             | 从每个元素调用 func 的结果创建一个新数组                           |
| sort(func)            | 将数组按func条件判断并排序，然后返回。例：arr.sort((a, b) => a-b)  |
| reverse()             | 在原地颠倒数组，然后返回它                                         |
| split(delim)          | 将字符串按 delim 分隔符拆分为数组并返回                            |
| join(delim)           | 将数组按 delim 分隔符黏合为字符串并返回                            |
| reduce(func, initial) | 通过为每个元素调用 func 计算数组上的单个值并在调用之间传递中间结果 |

### 迭代元素

| 方法          | 描述                                |
| ------------- | ----------------------------------- |
| forEach(func) | 为每个元素调用 func，不返回任何东西 |

### 其他 <!-- omit in toc -->

| 方法               | 描述                    |
| ------------------ | ----------------------- |
| Array.isArray(arr) | 检查 arr 是否是一个数组 |

注意：sort，reverse 和 splice 方法修改数组本身。

这些方法是最常用的方法，它们覆盖 99％ 的用例。但是还有其他几个：

| 方法                               | 描述                                                                                     |
| ---------------------------------- | ---------------------------------------------------------------------------------------- |
| arr.some(fn)/arr.every(fn)         | 检查数组，对数组每个元素调用函数 fn。若任何/所有结果为 true，则返回 true，否则返回 false |
| arr.fill(value, start, end)        | 从 start 到 end 用 value 重复填充数组                                                    |
| arr.copyWithin(target, start, end) | 将其元素从 start 到 end 在 target 位置复制到本身（覆盖现有）                             |

```js
Array(5).fill({name:'Haze', age: 18, sex: 1})

//结果
[ { name: 'Haze', age: 18, sex: 1 },
  { name: 'Haze', age: 18, sex: 1 },
  { name: 'Haze', age: 18, sex: 1 },
  { name: 'Haze', age: 18, sex: 1 },
  { name: 'Haze', age: 18, sex: 1 } ]
```

<!-- 变量区 -->

[数组方法]: https://zh.javascript.info/array-methods#zong-jie
