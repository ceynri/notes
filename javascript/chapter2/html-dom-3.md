---
title: "HTML DOM（3）"
date: "2019-09-04"
---

# JavaScript | HTML DOM 拓展内容

一些关于 HTML DOM 的拓展内容。

## 目录 <!-- omit in toc -->

- [属性与特性](#属性与特性)
  - [方法](#方法)
  - [对比](#对比)
  - [特性使用场景](#特性使用场景)
  - [特性合法化](#特性合法化)
  - [什么时候使用](#什么时候使用)

<br>

---

<br>

## 属性与特性

当浏览器加载页面时，它会解析 HTML 文本并生成 DOM 对象。对于元素节点，大多数 HTML **特性**（attribute）会自动变成 DOM 对象的**属性**（property）。比如一个标签是 `<body id="page">`，那么 DOM 对象会生成这样一个属性 body.id="page"，我们称这个特性是标准化特性。

但是特性与属性并不总是一一对应的。当一个特性（假设为 `something`）是非标准的时候，它会作为特性而不会转为属性，此时我们无法使用 `elem.something` 去访问它，但可以调用方法去获得、修改、删除特性。

### 方法

| 方法 / 属性                          | 描述                     |
| ------------------------------------ | ------------------------ |
| *elem*.hasAttribute(*name*)          | 检查是否存在这个特性     |
| *elem*.getAttribute(*name*)          | 获取这个特性             |
| *elem*.setAttribute(*name*, *value*) | 把这个特性设置为 name 值 |
| *elem*.removeAttribute(*name*)       | 移除这个特性             |
| *elem*.attributes                    | 所有特性的集合           |

### 对比

|                | 类型   | 名字             |
| -------------- | ------ | ---------------- |
| 属性 property  | 属性值 | 键名大小写敏感   |
| 特性 attribute | 字符串 | 键名大小写不敏感 |

一般来说，标准化的特性被改变的时候能够自动同步到属性，反之亦然。但对于特殊情况，只能从特性同步到属性，如 `input` 的 `value`：

```html
<input>

<script>
  let input = document.querySelector('input');

  // 特性 => 属性
  input.setAttribute('value', 'text');
  alert(input.value); // text

  // 属性 => 特性 操作无效
  input.value = 'newValue';
  alert(input.getAttribute('value')); // text（没有更新）
</script>
```

虽然特性都是字符串，但是转换过来的属性可能是布尔值、对象甚至和原来都不是同一种内容的东西，
例如：DOM 属性 `href` 总是存储绝对路径，而特性值 `href` 可能只包含相对路径或者只包含 `#hash` 部分。

### 特性使用场景

借助非标准特性，我们可以给 HTML 元素打上“标记”。

```html
<!-- 标记这个 div 中要显示 "name" -->
<div show-info="name"></div>
<!-- 这里要显示 "age" -->
<div show-info="age"></div>

<script>
  // 这段代码是找到该元素并且按照给定数据展示到页面上
  let user = {
    name: "Pete",
    age: 25
  };

  for(let div of document.querySelectorAll('[show-info]')) {
    // 插入相应的数据
    let field = div.getAttribute('show-info');
    div.innerHTML = user[field]; // Pete，然后是年龄
  }
</script>
```

还可以应用于元素的样式上：

```html
<style>
  /* 按照 "order-state" 的设定产生对应样式 */
  .order[order-state="new"] {
    color: green;
  }

  .order[order-state="pending"] {
    color: blue;
  }

  .order[order-state="canceled"] {
    color: red;
  }
</style>

<div class="order" order-state="new">
  A new order.
</div>

<div class="order" order-state="pending">
  A pending order.
</div>

<div class="order" order-state="canceled">
  A canceled order.
</div>
```

那么，为什么使用特性而不直接设置class / id？因为特性值更容易管理，我们可以轻易的通过特性值的改变切换样式，比如下面这样：

```js
// 可以轻易的移除或者添加一个新的类名。
div.setAttribute('order-state', 'canceled');
```

### 特性合法化

虽然特性十分便利，但是自定义特性也存在问题：如果一个非标准化的特性在日后因为 HTML 标准的改变而标准化了（因为既然经常出现某一个非标准的特性，说明其好用，所以就会考虑将其标准化），这样就会出现问题。

为此 HTML 标准规定了所有以“**`data-`**”开头的特性值都可以正常使用，同时还会被作为 `dataset` 的合法值，可读可写。

例如：

```html
<body data-about="Elephants">
<script>
  alert(document.body.dataset.about); // Elephants
</script>
```

而由横线连接的变量名可以写成驼峰式：

```html
<div data-order-state="new">
  A new order.
</div>

<script>
  alert(order.dataset.orderState);  // new
</script>
```

### 什么时候使用

对于大多数需求，`DOM` 属性已经可以给予很好的支持。应当在 `DOM` 属性实在无法满足开发需求的情况下才使用特性，比如以下情况：

- 我们需要一个非标准化的特性。  
  不过，如果使用 `data-` 来设置特性值，就可以 `dataset` 来获取属性值。
- 我们想要读取到 `HTML` 的展示内容。  
  比如 `href` 属性总是一个绝对路径，但是我们只想要相对路径。
