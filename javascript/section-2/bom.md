---
title: "BOM"
date: "2019-09-07"
---

# JavaScript | BOM

## 目录 <!-- omit in toc -->

- [window 对象](#window-对象)
- [窗口尺寸](#窗口尺寸)
- [元素尺寸](#元素尺寸)
- [页面滚动](#页面滚动)
- [坐标](#坐标)
  - [窗口坐标](#窗口坐标)
  - [文档坐标](#文档坐标)
- [window 对象属性](#window-对象属性)
  - [window.screen 对象](#windowscreen-对象)
  - [window.location 对象](#windowlocation-对象)
  - [window.History 对象](#windowhistory-对象)
  - [window.navigator 对象](#windownavigator-对象)
- [Timing 事件](#timing-事件)
- [Cookies](#cookies)

<br/>

---

<br/>

## window 对象

window 对象代表浏览器的窗口，相当于“全局”。

全局变量是 window 对象的属性，全局函数是 window 对象的方法。

故“`window.`”常常可以省略。

```JS
window.document.getElementById("header");
// 等价于
document.getElementById("header");
```


**一些方法**

| 方法              | 描述             |
| ----------------- | ---------------- |
| window.open()     | 打开新窗口       |
| window.close()    | 关闭当前窗口     |
| window.moveTo()   | 移动当前窗口     |
| window.resizeTo() | 重新调整当前窗口 |

<br/>

## 窗口尺寸

文档可视范围的宽度/高度（内容区域的宽高）：

- `document.documentElement.clientWidth`
- `document.documentElement.clientHeight`

如果使用 windows 对象的属性获取浏览器窗口的内高度/内宽度：

- `window.innerHeight`
- `window.innerWidth`

::: warning

**不建议**使用 `window.innerHeight/Width` 属性。原因是当页面存在滚动条的时候，innerHeight/Width 会忽略滚动条，如果是需要绘制或者定位某些东西的时候，可能会被滚动条所遮挡。

:::

<br/>

## 元素尺寸

元素的一系列宽度属性：（Height类同）

| 属性        | 包括内容                   | 不包括内容           | 读写性 |
| ----------- | -------------------------- | -------------------- | ------ |
| clientWidth | 元素宽度、内边距           | 边框和外边距         | 只读   |
| offsetWidth | 元素宽度、内边距、边框     | 外边距               | 只读   |
| scrollWidth | 元素宽度、内边距、溢出尺寸 | 边框和外边距         | 可读写 |
| style.width | 元素宽度                   | 内边距、边框和外边距 | 可读写 |

::: warning

不建议从 css 直接读取宽高属性。

:::

<br/>

由于历史原因及兼容问题，如果想要获得可靠的窗口大小，最好采取获得它们的最大值：

```js
let scrollHeight = Math.max(
  document.body.scrollHeight, document.documentElement.scrollHeight,
  document.body.offsetHeight, document.documentElement.offsetHeight,
  document.body.clientHeight, document.documentElement.clientHeight
);
```

<br/>

## 页面滚动

滚动页面需要等到 DOM 完全构建好才可以进行。

- 获得当前的滚动状态建议使用 `window.pageYOffset/pageXOffset` 属性。（只读）
    
    > `documentElement.scrollLeft/scrollTop` 属性并不方便且存在 bugs，有些浏览器需要用 `document.body` 代替 `document.documentElement`。

- 改变当前滚动：
    | 描述                          | 方法                                  |
    | ----------------------------- | ------------------------------------- |
    | 绝对定位                      | window.scrollTo(*pageX*, *pageY*)     |
    | 相对当前位置滚动              | window.scrollBy(*x*, *y*)             |
    | *elem* 与 与窗口顶部/底部对齐 | *elem*.scrollIntoView([*topBoolean*]) |

<br/>

## 坐标

在 CSS 中，`窗口坐标`对应的是 `position:fixed`，而`文档坐标`则类似顶部的 `position:absolute`。

### 窗口坐标

窗口的坐标是从窗口的左上角开始计算的。

`elem.getBoundingClientRect()` 方法返回一个 elem 的窗口坐标对象，这个对象有以下这些属性：

| 属性   | 描述                  |
| ------ | --------------------- |
| top    | 元素顶部边缘的 Y 坐标 |
| left   | 元素左边边缘的 X 坐标 |
| right  | 元素右边边缘的 X 坐标 |
| bottom | 元素底部边缘的 Y 坐标 |

<br/>

### 文档坐标

文档坐标类似于绝对定位，其不随页面滚动而改变。

在现在的 JavaScript 中并没有获取一个元素的文档坐标的标准方法，但是我们可以通过 `窗口坐标 + 文档滚动的长度` 计算获得。

```js
// 获取元素的文档坐标
function getCoords(elem) {
  let box = elem.getBoundingClientRect();

  return {
    top: box.top + pageYOffset,
    left: box.left + pageXOffset
  };
}
```

<br/>

## window 对象属性

### window.screen 对象

访问者屏幕宽度/高度：

- screen.width
- screen.height

访问者屏幕可用宽度/可用高度（会减去窗口工具条之类的界面特征，即窗口全屏时的整体尺寸）：

- screen.availWidth
- screen.availHeight

色彩深度/像素深度（两者通常相等，意为表示一种颜色所需的bit数，如16位、24位、32位）：

- screen.colorDepth
- screen.pixelDepth

<br/>

### window.location 对象

| 属性 / 方法            | 描述                       |
| ---------------------- | -------------------------- |
| location.href          | 返回当前页面的 URL         |
| location.hostname      | 返回 web 主机的域名        |
| location.pathname      | 返回当前页面的路径或文件名 |
| location.protocol      | 返回页面的 web 协议        |
| location.assign(*url*) | 加载新文档                 |

<br/>

### window.History 对象

window.history 对象包含浏览器历史，为了保护用户的隐私，JavaScript 访问此对象存在限制。

| 方法              | 描述                         |
| ----------------- | ---------------------------- |
| history.back()    | 等同于在浏览器点击后退按钮   |
| history.forward() | 等同于在浏览器中点击前进按钮 |

<br/>

### window.navigator 对象

window.navigator 对象包含有关访问者的信息。

| 属性 / 方法             | 描述                                     |
| ----------------------- | ---------------------------------------- |
| navigator.appName       | 浏览器应用程序名称                       |
| navigator.appCodeName   | 浏览器应用程序代码名称                   |
| navigator.platform      | 浏览器平台（操作系统）                   |
| navigator.cookieEnabled | cookie 是否启用                          |
| navigator.product       | 浏览器引擎名称                           |
| navigator.appVersion    | 浏览器版本信息                           |
| navigator.userAgent     | 由浏览器发送到服务器的 user-agent header |
| navigator.language      | 浏览器语言                               |
| navigator.onLine        | 浏览器是否在线                           |
| navigator.javaEnabled() | Java 是否已启用                          |

<br/>

## Timing 事件

window 对象允许以指定的时间间隔执行代码,这些时间间隔称为定时事件。

- setTimeout(*function*, *milliseconds*)  
  在等待指定的毫秒数后执行函数。

- clearTimeout(*timeoutVariable*)  
  停止执行 `setTimeout()` 中规定的函数。

- setInterval(*function*, *milliseconds*)  
  持续重复在等待指定的毫秒数后执行该函数。

- clearInterval(*timeoutVariable*)  
  停止执行 `clearInterval()` 中规定的函数。

其中，*timeoutVariable* 为 `setInterval()` 的返回值。

例子：

```html
<button onclick="myVar = setTimeout(myFunction, 3000)">试一试</button>

<button onclick="clearTimeout(myVar)">停止执行</button>
```

<br/>

## Cookies

> Cookie 是在您的计算机上存储在小的文本文件中的数据。当 web 服务器向浏览器发送网页后，连接被关闭，服务器会忘记用户的一切。
>
> 而 cookie 是为了解决“如何记住用户信息”而发明的。当用户访问网页时，他的名字可以存储在 cookie 中。下次用户访问该页面时，cookie 会“记住”他的名字。
>
> Cookie 保存在名称值对中，如：
>
> ```json
> username = Bill Gates
> ```
>
> 当浏览器从服务器请求一个网页时，将属于该页的 cookie 添加到该请求中。这样服务器就获得了必要的数据来“记住”用户的信息。
>
> 如果浏览器已关闭本地 cookie 支持，则以下实例均无法工作。

- JavaScript 可以用 `document.cookie` 属性创建、读取、删除 cookie。

    ```js
    document.cookie = "username=Bill Gates; expires=Sun, 31 Dec 2017 12:00:00 UTC; path=/";
    ```

    通过 `path` 参数，您可以告诉浏览器 cookie 属于什么路径。默认情况下，cookie 属于当前页。

    默认情况下，在浏览器关闭时会删除 cookie。

- 将 `document.cookie` 赋值给一个变量，会获得 cookie 的字符串。
  
- 将时间设置为过去，即可删除 cookie。

    ```js
    document.cookie = "username=; expires=Thu, 01 Jan 1970 00:00:00 UTC; path=/";
    ```
