---
title: 'Promise 对象'
date: '2020-07-15'
---

# JavaScript | Promise 对象

Promise 是入门现代 JavaScript 异步编程的基石。

<br>

## 前言

在我开始入门前端的很长一段时间，我都没能够理解 Promise 到底是个什么东西，各种各样的教程看了又看，只落下个“解决丑陋的回调嵌套”、“更优雅的异步编程方式”的印象。其实这不能怪我，因为在这一段时间里，我都没有接触过异步编程，编写的页面都是纯前端的静态页面，不需要和后端进行数据的交换，自然也就很难理解异步编程里各种各样的概念以及它们背后的意义了。

因为实在是缺乏使用，让我一度产生了 Promise 并不是一个很重要的语法的错觉，直到我逐渐从自个把玩的静态页面过渡到需要前后端对接的动态页面时，我才终于明白为什么面试基础题里 90% 都会考它。

说到底，Promise 就是**针对“异步编程”场景，应用于前端和后端的数据交互，给出相比于“事件监听-回调函数”更加合理直观的解决方案**。

本文希望能够从新手的角度，去理解 Promise 的作用，以及简单的特点，而不去深入展开各种复杂的语法。

<br>

## 传统方式

回调是 JavaScript 非常重要的特点，通过回调，我们可以让一些事情能够在某件事情的特定阶段中去执行。而在异步编程中，我们通过监听某某事件的完成，来回调我们想要在完成该事件后需要执行的代码。

比如说，我们希望加载一个新的脚本，然后执行该脚本里的一个函数，但从网络去获取该脚本的内容并下载下来是需要时间的，而这个加载过程在 JavaScript 中一般是异步的，这就导致你不能在发出加载脚本的请求后就立刻去尝试使用该脚本的东西。

```js
// 假设我们有一个 loadScript，能够异步加载一个脚本文件
// script.js 中有一个方法 "doSth"
loadScript('script.js');
doSth(); // error: 没有这个函数！
```

```js
// loadScript 实现
function loadScript(src) {
  let script = document.createElement('script');
  script.src = src;
  document.head.append(script);
}
```

好在我们可以尝试去**监听脚本加载完的事件**，在该事件发生后，我们再通过**回调**的方式，去执行需要使用到该脚本的代码。

```js
// 修改一下 loadScript 的实现
function loadScript(src, callback) {
  let script = document.createElement('script');
  script.src = src;
  script.onload = () => callback(script); // *
  document.head.append(script);
}
```

```js
loadScript('script.js', () => {
  // 在脚本加载完成后，回调函数才会执行
  doSth();
});
```

这就是常见的异步编程基本原理，它并不难理解，而且经常出现，不懂异步编程的人也使用过类似的调用方式。

### 问题

简单的事件监听回调，看起来合理而易用，但随着程序逐渐变得复杂，就会开始暴露出一些问题来了。

在异步编程中，我们可能某一个行为，需要进行多次的请求才能够完成，而它们之间是有着前后顺序的。例如我们可以假设一下，拆分一个“登录”行为，我们进行以下多个请求：

- 验证账号是否存在
- 验证账号所对应的密码是否正确
- 验证验证码是否输入正确

> 实际上该行为只需要一次请求，只是为了体现问题所以将他们拆分开来了

```js
sendRequest('checkAccount', 'admin', (result) => {
  if (result === 'ok') {
    sendRequest('checkPassword', 'password', (result) => {
      if (result === 'ok') {
        sendRequest('checkCaptcha', 'ABCD', (result) => {
          if (result === 'ok') {
              // 通过
          }
        });
      }
    });
  }
});
```

可以看到，这里已经出现了比较严重的嵌套，而且还没有包含错误处理。看似这个问题，我们可以进行一些优化，让它看起来不嵌套，但本质上问题并没有被解决。而且当每个请求之间要是还有其他逻辑，再加上错误处理、条件逻辑判断等等，很快这块代码就变得又长又臭，难以阅读。

为了比较好的解决这个问题，ES6 为我们带来了 Promise。

<br>

## Promise

Promise 最早来自于社区，其作为一个优秀的异步编程方案，于 ES6 被收入 JavaScript 的语言标准中。Promise 如同它的词义，会返回一个带有“承诺”的对象。这是什么意思呢？举一个经典的例子：

### 例子

假设你是一名厂商，正在研发一个新的商品，旗下的商店需要购买一批该商品，卖给正在期待该商品的顾客。

研发商品需要时间（*异步*），所以不能一启动研发、商店就来找你进货，故顾客也不能马上就在商店买到。

一种解决方法就是商店派一个人在门口等（*事件监听*），一直等到你研发完成后（*事件触发*），商店就来收购该商品带回店里（*函数回调*）。但这种方法并不是很方便，因为想要买该商品的顾客也要经常来店里看商品上了没有，好在第一时间从商店买到（*回调嵌套*）。

Promise 的解决方式，就在于作为厂商的你，可以给商店一个承诺：

- 我送你一个宝贝（*Promise 对象*），它会显示当前商品的研发状态。
- 当我还在研发的时候，它会一直显示“pending”，你也不用来问。
- 如果研发完成了，我这边设置一下指令（*resolve*），它就会显示“fulfilled”，告诉你是什么产品研发好了（*resolve 的参数*）；
- 如果研发失败了，我也设置另一个指令（*reject*），这个宝贝就显示“rejected”，告诉你研发出现了什么问题（*reject 的参数*）。
- 到时候你根据我给你发的状态（*resolve* 或 *reject*），做不同的处理（*then* 或 *catch*）。
- 你也可以给顾客也发个这样的宝贝，等到货了就可以通知它们。

这样一来，商家就不用派人等，顾客也可以第一时间收到消息了。

<br>

### 代码实现

我们把上面这个例子翻译成 Promise 实现，可以是这样的代码：

```js
// 以“_”开头的函数和变量都是伪代码，不是语法自带的

let produce = new Promise((resolve, reject) => {
  // 生产
  // ...

  if (_success) {
    resolve(_productName);
  }
  reject(_errorMsg);
}).then(value => {
  // 商店上架商品
  _putOnShelf(value);
}).then(() => {
  // 顾客来商店
  _goShopping();
}).catch(error => {
  // 研发失败
  console.error(error);
});
```

在这里，我们来逐句分析一下，以对 Promise 的语法有一个简单的了解：

- Promise 构造函数接受一个回调函数，这个回调函数具有两个参数。注意，这两个参数都是回调函数的名字

  ```js
  let produce = new Promise((resolve, reject) => {
    // ...
  };
  ```

- 因为 Promise 接受的是回调函数，所以在 new Promise 后，直接就返回了一个 Promise 对象，允许调用它的 then 方法

  ```js
  new Promise((resolve, reject) => {
    // ...
  }).then(value => {
    // ...
  });
  ```

- 同理，then 方法返回的也是 Promise 对象，所以可以继续链式调用 then 方法

  ```js
  produce.then(
    () => { /* ... */}
    // then 函数包装回调函数的内容，返回一个新的 Promise 对象
  ).then(() => {
    // ...
  });
  ```

- 经过生产后，如果生产成功，我们可以调用 resolve 函数，resolve 的参数会作为后面的 then 方法回调的函数的参数（`value`）

  ```js
  new Promise((resolve, reject) => {
    resolve('42');
  }).then(value => {
    console.log(value); // 42
  });
  ```

- 如果生产失败，调用 reject 函数，函数的参数会作为 catch 方法回调的函数的参数（`error`）

  ```js
  new Promise((resolve, reject) => {
    reject('42');
  }).catch(e => {
    console.error(e); // Uncaught error: 42
  });
  ```

- then 方法里可以进行 return，返回值会作为下一个最近的 then 方法回调函数的参数被使用

  ```js
  produce.then(() => {
    return 42;
  }).then(value => {
    console.log(value); // 42
  });
  ```

- then 方法里可以进行 catch，返回值会作为下一个最近的 catch 方法回调函数的参数被使用

  ```js
  produce.then(() => {
    throw 42;
  }).catch(e => {
    console.error(e); // Uncaught error: 42
  });
  ```

<br>

## 总结

到了这里，你对 Promise 是否具有了一些印象，开始理解为什么要使用 Promise 了么？

依我个人来看，Promise 的特点就在得益于“连缀语法”的特点，不仅 new Promise 返回的是 Promise 对象，then、catch 方法也会返回 Promise 对象，这使得我们可以不断尾随 then 方法以实现原本需要嵌套多层代码才能完成的事情，将立体的复杂阅读顺序给扁平化了。并且以“承诺”的方式，不阻塞代码流程，且提供更好用的 API，让开发与阅读变得更加容易。

以上都只是关于 Promise 的初步认识，并没有深入讲解 Promise 更多的语法特性以及 API，也是避免扰乱像我一样没接触过异步编程的人的理解。如果想要熟练使用它，最好可以再继续了解 Promise 的特性、常用 API，甚至是事件循环里 Promise 作为“微任务”的特性，以更好地在项目中使用它们。

不过值得说的一点是，如果在项目里准备大量使用异步编程的你还不了解 async/await 语法，那需要提前知道的是，async 语法可以让 Promise 变得更加优雅易读，非常值得在 Promise 后学习使用。

> 继续学习 Promise，可以参考：阮一峰 ES6 入门教程 - Promise 对象 <https://es6.ruanyifeng.com/#docs/promise>

<br>
