---
title: "JavaScript 性能"
date: "2019-08-29"
---

# JavaScript | 性能 <!-- omit in toc -->

目前 JavaScript 语言性能越来越好，个人电脑的平均配置也越来越高，但是注重良好的编程规范仍然是优秀编程者的素养。

## 目录 <!-- omit in toc -->

- [JS 代码](#js-代码)
  - [减少循环中的活动](#减少循环中的活动)
  - [避免新建不必要的变量](#避免新建不必要的变量)
- [DOM 操作](#dom-操作)
  - [减少 DOM 访问](#减少-dom-访问)
  - [减少 DOM 操作](#减少-dom-操作)
  - [减少页面 reflow](#减少页面-reflow)
  - [缩减 DOM 规模](#缩减-dom-规模)
- [结构](#结构)
  - [延迟 JavaScript 加载](#延迟-javascript-加载)
- [待补充](#待补充)

<br/>

---

<br/>

## JS 代码

### 减少循环中的活动

若循环中存在某个对象的属性经常被访问而循环不会对其进行修改，可以将其提取出来。

```js
// 重构前
var i;
for (i = 0; i < arr.length; i++) {
    // ...
}

// 重构后
var i;
var l = arr.length;
for (i = 0; i < l; i++) {
    // ...
}
```

<br/>

### 避免新建不必要的变量

```js
// 重构前
var fullName = firstName + " " + lastName;
document.getElementById("demo").innerHTML = fullName; 

// 重构后
document.getElementById("demo").innerHTML = firstName + " " + lastName;
```

注意可读性与性能之间的权衡。

<br/>

## DOM 操作

### 减少 DOM 访问

访问 HTML DOM 的速度很慢，如果需要多次访问同一个 DOM 元素，可以将其作为本地变量保存下来使用：

<br/>

### 减少 DOM 操作

构建一个列表。我们可以用两种方式：

- 在循环体中 createElement 并 append 到父元素中。
- 在循环体中拼接 HTML 字符串，循环结束后写父元素的 innerHTML。

第一种方法看起来比较标准，但是每次循环都会对 DOM 进行操作，性能极低。在这里推荐使用第二种方法。

<br/>

### 减少页面 reflow

页面 reflow 是非常耗时的行为，非常容易导致性能瓶颈。下面一些场景会触发浏览器的reflow：

- DOM元素的添加、修改（内容）、删除。
- 应用新的样式或者修改任何影响元素布局的属性。
- Resize浏览器窗口、滚动页面。
- 读取元素的某些属性（offsetLeft/Top/Height/Width、scrollTop/Left/Width/Height、clientTop/Left/Width/Height、getComputedStyle()、currentStyle(in IE))。

<br/>

### 缩减 DOM 规模

编写 HTML 时，尽量保持 HTML DOM 中较少的元素数量，可以提高页面加载速度。

一个较小的 DOM 使每一次搜索 DOM（比如 getElementsByTagName）都更加快速。

<br/>

## 结构

### 延迟 JavaScript 加载

下载脚本会阻塞其他下载，把脚本放在页面底部可以使浏览器先加载页面。

1. 在 script 标签中使用 defer="true"。  
    defer 属性规定脚本应在页面完成解析后执行（只适用于外部脚本）。

2. 通过代码向页面添加脚本：

    ```html
    <script>
    window.onload = downScripts;

    function downScripts() {
        var element = document.createElement("script");
        element.src = "myScript.js";
        document.body.appendChild(element);
    }
    </script>
    ```

<br/>

## 待补充
