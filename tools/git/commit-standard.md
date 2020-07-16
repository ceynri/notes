---
title: Git commit 规范
date: 2020-05-08
---

# Git commit 规范

## 前言

观察别人的项目，有时候会发现好的项目的 commit 记录都遵循着`<type>: <subject>`的规则。

好处显而易见：`type`能够第一时间了解到该 commit 的性质，`subject`则是对该 commit 的简短描述。

保持该规范对 commit 的整洁性有着很大的帮助 😄

<br>

## 规范

不过在具体的规范中，我们到底要不要对`type`的种类进行限制呢？首字母到底要不要大写呢？

其实在这方面，早就有人做好了 Git Commit 的自动化代码提交规范工具，比较常见的是 [Commitlint](https://www.npmjs.com/package/@commitlint/config-conventional)，它提出了一些简单的规范：

- feat：新功能（feature）
- fix：修补 bug
- docs：文档（documentation）
- style：格式方面的优化（空格、代码格式化等）
- refactor：代码重构（不是 bug 也不是 feature）
- test：测试
- chore：构建过程或辅助工具等无关紧要的变动

如果 commit 时不存在于以上的 type 中，则该 commit 会被拦截下来提交失败。

当然了，如果觉得这些 type 不够，或者想增加更多的规则，也可以修改其配置文件。

比如加个 publish、breaking 等，也不是不行，但最好能在一开始约定好，频繁地变动会导致规范变得没有意义。

<br>

## 完整规范

我们常用的单行 commit 信息其实只是 commit 的 header 部分，对于完整的 commit，还有 body 与 footer。

```
<type>(<scope>): <subject>

<body>

<footer>
```

一般而言，我们只用使用 header 就可以完整表明，其中的 scope 代表本次 commit 所影响的范围，可以选择性添加。

body 是对 commit 的详细描述，可以写为多行。注意 header、body、footer直接都有一个空行。

footer 则是功能性的，比如本次 commit 关闭某一个 issue。

<br>

## 后记

如果是个人项目，我觉得自己私底下定一下规则就好了，比如我们可以在每个 header 前加上 emoji 表情，甚至用 emoji 代替 header 我觉得都是可行的方案。

只要达到了规范的目的，项目就会变得更加整洁。

上面的规范都是针对有代码的项目的，这里我自己简单地定一个面向文档笔记项目的 commit 规范，供大家参考：

- new：新文章
- add：旧文档增加新内容
- fix：错误内容的修正
- typo：拼写错误
- modify：部分内容修改
- move：文件结构的变动
- rename：文件名更改所引起的相关变动
- remove：删除文件
- chore：其他无关紧要的变动

还有一种更简洁的方法，就是用符号当作 header，冒号`:`也省略掉：

- +：增加新东西
- -：删减部分内容
- *：修改代码
- !：重要变动
- ...

也挺好看的，就是易懂的符号的个数有点受限，对于比较特殊的符号可能就不便于他人理解了。不过毕竟是个人项目，适合自己，看起来舒服就好啦。

<br>
