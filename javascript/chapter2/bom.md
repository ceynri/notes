# JavaScript | BOM


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

## Window 的尺寸与滚动

几何：

- 文档可视范围的宽度/高度（内容区域的宽高）：`document.documentElement.clientWidth/Height`

整个文档的宽度/高度，包括滚动区域外的部分：

```js
let scrollHeight = Math.max(
  document.body.scrollHeight, document.documentElement.scrollHeight,
  document.body.offsetHeight, document.documentElement.offsetHeight,
  document.body.clientHeight, document.documentElement.clientHeight
);
```

滚动：

- 读取当前的滚动：`window.pageYOffset/pageXOffset`

- 改变当前的滚动：
  - `window.scrollTo(pageX,pageY)` — 绝对定位
  - `window.scrollBy(x,y)` — 相对当前位置的滚动
  - `elem.scrollIntoView(top)` — 滚动到正好elem可视的位置（elem 与窗口的顶部/底部对齐）
