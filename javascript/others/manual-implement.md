---
title: 手动实现...
date: 2020-04-08
---

# 手动实现...

## Function.prototype.call()

```js
Function.prototype.myCall = function(context) {
    if (typeof this !== 'function') {
        throw new TypeError('Error');
    }
    context = context || window;
    context.fn = this;
    const args = [...arguments].slice(1);
    const result = context.fn(...args);
    delete context.fn;
    return result;
}
```

## Function.prototype.apply()

```js
Function.prototype.myApply = function(context) {
    if (typeof this !== 'function') {
        throw new TypeError('Error');
    }
    context = context || window;
    context.fn = this;
    let result;
    // 处理参数和 call 有区别
    if (arguments[1]) {
      result = context.fn(...arguments[1]);
    } else {
      result = context.fn();
    }
    delete context.fn;
    return result;
}
```

## Function.prototype.bind()

```js
Function.prototype.myBind = function () {
    if (typeof this !== 'function') {
        throw new TypeError('Error');
    }
    const self = this,                  // 保存原函数的this指针
        context = arguments[0],         // 保存需要绑定的this上下文
        args = [...arguments].slice(1); // 剩余的参数转为数组
    // 返回一个新函数
    return function F() {
        // 如果是通过new调用返回的函数，则this为F的对象
        if (this instanceof F) {
            return new _this(...args, ...arguments)
        }
        // 否则，调用该函数
        self.apply(context, args.concat(...arguments));
    }
}
```
