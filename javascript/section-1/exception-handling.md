---
title: "异常处理语句"
date: "2020-02-12"
---

# JavaScript | 异常处理语句

如果你系统地学习过 C++ 或 Java，那么`throw`与`try...catch`语句你肯定不会陌生。

在 JavaScript 中，我们也能使用`throw`语句去抛出一个异常，并用`try...catch`语句去捕获并处理它。

## 目录  <!-- omit in toc -->

- [try...catch 语句](#trycatch-语句)
- [异常对象](#异常对象)
- [throw 语句](#throw-语句)
- [...finally 语句](#finally-语句)

<br>

---

<br>

## try...catch 语句

编写代码的过程中，我们经常会遇到代码跑到一半遇到错误导致接下来的代码全部被无视掉，然后控制台无情地弹出红色的错误警告......这经常令人不快，因为很多时候某个地方发生错误并不会影响其他代码地运行，最多可能只是页面掉了某个元素。

如果你知道哪些地方可能会产生错误，那么我们可以使用一种更为合理地语法结构`try...catch`来捕捉这些异常并进行相应的处理，使得代码不会停止运行，甚至能对这个错误做一些补偿使其看起来并没有发生过错误。

`try...catch`语句通常长这样子：

```js
try {
  // 可能产生错误的代码
} catch (err) {
  // 发生异常后的处理，err为被捕捉的错误名，可以取其他名
}

```

在`try`语句块中发生错误，控制流会由发生错误的语句直接跳转到`catch`语块中，而`try`语句块中后面的代码会被跳过。所以`try`语句不是把所有的代码一包就好的，它应该根据代码的功能进行合理的包裹。

<br>

## 异常对象

当异常发生时，JavaScript 会生成一个包含异常的细节的对象，作为参数传递给`catch`语句。

每一个标准的异常对象都有这两个属性：

- `name`  
  异常的名称
- `message`  
  异常的详细文字描述

还有许多非标准的属性，在很多情况下都能够使用，其中使用最广泛的是：

- `stack`  
  当前调用栈

JavaScript 内置一些常用的异常的构造器，我们可以直接使用它们来创建异常对象。

```js
let error = new Error(message);
let error = new SyntaxError(message);
let error = new ReferenceError(message);
// ...
```

你也可以新建一个自定义的“异常对象”，然后抛出它。

```js
// 新建一个用户异常
function UserException (message){
  this.message = message;
  this.name = "UserException";
}
// 定义toString方法
UserException.prototype.toString = function (){
  return this.name + ': "' + this.message + '"';
}

// ...

// 如果某个地方不符合我们的预期
if (!something) {
    // 创建对象类型的实例并抛出它
    throw new UserException("Value too high");
}
```


<br>

## throw 语句

直接用`try...catch`语句就可以捕获由系统产生的异常错误了，但如果我们想自己设置一个错误抛出，可以使用`throw`语句可以抛出一个异常。

```js
throw <error>;
```

在 JavaScript 中，异常可以抛出任意对象或基本类型。

```js
throw "Error";    // String 类型
throw 42;         // Number 类型
throw true;       // Boolean 类型
throw { toString: function() { return "I'm an object!"; } };  // 对象类型
```

<br>

## ...finally 语句

`try...catch`语句一般时候已经够用了，但它还有另外的语法：`try...catch...finally`和`try...finally`。

`finally`语句包裹了一个绝对会被执行的代码块，不论`try`和`catch`代码块内发生了什么，是捕捉到了错误还是正常运行，甚至已经`return`或`break`准备跳出函数体/循环体了，`finally`代码块内的语句仍然会被执行。

这很可靠，因为它保证了某些语句一定会被执行，提供了可读性更好的代码写法。

```js
function func() {
  // 开始做需要被完成的操作
  try {
    // 可能会发生异常的操作
  } catch (e) {
    // 处理捕捉到的异常
  } finally {
    // 完成必须要做的事情，即使 try 里面执行失败，或者已经 return，或者在 catch 中抛出了新的异常
    // 如果省略了上面的 catch 语句部分，且发生了异常，则不会处理它，让他被丢出函数外
  }
}
```

<br>
