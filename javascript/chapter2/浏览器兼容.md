---
title: "浏览器兼容"
date: "2019-08-27"
---

# 浏览器兼容

*未整理*

## 目录 <!-- omit in toc -->

## 添加事件监听器

```js
var x = document.getElementById("myBtn");
if (x.addEventListener) {                    // 针对主流浏览器，除了 IE 8 及更正版本
    x.addEventListener("click", myFunction);
} else if (x.attachEvent) {                  // 针对 IE 8 及更早版本
    x.attachEvent("onclick", myFunction);
}
```
