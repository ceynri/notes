---
title: "Hexo 指令"
date: "2019-09-02"
---

# Hexo 指令

官网指令文档：[指令 | Hexo](https://hexo.io/zh-cn/docs/commands)

## 初始指令

### 安装 Hexo

```bash
npm install hexo -g
```

### 升级 Hexo

```bash
npm update hexo -g
```

### 初始化博客

```bash
hexo init [folder]
```

如果省略folder则默认在当前文件夹建立网站。

## 命令简写

| 简写              | 全称                | 作用         |
| ----------------- | ------------------- | ------------ |
| hexo n "我的博客" | hexo new "我的博客" | 新建文章     |
| hexo g            | hexo generate       | 生成         |
| hexo s            | hexo server         | 启动服务预览 |
| hexo d            | hexo deploy         | 部署         |

## 即时生成

```bash
hexo generate -w
```

## 服务器指令

hexo server #Hexo会监视文件变动并自动更新，无须重启服务器
hexo server -s #静态模式
hexo server -p 5000 #更改端口
hexo server -i 192.168.1.1 #自定义 IP
hexo clean #清除缓存，若是网页正常情况下可以忽略这条命令
