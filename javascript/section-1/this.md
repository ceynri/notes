---
title: "this"
date: "2020-02-19"
---

# this

JavaScript 的`this`相比其他语言有那么一点不同，它在不同的情况下有着不同的指向，具有相当的灵活性。

但是这也导致它的指向并不是一如表面那么直接，在不同的情况下，我们要考虑这里的`this`到底指向了什么。（那么，代价是什么.jpg）

<br>

---

<br>

## 从函数讲起

我们日常见到的`this`基本都出现在函数中，这是因为如果在全局上下文中调用`this`，实际上就是调用`window`，而在全局中这是可以忽略的。

例如全局变量，实际上它们的命名空间在`window`对象上，函数也是如此，即便是有些内置的函数`setTimeout()`，其实完整的写法是`window.setTimeout()`。

那么，函数中的`this`指向的又是谁呢？

在其他面向对象的语言中，一般是在“class 类”中使用到`this`指针，然后使用`new 类名`来创建对象，`this`指向的往往就是创建的对象本身。

而在 JavaScript 中，对象是通过`new 构造函数`来创建的（先忽略 ES6 新加入的 class 语法），看起来我们的`this`和其他语言没有什么区别，运行的效果也是和我们所期望的一致。

```js
function MyNum() {
    this.value = 0;
    this.setNum = function() {
        this.value = 42
    };
}

const num = new MyNum();
console.log(num.value);  // 0

num.setNum();
console.log(num.value);  // 42
```

但是，JavaScript 的函数中的`this`实际上指向的是**调用该函数的调用者**。


> 在 ES6 以后，使用`use strict`模式，则在全局环境中调用函数，函数中的`this`不再指向`window`而是指向`undefined`

# 写不下去了
