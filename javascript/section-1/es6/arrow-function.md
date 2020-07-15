---
title: '箭头函数'
date: '2020-04-04'
---

# JavaScript | 箭头函数

如果说函数是 JavaScript 中的一等公民，那么箭头函数，就是一等公民中的佼佼者。

<br>

## 介绍

在[函数](../function.md)一章中，我们已经简单地介绍了箭头函数的语法。简单回顾一下：

```js
// 普通函数
function func(str) {
  return 'Ceynri: ' + str;
}
// 匿名函数（用变量保存）
let func = function (str) {
  return 'Ceynri: ' + str;
};
// 使用箭头函数实现类似效果
let func = (str) => {
  return 'Ceynri: ' + str;
};
// 单参数，可以省略圆括号
let func = (str) => {
  return 'Ceynri: ' + str;
};
// 单句语句，可以省略花括号
// 省略花括号时，会默认return该表达式的结果
let func = (str) => 'Ceynri: ' + str;
```

可以看到，箭头函数非常简洁优雅，看起来是个很甜的“语法糖”——

但是，箭头函数实际上并不算是“语法糖”，因为它和普通函数、匿名函数都有不同的地方，在某些情形下非常有必要知道这些差别。

我们在[Objects 对象基础（2）](../objects-2.md)中的[回调函数中的 this](../objects-2.md#回调函数中的-this)部分中已经详细讲解了箭头函数在`this`方面与其他函数的不同。在这里，我们再对一些其他的不同点进行汇总。

<br>

## 与普通函数的区别

- 箭头函数不绑定`this`，在函数内调用`this`，会取到其所在上下文的`this`值

  ```js
  this.num = '?';

  let obj = {
    num: 42,
    getFalseNum: () => {
      return this.num;
    },
    getTrueNum: function () {
      return this.num;
    },
  };
  console.log(obj.getFalseNum()); // ?
  console.log(obj.getTrueNum()); // 42
  ```

- 无法作为构造函数，使用 `new` 创建实例

  ```js
  let Constructor = () => {
    console.log('?');
  };
  let fc = new Constructor();
  // Uncaught TypeError: Constructor is not a constructor
  ```

- 不绑定`arguments`（有需要的话可以用`剩余参数`语法来解决这个问题）

  ```js
  let accumulator = (...rest) => {
    let sum = 0;
    for (let num of rest) {
      sum += num;
    }
    return sum;
  };
  console.log(accumulator(1, 2, 3, 4)); // 10
  ```

- 对其使用`bind()`、`call()`或`apply()`，并不会对`this`产生影响

- 没有`prototype`原型对象

- 不能当做`Generator`函数，不能使用`yield`关键字（不过，可以使用 async/wait）

- 没有`super`，没有`new.target`

<br>

## 与匿名函数的区别

- 匿名函数中的`this`指向`undefined`或者`window`

- 用匿名函数给变量或属性赋值，就变为了一般的函数，有着普通函数的`this`行为

- 普通函数有的，匿名函数一般也有

<br>
