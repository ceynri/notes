---
title: "Class 类"
date: "2019-08-22"
---

# JavaScript | Class 类

## *内容待丰富*

<br>

## 语法

```js
class MyClass {
  prop = value; // field

  constructor(...) { // 构造器
    // ...
  }

  method(...) {} // 方法

  get something(...) {} // getter 方法
  set something(...) {} // setter 方法

  [Symbol.iterator]() {} // 计算 name/symbol 名方法
  // ...
}
```

技术上来说，MyClass 是一个函数（我们提供作为 `constructor` 的那个），而 methods，getters 和 settors 都被写入 `MyClass.prototype`。

对于 class 属性，旧的浏览器可能需要 polyfill —— 类级别的属性是最近才添加到语言中的。
