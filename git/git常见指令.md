# Git 常见指令 <!-- omit in toc -->

注：本文中带尖括号（`<`、`>`）的标签是需要被替换为对应文本的标记。

## 索引 <!-- omit in toc -->

- [常用操作](#常用操作)
  - [添加文件](#添加文件)
  - [提交文件](#提交文件)
  - [查看暂存状态](#查看暂存状态)
  - [发送到其他仓库](#发送到其他仓库)
- [撤销操作](#撤销操作)
  - [撤销最后一次提交](#撤销最后一次提交)
  - [取消暂存的文件](#取消暂存的文件)
  - [删除暂存的文件](#删除暂存的文件)
  - [取消修改/退回文件版本](#取消修改退回文件版本)

<br>

---

<br>

## 常用操作

### 添加文件

```
git add <file>
```

### 提交文件

```
git commit -m <message>
```

### 查看暂存状态

```
git status
```

### 发送到其他仓库

```
push
```

## 撤销操作

### 撤销最后一次提交

例子：

```
$ git commit -m 'initial commit'
$ git add forgotten_file
$ git commit --amend
```

该情况下，最终只会产生一个提交，第二个提交命令修正了第一个的提交内容。

### 取消暂存的文件

```
git reset HEAD <file>
```

`git status` 命令其实自带提醒如何取消：

```
$ git add .
$ git status
On branch master
Changes to be committed:
    (use "git reset HEAD <file>..." to unstage)
 
        modified:   README.txt
        modified:   benchmarks.rb
```

### 删除暂存的文件

不删除物理文件，仅将该文件从缓存中删除：

```
$ git rm -r --cached <file>
```

### 取消修改/退回文件版本

```
$ git checkout -- <file>
```

这同样在 `git status` 命令中有所提示：

```
$ git checkout -- benchmarks.rb
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   README.txt
```

注意：此方法会覆盖你修改好的文件且无法找回，使用前需确保操作正确。建议使用 tashing 和分支来处理此问题。

