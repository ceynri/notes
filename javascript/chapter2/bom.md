---
title: "BOM"
date: "2019-09-07"
---

# JavaScript | BOM

## 目录 <!-- omit in toc -->

- [window 对象](#window-对象)
  - [一些方法](#一些方法)
- [窗口尺寸](#窗口尺寸)
- [元素尺寸](#元素尺寸)
- [window.screen 对象](#windowscreen-对象)
- [window.location 对象](#windowlocation-对象)
- [window.History 对象](#windowhistory-对象)
- [window.navigator 对象](#windownavigator-对象)
- [timing 事件](#timing-事件)
- [Cookies](#cookies)
- [滚动](#滚动)
- [元素的尺寸与滚动](#元素的尺寸与滚动)

<br/>

---

<br/>

## window 对象

window 对象代表浏览器的窗口，相当于“全局”。全局变量是 window 对象的属性，全局函数是 window 对象的方法。

```JS
window.document.getElementById("header");
// 等价于
document.getElementById("header");
```

故“`window.`”常常可以省略。

### 一些方法

window.open() - 打开新窗口
window.close() - 关闭当前窗口
window.moveTo() -移动当前窗口
window.resizeTo() -重新调整当前窗口

<br/>

## 窗口尺寸

文档可视范围的宽度/高度（内容区域的宽高）：

- document.documentElement.clientWidth
- document.documentElement.clientHeight

如果使用 windows 对象的属性获取浏览器窗口的内高度/内宽度：

- window.innerHeight
- window.innerWidth

<br/>

## 元素尺寸

元素的一系列宽度属性：（Height类同）

| 属性        | 包括内容                   | 不包括内容           | 读写性 |
| ----------- | -------------------------- | -------------------- | ------ |
| clientWidth | 元素宽度、内边距           | 边框和外边距         | 只读   |
| offsetWidth | 元素宽度、内边距、边框     | 外边距               | 只读   |
| scrollWidth | 元素宽度、内边距、溢出尺寸 | 边框和外边距         | 可读写 |
| style.width | 元素宽度                   | 内边距、边框和外边距 | 可读写 |

不建议从 css 直接读取宽高属性。

<br/>

## window.screen 对象

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

## window.location 对象

| 属性 / 方法            | 描述                       |
| ---------------------- | -------------------------- |
| location.href          | 返回当前页面的 URL         |
| location.hostname      | 返回 web 主机的域名        |
| location.pathname      | 返回当前页面的路径或文件名 |
| location.protocol      | 返回页面的 web 协议        |
| location.assign(*url*) | 加载新文档                 |

<br/>

## window.History 对象

window.history 对象包含浏览器历史，为了保护用户的隐私，JavaScript 访问此对象存在限制。

| 方法              | 描述                         |
| ----------------- | ---------------------------- |
| history.back()    | 等同于在浏览器点击后退按钮   |
| history.forward() | 等同于在浏览器中点击前进按钮 |

<br/>

## window.navigator 对象

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

## timing 事件

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

## 滚动

- 读取当前的滚动：`window.pageYOffset/pageXOffset`

- 改变当前的滚动：
  - `window.scrollTo(pageX,pageY)` — 绝对定位
  - `window.scrollBy(x,y)` — 相对当前位置的滚动
  - `elem.scrollIntoView(top)` — 滚动到正好elem可视的位置（elem 与窗口的顶部/底部对齐）

<br/>

## 元素的尺寸与滚动

元素具有以下几何属性：

- offsetParent — 是最近的有定位属性的祖先元素，或者是 td、th、table、body。
- offsetLeft/offsetTop — 是相对于 offsetParent 的左上角边缘坐标。
- offsetWidth/offsetHeight — 元素的“外部”宽/高 ，边框尺寸计算在内。
- clientLeft/clientTop — 从元素左上角外部到内部的距离，对于从左到右渲染元素的操作系统，它始终是左/顶部边界的宽度，而对于从右到左的操作系统，垂直滚动条在左边，所以 clientLeft 也包括滚动条的宽度。
- clientWidth/clientHeight — 内容的宽度/高度，包括内间距，但没有滚动条。
- scrollWidth/scrollHeight — 内容的宽度/高度，包括可滚动的可视区域外的尺寸，也包括内间距，但不包括滚动条。
- scrollLeft/scrollTop — 从左上角开始的元素的滚动部分的宽度/高度。

除了 scrollLeft/scrollTop 之外，所有属性都是只读的。如果更改，浏览器会使元素滚动。
