# Git 常见指令 <!-- omit in toc -->

注：本文中带尖括号（`<`、`>`）的标签是需要被替换为对应文本的标记。

## 索引 <!-- omit in toc -->

- [常用操作](#常用操作)
  - [添加文件](#添加文件)
  - [提交文件](#提交文件)
  - [查看暂存状态](#查看暂存状态)
  - [发送至远程仓库](#发送至远程仓库)
  - [克隆其他仓库](#克隆其他仓库)
  - [从远程仓库更新本地](#从远程仓库更新本地)
- [撤销操作](#撤销操作)
  - [撤销最后一次提交](#撤销最后一次提交)
  - [取消暂存的文件](#取消暂存的文件)
  - [删除暂存的文件](#删除暂存的文件)
  - [取消修改/退回文件版本](#取消修改退回文件版本)
- [冷门指令](#冷门指令)
  - [修改远程库地址](#修改远程库地址)

<br>

---

<br>

## 常用操作

### 添加文件

```bash
git add <file>
```

添加 `-A` 或 `-all` 参数，可以一次性添加当前文件夹下所有文件。

### 提交文件

```bash
git commit -m <message>
```

### 查看暂存状态

```bash
git status
```

### 发送至远程仓库

```bash
git push
```

| 参数         | 作用                   |
| ------------ | ---------------------- |
| -f / --force | 强制覆盖远程仓库       |
| -u           | 选择当前为默认仓库分支 |

### 克隆其他仓库

```bash
git clone <url> [renamed-name]
```

### 从远程仓库更新本地

```bash
git pull <远程主机名> [<远程分支名>[:<本地分支名>]]
# 等价于
git fetch <远程主机名> [<远程分支名>[:<本地分支名>]]
git merge FETCH_HEAD
```


## 撤销操作

### 撤销最后一次提交

例子：

```bash
git commit -m 'initial commit'
git add forgotten_file
git commit --amend
```

该情况下，最终只会产生一个提交，第二个提交命令修正了第一个的提交内容。

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

### 删除暂存的文件

不删除物理文件，仅将该文件从缓存中删除：

```bash
git rm -r --cached <file>
```

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

## 冷门指令

收一些我用了一次的指令

### 修改远程库地址

```bash
git remote set-url origin git@github.com:USERNAME/REPOSITORY.git
```

其中的 url 使用 HTTPS 或者 SSh 都可以。


