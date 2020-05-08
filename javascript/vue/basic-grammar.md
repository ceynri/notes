---
title: "Vue 基础语法入门"
date: "2019-11-13"
---

# Vue 基础语法入门

Vue 可能是近年来最火的前端框架了，哪怕你没有接触过前端编程，或许都听过 Vue 在前端框架中的地位——它的主要编写者为国人，它的简单易懂性使得几乎所有的入门教程都会推荐从 Vue 入手前端框架，它在 Github 上的 Star 数能排进前三......从中不难看出 Vue 的优越性、实用性与火爆程度。故学习了解并掌握 Vue 逐渐变成入门前端的必修课之一了。

当然，在学习 Vue 之前还是应该先掌握 HTML、CSS 和 JavaScript 的基本知识为佳，有了良好的基础才不会影响之后的学习。

<br/>

## 引入 Vue.js

引入 Vue.js 的最简单的方式便是直接在 head 标签中添加 script 标签引用 vue.js 库，从而允许在接下来的内容中使用 Vue 的相关语法。

```html
<!-- 以下二选一 -->
<!-- 开发环境版本，包含了有帮助的命令行警告 -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<!-- 生产环境版本，优化了尺寸和速度 -->
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
```

我们学习的时候使用“开发环境版本”比较合适，报错时会提供有帮助的命令行警告。

<br/>

## 声明式渲染

一个简单的样例：

```html
<div id="root">
    {{content}}
</div>
```

```js
new Vue({
	el: '#root',
    data: {
    	content: 'Hello Vue!'
	}
})
```

结果：

<div id="root">
    Hello Vue!
</div>

<br/>

我们可以看到，在 HTML 文档内：

- 我们创建了一个具有`id`的元素，然后在其中加入了一个“带有双重花括号的文本”。
- 在脚本中则 new 了一个`Vue`对象实例，对象的参数是一个对象，其包含了`el`、`data`选项。
- 通过设置`el`（element）选项的值，我们建立了该 Vue 实例与`#root`元素的关联。
- 而`data`的值是一个包含和 HTML 中的`content`相同的属性的对象。
- 其产生的结果是使用`content`属性的值 'Hello Vue!' 替换了 HTML 中的 {{content}}。

这便是最简单的一个 Vue 应用，它将数据与 DOM 建立的关联，通过更改数据可以直接更改页面内容。接下来我们介绍这些代码所表达的含义。

<br/>

## 插值

### 插值表达式

对于上面的例子，`{{content}}`其实就是一个遵从“Mustache”语法的被称为**插值表达式**的标记，当我们在 HTML 中使用花括号包裹一个名称时，便可以在之后的 Vue 脚本中通过这个名称改变对应插值的内容。

在 MVVM 模型中，它也被称为“挂载点”。

虽然这里使用的是简单的数据名访问数据，但在`{{`与`}}`之间其实支持简单的 JavaScript 表达式。（如果需要复杂的计算，则需要通过后文的[计算属性](#计算属性)实现。）

```html
{{ ok ? 'yes_data' : 'no_data' }}
{{ message.split('').reverse().join('') }}
```

<br/>

### 文本

虽然插值表达式能够让我们将 Vue 传来的数据插入 HTML 中，但是当网络不好时，网页有可能会先显示插值表达式的原本的内容，之后加载完成才被替换为表达式对应的数据。为了避免这种尴尬的情况，有一个属性能够胜任——`v-text`。

```html
<div id="root">
    <div v-text="content"></div>
</div>
```

这种方式同样可以将名为`content`的数据插入 HTML 文档中。

那么直接插值的好处在哪呢？

实际上，使用`v-text`这样的属性会完全替换该元素内的所有内容（`innerHTML`），所以插值表达式有着更好的灵活性，根据不同的情景选择合适的方法才是最好的。

<br/>

### 原始 HTML

使用`v-text`或者插值表达式插入的数据会自动转义可能存在的 HTML 标签变成纯文本，如果想要保留数据中的 HTML 标签，用类似的方法使用`v-html`属性即可。（最好不要使用`v-html`来复合局部模板，因为 Vue 不是基于字符串的模板引擎。）

<br/>

### 绑定与双向绑定

在 HTML 中，为某一个属性添加**绑定**可以在其前面添加`v-bind:`，数据的改变会影响到该属性的值，而该属性对于`v-bind`称为“参数”。

`v-bind:`的**缩写**为`:`。

```html
<div id="root">
	<div v-bind:title="title">hover me</div>
	<div :title="title">hover me</div>
</div>
```

```js
new Vue({
	el: '#root',
    data: {
        title: 'this is title',
	}
})
```

如果想要让属性值反过来也能够影响数据值，则需要添加**双向绑定**`v-model`。

```html
<div id="root">
	姓名：<input v-model="name" />
	<div>{{name}}</div>
</div>
```

```js
new Vue({
	el: '#root',
    data: {
    	name: 'name'
	}
})
```

这个例子可以在 input 元素内容改变时，页面文本内容同时发生改变。

注意到`v-model`并没有在后面指定具体的属性，而是直接赋值，这是因为它会根据控件类型自动选取正确的方法来更新元素。

例如 text 和 textarea 元素使用 `value` 属性和 `input` 事件，checkbox 和 radio 使用 `checked` 属性和 `change` 事件。

它是一个语法糖，我们可以认为它会实现我们直觉上所期待的效果。

<br/>

## 实例选项

### 数据

`data`选项用来放置关于该 Vue 实例的数据。

```js
let vm = new Vue({
    //...
    data: {
        content: 'this is content'
    }
})

console.log(vm.$data.content === vm.content);    // true
// 出于保护属性不被用户更改的目的，Vue 实例的选项如`data`会在前面加上`$`
```

所以在 Vue 对象内的方法中，当我们需要访问数据时可以使用`this.`+`数据名`的方式得到数据。

<br/>

### 模板

**模板**是一种使用`template`选项将原本写在 HTML 中的内容放到 Script 里的一种方式。

```js
new Vue({
	el: '#root',
    template: '<h1>hello {{content}}!</h1>',
    data: {
    	content: 'Vue!'
	}
})
```

模板内的标签不会转义，且它会覆盖原标签内的所有内容。

template 的最外层应该使用一个 DOM 标签（比如样例中的`<h1>`）去包裹它，否则是无法被渲染的。

一开始我们可能不会用到它，但它在组件中应用很广。

<br/>

### 方法

方法对应的是`methods`选项。

注意对于`data`内的数据名称，需要在前面添加`this.`才合法。

```js
new Vue({
	el: '#root',
    data: {
    	content: 'Hello Vue!'
	},
    methods: {
    	handleClick: function() {
    		this.content = 'Hello World!'
		}
	}
})
```

> 请不要使用箭头函数代替`function() {...}`，因为箭头函数没有`this`指针，这通常会导致各种错误。

<br/>

### 计算属性

在 JavaScript 中存在的`计算属性`概念在 Vue 中也有类似的角色。通过`computed`属性我们可以给一个数据通过计算获得数据值。

```html
<div id="root">
	姓：<input v-model="firstName">
    名：<input v-model="lastName">
    <div>{{fullName}}</div>
</div>
```

```js
new Vue({
	el: '#root',
    data: {
        firstName: '',
        lastName: ''
	},
    computed: {
        fullName: function () {
            return this.firstName + ' ' + this.lastName
        }
    }
})
```

该例子中`fullName`由`firstName`与`lastName`相加得到。

需要注意的是，使用函数可以达到类似的效果：将一些数据计算后返回一个想要的结果。但是，计算属性的优点在于它并不是每次使用`fullName`都要重新计算，它具有一个缓存，当且仅当因为计算该数据而被引用的数据（firstName 与 lastName）发生变化时，才会引起重新计算。故计算属性在不经常改变数据值时，计算属性的性能是相对较好的。除非你不需要缓存，才建议使用方法的形式实现这样的功能。

<br/>

### 侦听属性

Vue 使用`watch`可以侦听一些数据的变化，只要数据一变化就会调用相应的函数。

```js
new Vue({
	el: '#root',
    data: {
        count: 0
	},
    watch: {
        fullName: function () {
            this.count++
        }
    },
})
```

该例中每当`fullName`变化一次，都会使`count`加一。

侦听属性有时候容易被滥用，实际上一些功能可以直接使用计算属性更加合适，故当使用侦听属性时，需要注意这个效果是否更合适用计算属性实现。

<br/>

## 标签属性

### 事件

在编写 HTML 时为元素添加`v-on`属性可以为元素添加**事件监听**，最简单的点击事件监听便是`v-on:click`。

`v-on:`的缩写是`@`。

```html
<div id="root">
    <div v-on:click="handleClick">{{content}}</div>
    <div @click="handleClick">{{content}}</div>
</div>
```

<br/>

### 隐藏与显示

Vue 提供了`v-if`与`v-show`两种隐藏/显示 HTML 标签的方式，当作为它们属性值的数据的值为`false`时，该元素会从 HTML 文档中隐藏。

```html
<div id="root">
    <div v-if="show">if</div>
    <div v-show="show">show</div>
    <button @click="handleClick">toggle</button>
</div>
```

```js
new Vue({
	el: '#root',
    data: {
        show: true
	},
    methods: {
        handleClick: function () {
            // show值取反
            this.show = !this.show
        }
    }
})
```

虽然点击按钮后，两个 div 都会被隐藏，但是不同之处在于，`v-if`会将元素节点从 HTML DOM 树中移除，而`v-show`则会为元素添加`display: hidden;`样式。

如果需要多次隐藏与显示，`v-show`的性能会相对较好；而如果只需要一次或者有去除节点的需要，使用`v-if`也是有必要的。

<br/>

### 循环

对于可迭代类型的数据，Vue 支持使用`v-for`循环迭代数据的元素，创建多个具有相同结构的 HTML 元素。这在生成列表、表格等重复的有规律的元素时非常实用。

```html
<div id="root">
    <ul>
        <li v-for="item of list">{{item}}</li>
    </ul>
</div>
```

```js
new Vue({
	el: '#root',
    data: {
        list: [1, 2, 3]
	}
})
```

效果如下：


<div id="root">
    <ul>
        <li>1</li>
        <li>2</li>
        <li>3</li>
    </ul>
</div>

<br/>

我们会注意到`v-for`内的写法，这是一个“迭代元素名 of 被迭代数据”的格式，类似于一般编程语言中的 for 循环迭代写法，而“迭代元素名”`item`则会在本元素节点中作为一个名称可以被使用。于是最终会生成`list`数组长度个数的列表。

我们也可以换种写法，获得迭代所使用的`key`值。

```html
<div id="root">
    <ul>
        <li v-for="(item, index) of list" :key="index">{{item}}</li>
    </ul>
</div>
```

`(item, index)`可以同时取出元素与元素所对应的索引`key`。

在这里`:key="index"`可以省略，因为默认迭代使用的就是`list`数据的`key`。但如果当你需要指定特定的`key`，比如在迭代一个对象数组时，指定特定的属性作为`key`,有助于我们绑定`key`与`value`。

```js
new Vue({
	el: '#root',
    data: {
        list: [
            { id: 1, name: '小明' },
			{ id: 2, name: '小红' },
            { id: 3, name: '小李' }
		]
	}
})
```

```html
<div id="root">
    <ul>
        <li v-for="(item, i) of list" :key="item.id">{{item.name}}</li>
    </ul>
</div>
```

这个时候当我们之后再往`list`中间插入数据，并不会像数组一样打乱索引`key`，从而保持`key`值与`value`一一对应的关系。

另外值得注意的是，虽然在 JavaScript 的 for 循环语句中，`for...in...`（遍历以原始插入顺序迭代对象的可枚举属性）与`for...of...`（对可迭代对象循环遍历其定义的要迭代的数据，如value）表达的意思并不一样，但在 Vue 中它们两个是相同的，所以一般而言使用`for...in...`也没有问题。

<br/>
