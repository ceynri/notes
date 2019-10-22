---
title: "HTML5 结构元素介绍"
date: "2019-10-15"
---

# HTML5 结构元素介绍

　　刚开始学习 HTML 时，总是对 HTML5 新增的语义化标签的使用情景有所迷糊，在小实战中纠结于到底应该什么时候使用这些标签元素才是合理的。虽然使用这些标签使得页面对搜索引擎来说更加具有可读性，但是错误地使用这些标签，反而会误导搜索引擎，从而影响了页面的SEO。于是，清楚地认识这些标签的使用范围并合理地使用它们是非常有必要的，尽管它们并不会为我们带来什么样式上的变化。

## header

　　header 元素通常用来包含放在页面的头部的内容，除此之外也可以用来作为一个内容区块（如 artice）的顶部内容。

## nav

　　nav 即 navigator 导航栏，用来定义导航链接。将页面具有导航性质的链接元素（如站内导航、页内导航、翻页导航等）归纳于 nav 元素区域内。

## article

　　article 元素往往定义的是一篇比较独立的文章、日志、评论之类的内容，其内部常常包含 header 元素、section 元素与 h1~h6 元素。所谓独立便是页面其他内容与该 article 元素内容无直接关联，在此处更换内容性质类似的 article 并不会影响整个页面的布局。

## section

　　section 元素经常被新手与 div 元素混用。section 元素用于对页面中的某些内容进行“分块”，但 section 元素的内部应该需要有标题，没有标题的内容区块应该使用其他的标签。

　　仅仅是为了选择设置样式的页面容器，应该使用 div 标签。（所以 div 标签在使用频率上要比 section 多很多）

　　同时，如果内容更适合用其他语义化标签（article、aside、nav），优先使用其他标签。

## aside

　　aside 元素用于定义页面的侧边栏，往往内容是一些介绍、内容相关的其他信息甚至广告等。宽度一般小于正文栏。

## footer

　　footer 元素定义定义一个页面或者区域的底部内容，在这方面它和 header 元素非常的相似。一般底部内容都是相关信息或者一些信息标识。

## 示例

最后做一个简单的“无样式”示例，使用以上H5结构元素构建一个页面：

```html
<body>
  <header>
    <h1>个人网站</h1>
    <span>一个兴趣使然的个人网站</span>
  </header>

  <nav>
    <ul>
      <li><a href="#">首页</a></li>
      <li><a href="#">博客</a></li>
      <li><a href="#">关于</a></li>
    </ul>
  </nav>

  <div style="display: flex;">
    <div style="flex: 1;">
      <article>
        <header>
          <h1>一篇文章</h1>
          <span>作者：ceynri</span>
        </header>

        <h2>章节一</h2>
        <p>文段一</p>

        <footer>
          <p>本文允许转载，禁止用于商业用途</p>
        </footer>
      </article>

      <article>
        <h1>评论</h1>
        <section>
          <header>
            <h1>Well</h1>
            <span>评论者：Tom</span>
          </header>
          <p>Explosion is art!</p>
        </section>

        <section>
          <header>
            <h1>OMG!</h1>
            <span>评论者：Mary</span>
          </header>
          <p>I'm coming</p>
        </section>
      </article>
    </div>

    <aside>
      <h1>广告</h1>
      <img src="ad.png" alt="ad">
    </aside>
  </div>

  <footer>
    <a href="#">关于本站</a>
    <a href="#">友情链接</a>
  </footer>
</body>
```

效果如下：

![h5-structure-tag-exercise-marked.jpg](https://i.loli.net/2019/10/22/ycTx5WwKM6FoG4C.jpg)
