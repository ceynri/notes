---
title: "npm 指令"
date: "2019-09-03"
---

# npm 指令

## 安装包

```bash
npm install <packagename>
```

install缩写：

```bash
npm i <packagename>
```

重复性操作：

```bash
npm i webpack
npm i babel-core

# 等价
npm i webpack babel-core
```

参数无先后顺序：

```bash
npm i -g webpack
# 等价
npm i webpack -g
```

| 可选参数 | 全称            | 作用                 |
| -------- | --------------- | -------------------- |
| -g       | global          | 全局安装             |
| -D       | devDependencies | 安装到  （开发环境） |
| -S       | dependencies    | 安装到  （上线环境） |

&&命令（常用于-D和-g混合）

```bash
npm i webpack -D && npm i webpack-cli -g
```

一开始没有创建package.json：

```bash
npm init -y
# 会自动检索安装的-S或—D并且重新生成目录
```

| 可选参数 | 全称 | 作用            |
| -------- | ---- | --------------- |
| -y       | yes  | 遇到选择全部yes |
| -n       | no   | 遇到选择全部no  |
