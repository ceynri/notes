---
title: "Git 常见指令"
date: "2019-08-22"
---

# Git 常见指令 <!-- omit in toc -->

注：本文中带尖括号（`<`、`>`）的标签是需要被替换为对应文本的标记。

## 索引 <!-- omit in toc -->

- [常用操作](#常用操作)
  - [添加文件](#添加文件)
  - [提交文件](#提交文件)
  - [查看暂存状态](#查看暂存状态)
- [修改操作](#修改操作)
  - [修改最后一次提交](#修改最后一次提交)
  - [修改commit时间](#修改commit时间)
- [撤销操作](#撤销操作)
  - [取消暂存的文件](#取消暂存的文件)
  - [删除暂存的文件](#删除暂存的文件)
  - [取消修改/退回文件版本](#取消修改退回文件版本)
  - [删除某文件的全部提交记录](#删除某文件的全部提交记录)
- [远程仓库](#远程仓库)
  - [添加远程仓库](#添加远程仓库)
  - [发送至远程仓库](#发送至远程仓库)
  - [克隆其他仓库](#克隆其他仓库)
  - [从远程仓库更新本地](#从远程仓库更新本地)
- [冷门指令](#冷门指令)
  - [修改远程库地址](#修改远程库地址)

<br/>

---

<br/>

## 常用操作

### 添加文件

```bash
git add <file>
```

以下参数可以一次性添加所有文件：

| 参数/符号 | 全称             | 区别                                          |
| --------- | ---------------- | --------------------------------------------- |
| `.`       | 即工作区的状态树 | 包括文件内容修改、新文件，不包括被删除文件    |
| `*`       | 通配符           | 会忽视.gitignore 把所有文件加入（其他的不会） |
| `-u`      | `--update`       | 仅监控已经被 add 的文件，不会提交新文件       |
| `-A`      | `--all`          | 既包含删除文件，也会提交新文件                |

<br/>

### 提交文件

```bash
git commit -m <message>
```

<br/>

### 查看暂存状态

```bash
git status
```

<br/>

## 修改操作

### 修改最后一次提交

例子：

```bash
git commit -m 'initial commit'
git add forgotten_file
git commit --amend -m 'initial commit'
```

该情况下，最终只会产生一个提交，第二个提交命令修正了第一个的提交内容。

<br/>

### 修改commit时间

在commit的时候添加参数`--date="<commit-time>"`即可，注意时间要按照格式输入。

例子：修改上次提交（`--amend`）的commit的时间（`--date`）

```bash
git commit --amend --date="Sun, 25 Dec 2016 19:42:09 +0800"
```

<br/>

## 撤销操作

### 取消暂存的文件

```bash
git reset HEAD <file>
```

`git status` 命令其实自带提醒如何取消：

```bash
$ git add .
$ git status
On branch master
Changes to be committed:
    (use "git reset HEAD <file>..." to unstage)

        modified:   README.txt
        modified:   benchmarks.rb
```

<br/>

### 删除暂存的文件

不删除物理文件，仅将该文件从缓存中删除：

```bash
git rm -r --cached <file>
```
`-r` 参数：即 `--recursive`，递归删除目录及其内容（用于文件夹）

<br/>

### 取消修改/退回文件版本

```bash
git checkout -- <file>
```

这同样在 `git status` 命令中有所提示：

```bash
$ git checkout -- benchmarks.rb
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   README.txt
```

注意：此方法会覆盖你修改好的文件且无法找回，使用前需确保操作正确。建议使用 tashing 和分支来处理此问题。

<br/>

### 删除某文件的全部提交记录

如果有一些隐私内容被提交进了 git 仓库，后续当要发布给其他人时想要删掉即可使用本命令。

原理：对所有文件的 commit log 进行重写，然后排除掉想要删掉的某些文件。

```bash
git filter-branch -f --tree-filter 'rm -rf aaa/app.config' HEAD
```

注意提前做好被删除文件的备份。

如果需要 push 到远程仓库，需要：

```bash
git push origin --force
```

<br/>

## 远程仓库

### 添加远程仓库

```bash
git remote add origin <url>
```

如果想修改远程仓库地址：

```bash
git remote set-url origin <new-url>
```

<br/>

### 发送至远程仓库

```bash
git push
```

| 参数         | 作用                   |
| ------------ | ---------------------- |
| -f / --force | 强制覆盖远程仓库       |
| -u           | 选择当前为默认仓库分支 |

<br/>

### 克隆其他仓库

```bash
git clone <url> [renamed-name]
```

<br/>

### 从远程仓库更新本地

```bash
git pull <远程主机名> [<远程分支名>[:<本地分支名>]]
# 等价于
git fetch <远程主机名> [<远程分支名>[:<本地分支名>]]
git merge FETCH_HEAD
```

<br/>

## 冷门指令

收一些我用了一次的指令

### 修改远程库地址

```bash
git remote set-url origin git@github.com:USERNAME/REPOSITORY.git
```

其中的 url 使用 HTTPS 或者 SSh 都可以。

<br/>
