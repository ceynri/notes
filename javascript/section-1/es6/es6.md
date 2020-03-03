---
title: "ES6 的其他特性"
date: "2019-09-06"
---

# JavaScript | ES6 的其他特性

*收集中*

## 对象的迭代

对象也支持获得 key 与 value，区别:

|          | Map        | Object           |
| -------- | ---------- | ---------------- |
| 调用语法 | map.keys() | Object.keys(obj) |
| 返回值   | 可迭代项   | 数组             |

注意是 `Object.keys(obj)` 而不是 `obj.keys()`，原因是支持用户自己编写keys()方法的同时也可以调用自带的Object.keys()方法。

*`Object.keys/values/entries` 会忽略 `Symbol` 类型的属性，如果想要获得 `Symbol` 类型的键，使用`Object.getOwnPropertySymbols()` 会返回一个只包含 `Symbol` 类型的键的数组；`Reflect.ownKeys(obj)` 方法会返回所有键。*

<br>
