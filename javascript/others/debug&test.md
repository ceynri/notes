---
title: "浏览器调试与代码测试"
date: "2019-09-01"
---

# JavaScript | 浏览器调试与代码测试 <!-- omit in toc -->

介绍如何使用现代浏览器进行简单的代码调试与编写自动化测试。

## 目录 <!-- omit in toc -->

- [浏览器控制台](#浏览器控制台)
- [Chrome 调试快捷键](#chrome-调试快捷键)
- [debugger 命令](#debugger-命令)
- [日志记录](#日志记录)
- [代码运行计时](#代码运行计时)
- [代码编写规范](#代码编写规范)
- [自动化测试](#自动化测试)
  - [常用库](#常用库)
  - [样例](#样例)
  - [其他函数](#其他函数)
  - [其他断言](#其他断言)

<br>

---

<br>


## 浏览器控制台

在浏览器（如 Firefox 与 Chrome）中的控制台测试功能时，换行需要使用 <kbd>Shift</kbd>+<kbd>Enter</kbd> 键，单独的 <kbd>Enter</kbd> 键会直接运行代码。

或者尝试以下方法：

```js
(function() {
    "use strict";

    // 脚本代码...

})
```

<br>

## Chrome 调试快捷键

| 快捷键                          | 功能               |
| ------------------------------- | ------------------ |
| <kbd>F8</kbd>                   | 继续执行           |
| <kbd>F10</kbd>                  | 下一步（跳过函数） |
| <kbd>F11</kbd>                  | 下一步（进入函数） |
| <kbd>Shift</kbd>+<kbd>F11</kbd> | 执行到函数末尾     |

此外，在代码的某一行右键菜单中有一个“Continue to here”的选项运行代码到指定位置，十分方便。

<br>

## debugger 命令

```js
function hello(name) {
  let phrase = `Hello, ${name}!`;
  debugger;  // <-- 调试器会在这停止
  say(phrase);
}
```

<br>

## 日志记录

```js
console.log(msg);
```

消息会发送到控制台中。

<br>

## 代码运行计时

使用`console.time`要比`new Date() - time`要方便很多。

```js
console.time('timerName');
for (let i = 0; i < 1000000; i++) {
  // ...
}
console.timeEnd('timerName'); // timerName: 3.134033203125ms
```

<br>

## 代码编写规范

 [javascript.info](https://zh.javascript.info) 上有一篇反讽糟糕的编写习惯的文章值得一阅：[ninja code](https://zh.javascript.info/ninja-code)

<br>

## 自动化测试

### 常用库

在原教程中使用了一下 JavaScript 库进行测试：

- Mocha —— 核心框架：提供了包括 `describe` 和 `it` 的通用型测试函数和运行测试的主函数。
- Chai —— 提供很多断言支持的库。它可以用很多不同的断言。现在我们只需要用 `assert.equal`。
- Sinon —— 用于监视函数、模拟内置函数和其他函数的库。

### 样例

```js
function pow() {
  return 8; // :) 我们作弊啦！
}

describe("pow", function() {

  it("2 raised to power 3 is 8", function() {
    assert.equal(pow(2, 3), 8);
  });

  it("3 raised to power 3 is 27", function() {
    assert.equal(pow(3, 3), 27);
  });

});
```

`describe("title", function() { ... })`

表示我们正在描述的功能是什么。用于组织 `it` 代码块。

`it("title", function() { ... })`

it 里面的 “title” 中我们以人类可读的方式描述特定的用例，第二个参数是一个测试它的函数。

最好一个it函数体内写一个测试，否则前面的测试报错会停止后面的测试。

`assert.equal(value1, value2)`

it 块中的代码。

将改代码包含进HTML页面中：

```HTML
<!DOCTYPE html>
<html>
<head>
  <!-- add mocha css, to show results -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/mocha/3.2.0/mocha.css">
  <!-- add mocha framework code -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/mocha/3.2.0/mocha.js"></script>
  <script>
    mocha.setup("bdd"); // minimal setup
  </script>
  <!-- add chai -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/chai/3.5.0/chai.js"></script>
  <script>
    // chai has a lot of stuff, let's make assert global
    let assert = chai.assert;
  </script>
</head>

<body>

  <script>
    function pow() {
      return 8; // :) 我们作弊啦！
    }
  </script>

  <!-- the script with tests (describe, it...) -->
  <script src="test.js"></script>

  <!-- the element with id="mocha" will contain test results -->
  <div id="mocha"></div>

  <!-- run tests! -->
  <script>
    mocha.run();
  </script>
</body>

</html>
```

该页面内容可分为四部分：

1. `<head>` 为测试添加第三方库和样式文件。
2. `<script>` 包含测试函数，在我们的例子中 --和 pow 相关的代码。
3. `test.js` 测试代码 – 包含上面 `describe("pow", ...)`。
4. HTML 元素 `<div id="mocha">` 将会被 Mocha 用来输出结果。

测试将以 mocha.run() 命令开始。

效果：

![阶乘测试]

另：测试函数支持嵌套。

### 其他函数

包含于`Mocha`库中还有一些函数。

例如 `before/after 和 beforeEach/afterEach`

例子：

```js
describe("test", function() {

  before(() => alert("Testing started – before all tests"));
  after(() => alert("Testing finished – after all tests"));

  beforeEach(() => alert("Before a test – enter a test"));
  afterEach(() => alert("After a test – exit a test"));

  it("test 1", () => alert(1));
  it("test 2", () => alert(2));

});
```

### 其他断言

`Chai`库中的常用断言例如：

| 断言函数                               | 作用                           |
| -------------------------------------- | ------------------------------ |
| assert.equal(value1, value2)           | 检测相等 value1 == value2      |
| assert.strictEqual(value1, value2)     | 检测严格相等 value1 === value2 |
| assert.notEqual, assert.notStrictEqual | 刚好和上面做相反的检查         |
| assert.isTrue(value)                   | 检查 value === true            |
| assert.isFalse(value)                  | 检查 value === false           |
| assert.isNaN(value)                    | 检查 value === NaN             |

更多请查看[docs](https://www.chaijs.com/api/assert/)

<!-- 变量区 -->

[阶乘测试]: https://i.loli.net/2019/09/08/7g3dOHf6PkxDLcz.jpg
