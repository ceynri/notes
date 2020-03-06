---
title: "Objects 对象基础（1）"
date: "2019-08-15"
---

# JavaScript | Objects 对象基础（1）

介绍 JavaScript 中的`Objects`对象的基础语法。

## 目录 <!-- omit in toc -->

- [基础](#基础)
  - [创建对象](#创建对象)
  - [文本与属性](#文本与属性)
  - [点语法](#点语法)
  - [方括号](#方括号)
  - [计算属性](#计算属性)
  - [存在性检查](#存在性检查)
  - [属性遍历](#属性遍历)
  - [引用与拷贝](#引用与拷贝)
  - [垃圾回收机制](#垃圾回收机制)
  - [其他](#其他)

<br>

---

<br>

## 基础

### 创建对象

创建对象的两种方式：

```js
let user = new Object(); // 构造函数 语法
let user = {};  // 字面量 语法
```

字面量方法一般更为常用。

### 文本与属性

我们可以在创建的对象力放一些键值对：

```js
let user = {
  name: "Haze",
  age: 18
};
```

对键的称呼需要加上双引号，如：第二个属性的键是`"age"`，值是`18`。

### 点语法

```js
// 读取文件的属性：
alert( user.name ); // Haze
alert( user.age );  // 18
```

允许直接添加属性：

```js
user.isAdmin = true;
```

移除属性使用 `delete` 操作符：

```js
delete user.age;
```

多个词的词语也可以作为一个属性名，但必须加上引号：

```js
let user = {
  name: "Haze",
  age: 18,
  "handsome boy": true  // 多词属性名必须加引号
};
```

当然，单个词也可以加上引号，但是显得多余，实际效果是相同的。

```js
let user = {
  name: "Haze",   // 无效
  "name": "Kaze"  // 会覆盖掉上一行
}
```

### 方括号

除了使用点语法访问对象的属性，也可以使用方括号来操作。对于多词属性名，只能用方括号来操作：

```js
//user.level = "high";
user["level"] = "high";         // 与上一行等价

//user.handsome boy = true;     // 语法错误
user.["handsome boy"] = true;   // 正确
```

此外，方括号还支持变量作为属性名来获取属性：

```js
let user = {
  name: "John",
  age: 30
};

let key = prompt("Who r u?", "name");

alert( user[key] ); // 使用变量作为key
```

所以要注意当使用方括号获得属性时，字符串要记得加引号，否则会被当作变量从而出错。

### 计算属性

> 计算属性是 ES6 的新增特性

在对象字面量中使用方括号，被称为**计算属性**，例如：

```js
let fruit = prompt("Which fruit to buy?", "apple");

let bag = {
  [fruit]: 1        // 属性名从 fruit 变量中计算
};

alert( bag.apple ); // 如果 fruit="apple"，则输出1
```

简单地说，就是属性名可以从变量中取名。

### 存在性检查

`JavaScript`支持访问对象不存在的属性而不会报错，只是访问一个不存在的属性会返回`undefined`。检查一个属性的存在性有两种方法：

```js
alert( user.noSuchProperty === undefined );
alert( "noSuchProperty" in user );
```

*两种通常来说效果一样，而当属性存在但被赋予`undefined`值的特殊情况下，只能使用`in`操作符。*

### 属性遍历

使用for...in语句实现对一个对象的属性遍历。

```js
let user = {
  name: "Haze",
  age: 18,
  isAdmin: true
};

for(let key in user) {
  // keys
  alert( key );       // name, age, isAdmin
  // value
  alert( user[key] ); // Haze, 18, true
}
```

#### 遍历顺序 <!-- omit in toc -->

遍历对象属性时，遍历顺序会按照属性创建的顺序，但**整数属性**则较为特殊。

> 整数属性，在这里指的是可以在不改变的情况下转换为整数的字符串。

对于整数属性，会被按照数值大小进行排序。举一个电话号码对象的例子：

```js
let codes = {
  "49": "Germany",
  "41": "Switzerland",
  "44": "Great Britain",
  // ..
  "1": "USA"
};

for(let code in codes) {
  alert(code); // 1, 41, 44, 49
}
```

如果想让它们按照创建对象的顺序排列，则将其转化为非整数即可。

```js
let codes = {
  "+49": "Germany",
  "+41": "Switzerland",
  "+44": "Great Britain",
  // ...
  "+1": "USA"
};

for(let code in codes) {
  alert( code );  // +49, +41, +44, +1
  alert( +code ); // 49, 41, 44, 1
}
```

注：其实，在字面量中，只有 string 和 symbol 可以作为键，其他类型会被转为 string。所以纯数字作为属性键，也会被转换为对应的字符串。

```js
let obj = {
  0: "test"       // 等同于 "0": "test"
};

alert( obj["0"] );
alert( obj[0] );  // 相同属性
```

### 引用与拷贝

和Java类似，JavaScript的对象的变量存储也是对象的引用。

故引用对象的变量之间的赋值会导致两个变量指向同一个对象，相互影响。

为了实现拷贝的方法，我们可以使用 `for...in` 遍历所有属性：

```js
for (let key in user) {
  clone[key] = user[key];
}
```

更好的方法是使用 `Object.assign` 函数来实现。

语法：

```js
Object.assign(dest[, src1, src2, src3...])
```

- 参数 `dest` 和 `src1, ..., srcN` 是对象。
- 这个方法复制 `src1, ..., srcN` 的所有对象属性到 `dest`，然后返回 `dest`。
- 形象比喻：“ `dest = (src1 + src2 + ... + srcN) and return dest` ”

例如：

```js
let user = { name: "John" };

let permissions1 = { canView: true };
let permissions2 = { canEdit: true };

Object.assign(user, permissions1, permissions2);

// user = {
//   name: "John",
//   canView: true,
//   canEdit: true
// }
```

对于同名属性，后面的属性值会覆盖前面的属性值。

所以，我们可以使用 `Object.assign` 来代理简单的复制方法：

```js
let user = {
  name: "John",
  age: 30
};

let clone = Object.assign({}, user);
```

但对于对象属性存储对象的情况，则会出现**浅拷贝**问题。

为了解决该问题，我们在复制的时候应该检查 `user[key]` 的每一个值，如果是一个对象，我们再复制一遍这个对象。这种行为叫做**深拷贝**。

关于深拷贝，已经有一个现成的轮子可供使用，叫做 `Structured cloning algorithm`，它的一个 JS 实现的库 `lodash`, 方法名叫做 **`_.cloneDeep(obj)`**。

### 垃圾回收机制

JavaScript 与 Java 类似，具有垃圾回收机制，在这点上比C语言轻松很多。

垃圾回收的概念即“不可达（无法再被访问）的内存空间会被垃圾回收器自动释放掉”。

垃圾回收机制的原理类似于图，从根结点出发，无法到达的结点会被删除，即维护一个有向强连通图。

垃圾回收的基本算法被称为“mark-and-sweep”。

> - 垃圾收集器找到所有的根并标记。
> - 然后遍历并标记来自它们的所有参考。
> - 然后它遍历到标记的对象并标记他们的引用。所有被遍历到的对象都会被记住，以免将来再次遍历到同一个对象。
> - 遍历结束，没有被标记的所有对象都被删除。

### 其他

- 在`JavaScript`中，保留字段不能虽然当作变量名，但可以当作对象的属性名，除了`"__proto__"`需要单独处理。

- 最后一个属性后面也可以跟着逗号，称为**尾逗号**或者**悬挂逗号**。  
这样方便我们添加、删除、移动属性。
  
  ```js
  let user = {
  name: "Haze",
  age: 18,
  }
  ```

- 当属性名与变量名相同时，可以进行简写：
  
  ```js
  let name = "Haze;
  let age = 18;
  let user = {
    name, // 与 name: name 相同
    age   // 与 age: age 相同
  }
  ```
  
  简写方式支持与正常方式混用。

- 两个对象之间使用`==`与`===`没有差别，都是判断引用的地址是否相同。

- 使用`const`操作符创建的对象的可以被修改，只是不能把它指向新的对象去。
