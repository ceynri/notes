---
title: "JavaScript 编码规范"
date: "2020-05-25"
---

# JavaScript 编码规范

## 前言

刚开始学习编程时，我们都定义过 a、a1、aaa 这样名字的变量，从来不在运算符之间加空格，注释几乎没有。倘若编辑器支持自动格式化代码，会使用快捷键进行代码格式化的人已经算是非常注重整洁的人了。随着学习的深入，同学之间互相交流代码是避免不了的，这时候才发现别人的代码读起来真费劲。

偶然间看到了代码风格非常漂亮的人开源在网上的代码，不由得为其中的细节赞叹出声，即便代码并不是很复杂，但也给我一种编写者的水平并不一般的感觉。心想与其让代码隔周就无法辨识，不如花一点时间了解一下标准的代码都是有着什么样的规范，日后大家都是花同样的时间写代码，美观性却能差出好几个等级。

启蒙我的代码规范是阿里巴巴的 JAVA 编程规范，第一次启用时它让我的代码多了数不清的波浪线。但细细去了解规则时，无处不在的空格、适当的换行、分支语句即使只有一行也必须使用花括号包裹，还有尽可能语义化的驼峰变量名、常量的大写定义、禁止行尾注释等等，都深深地让我感受到 JAVA 的优雅。

虽然我现在几乎不再写 JAVA 代码了，但在其他的语言我都愿意在学习完大概的语法后都去了解一下它们比较流行的编码规范。好在它们的规则大多都是相通的，学习一时，受用终生。

> 本文省略了绝大部分代码格式化工具都会带有的规则
>
> 例如“运算符左右设置各设置一个空格”、“多参数的`,`后跟空格”、“`if`与`(`之间需要一个空格”等

<br/>

## 命名

- 变量 camelCase
- 常量 UPPER_CASE
- 函数/方法 camelCase
- 类/对象 PascalCase
- 文件 kebab-case

- 【推荐】 如果属性/方法是一个 `boolean` 值，使用 `isXxx()` 或者 `hasXxx()` 命名
- 【可选】 对属性读取或赋值，可以使用 `getXxx()` 或 `setXxx()` 命名，减少使用 getters/setters 方法

## 引用

- 【必须】 使用`const`定义所有引用，而不使用`var`
- 【必须】 如果必须重新赋值引用，则使用`let`代替`var`

## 对象

- 【必须】 使用字面量语法定义对象
- 【推荐】 使用对象方法简写、属性值简写
- 【推荐】 被简写的属性放在所有属性前面
- 【推荐】 使用扩展操作符、剩余运算符来获得一个对象的浅拷贝（可顺便增加/减少某些属性）
- 【推荐】 在对象/数组最后一个属性/元素后添加尾随逗号，便于添加新元素或移动该元素的位置

```js
// bad
const hero = {
  firstName: "Ryan",
  lastName: "Arcand"
};

// good
const hero = {
  firstName: "Ryan",
  lastName: "Arcand",
};
```

## 数组

- 【推荐】 使用扩展操作符、剩余运算符来获得一个数组的浅拷贝
- 【推荐】 如果要换多行，则在`[`前、`]`后分别换行（对象的`{}`也是）

```js
// bad
const arr = [[0, 1],
             [2, 3],
             [4, 5]];

const objArr = [{
    id: 1,
  },{
    id: 2,
  }];

// good
const arr = [
  [0, 1],
  [2, 3],
  [4, 5],
];

const objArr = [
  {
    id: 1,
  },
  {
    id: 2,
  },
];
```

## 解构

- 【推荐】 使用对象解构和数组解构来接收需要的值
- 【推荐】 需要返回多个返回值时, 使用对象解构，而不是数组解构

## 字符

- 【推荐】 使用单引号`'`来定义字符串
- 【必须】 使用字符串模板代替字符串拼接

```js
// bad
function sayHi(name) {
  return "How are you, " + name + "?";
}

// bad
function sayHi(name) {
  return ["How are you, ", name, "?"].join();
}

// good
function sayHi(name) {
  return `How are you, ${name}?`;
}
```

- 【推荐】 使用 `String()` 函数将变量转成字符串，比较保险

```js
// bad
const str = new String(this.score); // typeof str is "object" not "string"

// bad
const str = this.score.toString(); // isn’t guaranteed to return a string

// not good
const str = this.score + ""; // invokes this.score.valueOf()

// good
const str = String(this.score);
```

## 函数

- 【推荐】 使用命名的函数表达式代替函数声明以避免作用域提前使得代码可维护性降低
- 【推荐】 使用 rest 语法`...`代替`arguments`
- 【推荐】 多函数参数换行规则也是每行只包含一个参数

```js
// bad
function foo(bar, 
             baz, 
             quux) {
  // ...
}

// good
function foo(
  bar, 
  baz, 
  quux
) {
  // ...
}
```

## 语句

- 【推荐】 如果 if 语句块内结尾进行了 return，无需再使用 else 进行分支
- 【推荐】 声明多个变量应该分开声明，避免使用`,`一次声明多个变量
- 【推荐】 使用 === 和 !== 而不是 == 和 !=
- 【推荐】 避免不必要的三元表达式

```js
// bad
const foo = a ? a : b;
const baz = c ? false : true;

// good
const foo = a || b;
const baz = !c;
```

- 【必须】 当有多行代码块的时候，应使用大括号包裹

```js
// bad
if (test) 
  return false;

// good
if (test) return false;

// good
if (test) {
  return false;
}
```

- 【推荐】 当控制语句太长需要换行时，每个条件一行，且逻辑运算符放在行的开始

```js
// bad
if (foo === 123 && 
  bar === "abc") {
    thing1();
}

// bad
if (foo === 123 
  && bar === "abc") {
    thing1();
}

// good
if (
  foo === 123
  && bar === "abc"
) {
  thing1();
}
```

- 【推荐】 使用`//`进行单行注释而不要进行行尾注释，注释放在需要注释的代码的上方新行，且可以在注释前放一个空行
- 【必须】 注释符号与内容之间都间隔一个空格以更好阅读
- 【推荐】 使用 tabs (空格字符) 设置为 2 个空格

## 其他习惯

最后说一点自己觉得的好习惯，偶尔想起来的时候就补充一下该部分

- 如果只用获取数组成员，使用 `for...of` 去代替 `for` 循环
- 如果 `if` 语句内包含了 `return`，那后面的语句不用再写 `else`
- `document.querySelector()` 与 `document.querySelectorAll()` 很好用，除非有极致的性能要求，一般很少会再用`getElementsByXxx()`的一系列方法了
- 用 `a = a || b` 代替 `a = (a != null ? a : b)` 更加简洁
- 多了解新的语法糖（class、剩余运算符、解构赋值等）并加以使用，可以使写代码更轻松
- 可以用`// FIXME: xxx`注释问题，`// TODO: xxx`待完成的内容
