---
title: 'async 函数'
date: 2020-07-16
---

# JavaScript | async 函数

async 是 Generator 函数销声匿迹的罪魁祸首，await 是 Promise 美化的得力伙伴。

## Generator 函数

如果你不太了解 Generator 函数是怎么用的，也没有太大关系，因为现在我们已经越来越少看到他的身影了，取而代之的就是 async 函数 —— Generator 函数的语法糖。

> 如果对 Generator 不感兴趣，可以先跳过这一部分

一个简单的 Generator 函数大概是这样子：

```js
function* myGenerator(x) {
  let y = yield x + 2;
  return y;
}

let g = myGenerator(1);
g.next()  // { value: 3, done: false }
g.next(2) // { value: 2, done: true }
```

当 function 标识符后面加上一个 `*` 时，就代表该函数为 Generator 函数。Generator 函数内可以添加 yield 关键字，当代码调用 Generator 函数时，代码并不会立即执行，只有调用它的 next 方法，函数才会运行，且会在 yield 关键字处停下，返回 yield 关键字后面的表达式的值。调用 next 方法得到的是一个包含 `value` 与 `done` 的对象，`value` 表示 yield 后的表达式的值，`done` 表示该 Generator 函数是否 return 结束。

next 方法接受一个参数，它会代替掉上一个 yield 关键字后的表达式的值，参与函数的运算。例如上例中，`g.next()` 获得的 `x + 2` 的值为 `3`，而接下来的 `g.next(2)` 用 `2` 代替了 `3`，进入代码逻辑中，赋值给变量 `y`，因为 next 方法会获得 return 值，所以 得到的对象 `value = 2`，且 `done = true`。

或许上面的 Generator 函数会让你感觉莫名其妙，好端端的函数非要变得那么复杂。实际上它只是用来快速说明 Generator 特性的一个例子，即“能够暂停代码的执行”，让出执行权。这个特性使得它可以比较好的应用在异步操作中，我们等待（yield）异步操作的回调，让该操作在执行完成后再执行下一个操作（next），从而避免“回调地狱”的问题。

但显然，单单的 Generator 函数并不能很方便地应用于异步编程中，需要进行一些包装，使其变得好用。虽然曾经有些库利用该特性为异步编程提供了不小的帮助，但 async 函数的出现，一下子就把它这个特点给很好的 cover 住了。

## async

把上面的例子用 async 语法来改写一下：

```js
async function myGenerator(x) {
  let y = await x + 2;
  return y;
}

let g = myGenerator(1); // Promise {<resolved>: 3}
```

经过对比可以看到，`async` 代替了 `*`，`await` 代替了 `yield`，就实现了从 Generator 函数到 async 函数的转换。

在 `function` 关键字之前加上 `async`，我们就声明了一个异步函数。这种函数一被执行就会返回一个 Promise 对象，不阻塞代码的执行。函数正常结束，就回调 resolve；抛出异常，则产生 reject。

而在函数内部，我们可以使用 await 关键字修饰表达式。await 的作用就在于，它能够让一个异步的代码串行化，如果 await 后面跟着的是 Promise 对象，代码就会“停下来”，等待后面的异步代码调用执行完毕，然后得到返回的 resolve 的参数（即便 await 后是原始类型的值，也会被自动转换为 resolved 的 Promise 对象）。

实际上，整个代码流程并不会真的在 await 处暂停，因为 async 函数代表了它是一个异步函数，当 async 函数内部暂停后，会将主动权让给 async 函数调用位置后续的代码，不阻塞主流程。所以 await 只能出现在 async 函数中。

另外，原本需要用 catch 来对 Promise 对象的异常进行捕获，现在在 async 函数中，我们可以用 `try...catch` 语句来完成这件事情。

这个特点就使得我们可以将原本需要不断 `then`、`then`、...、`catch` 的代码变得和普通的串行代码看起来没有太大的差别，这在阅读上有了很好的改观，同时也对日后的代码重构非常友好。

```js
// 替换前
promiseObj.then(a => {
  let value = asyncFunc(a);
  value += 42;
  return value;
}).then(b => {
  console.log(b);
}).catch(err => {
  console.error(error);
})

// 替换后
try {
  let a = await promiseObj;
  let b = await asyncFunc(a);
  b += 42;
  console.log(b);
} catch (err) {
  console.error(error);
}
```

当然，如果在你的代码块中，异步操作后还跟着同步操作，那就不能这么代替了。

```js
(() => {
  new Promise((resolve, reject) => {
    resolve();
  }).then(() => {
    console.log(1);
  })
  console.log(2);
})();
// 输出结果：2、1

(async() => {
  await new Promise((resolve, reject) => {
    resolve();
  });
  console.log(1);
  console.log(2);
})();
// 输出结果：1、2
```

不过一般来说，出现这样的情况说明 `console.log(2)` 与前面的异步代码没有联系，做的不是相同的事情，反而可以考虑它们有没有必要放在同一个函数里面了。

总之 async/await 语法并不难懂，只要我们理清了 Promise、async、generator 之间的关系，剩下的就是不断熟练语法了~尝试更优雅的编写异步代码吧😄
