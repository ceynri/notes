---
title: "Map & Set 类型"
date: "2019-08-20"
---

# JavaScript | Map 与 Set 类型 <!-- omit in toc -->

介绍 Map 类型与 Set 类型的特性与方法。

## 目录 <!-- omit in toc -->

- [Map](#map)
  - [主要方法](#主要方法)
  - [创建Map](#创建map)
- [Set](#set)
  - [主要方法](#主要方法-1)
- [WeakMap 和 WeakSet](#weakmap-和-weakset)

<br>

---

<br>

## Map

`Map` 是一个键值对的集合，与 `Object` 的主要的区别是：`Map` 允许所有数据类型作为键，包括对象。

### 主要方法

| 方法                | 描述                                       |
| ------------------- | ------------------------------------------ |
| new Map()           | 创建 map                                   |
| map.set(key, value) | 根据键（key）存储值（value）。支持链式调用 |
| map.get(key)        | 根据键返回值。若该键不存在，返回 undefined |
| map.has(key)        | 若键存在，返回 true，否则返回 false        |
| map.delete(key)     | 移除该键的值                               |
| map.clear()         | 清空 map                                   |
| map.size            | 返回当前元素个数                           |

### 创建Map

```js
// [key, value] 键值对数组
let map = new Map([
  ['1',  'str1'],
  [1,    'num1'],
  [true, 'bool1']
]);
```

`Object.entries(obj)`可以返回对象的键值对数组，利用它可以实现Object到Map的转换。

```js
let object = {
  name: "Haze",
  age: 18
}
let map = new Map( Object.entries(object) );
```

<br>

## Set

Set 是一个值的集合，这个集合中所有的值仅出现一次。

### 主要方法

| 方法              | 描述                                                |
| ----------------- | --------------------------------------------------- |
| new Set(iterable) | 创建 set，可以利用可迭代对象（如数组）来创建        |
| set.add(value)    | 添加值，返回 set 自身                               |
| set.delete(value) | 删除值，若该 value 存在则返回 true ，否则返回 false |
| set.has(value)    | 如果 set 中存在该值则返回 true ，否则返回 false     |
| set.clear()       | 清空 set                                            |
| set.size          | 返回当前元素个数                                    |

<br>

## WeakMap 和 WeakSet

WeakMap 和 WeakSet 是 Map 与 Set 的变体。

- WeakMap 仅允许对象作为键，并且当对象由于其他原因不可引用的时候将其删除。
- WeakMap 没有 size 属性，没有 clear() 方法，没有迭代器，无法使用keys()、values()等方法。

- WeakSet 仅存储对象，并且当对象由于其他原因不可引用的时候将其删除。
- 同样不支持 size/clear() 和迭代器，无法使用keys()。

WeakMap 和 WeakSet 被用作主要对象存储的次要数据结构补充。一旦对象从存储移除，那么存在于 WeakMap/WeakSet 的数据将会被自动清除。

我们可以用在当我们释放对象的时候，同时就能把对应存储在Set/Map里的内存一并释放，而无需手动删除。
