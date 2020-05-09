---
title: "上传至 Github"
date: "2019-08-24"
---

# 从本地仓库上传至 Github

1. 初始化仓库

    在想要创建 git 仓库的地方打开git窗口（Windows系统下 右键-Git Bash Here），输入 `git init`。

    ```bash
    $ git init
    Initialized empty Git repository in /Users/michael/learngit/.git/
    ```

2. `git add <file>` 和 `git commit -m <message>`

    ```bash
    git add file1.txt
    git add file2.txt file3.txt
    git commit -m "add 3 files."
    ```

    当 message 只有一个单词时可以不用引号包起来。

3. 设置用户名与邮箱（如果没有设置的话）

    ```bash
    git config --global user.name "<你的GitHub用户名>"
    git config --global user.email "<你的GitHub注册邮箱>"
    ```

4. 生成并设置 ssh 密钥文件（如果你是第一次在这个电脑上传到github上）

    ```bash
    ssh-keygen -t rsa -C "<你的GitHub注册邮箱>"
    ```

    遇到询问直接回车（选择默认），然后找到生成的.ssh的文件夹（应该会有输出提示其位置）中的id_rsa.pub密钥，将内容全部复制。

    打开 Github 的 [SSH and GPG keys](https://github.com/settings/keys) 页面，选择 New SSH key

    标题任意，然后将刚刚复制的 id_rsa.pub 内容粘贴进去，最后点击Add SSH key。

    可以在 .ssh 文件夹 Git Bash 中检测 GitHub 公钥设置是否成功，输入 `ssh git@github.com`

    > 设置GitHub密钥原因：
    >
    > 通过非对称加密的公钥与私钥来完成加密，公钥放置在GitHub上，私钥放置在自己的电脑里。GitHub要求每次推送代码都是合法用户，所以每次推送都需要输入账号密码验证推送用户是否是合法用户，为了省去每次输入密码的步骤，采用了ssh，当你推送的时候，git就会匹配你的私钥跟GitHub上面的公钥是否是配对的，若是匹配就认为你是合法用户，则允许推送。这样可以保证每次的推送都是正确合法的。

5. 在 Github 上创建仓库

    根据指示输入指令：

    ![github-new-repo]

    ```bash
    # 指定远程仓库
    git remote add origin https://github.com/HazeAcc/tmp-repo.git
    # push到远程仓库
    git push -u origin master
    ```

    其中第一行的url换成你对应的url即可。

6. `git push`

    以后上传文件无需再使用 `git push -u origin master`，因为 `-u` 参数已经指定了 `origin` 作为默认远程仓库，在没有其他分支的情况下，直接使用 `git push` 指令即可完成远程仓库与本地仓库的同步。

## 常见问题

1. 如果远程仓库已经有了文件怎么办？

    ![仓库已初始化]

    原因：

    远程库存在文件，需要先 `pull` 下来。

    解决方法：

    ```bash
    git pull origin master --allow-unrelated-histories
    ```

    然后在 vim 编辑器模式下编写完 commit 信息后保存即可重新 push。

    另：如果你确认远程仓库里的文件都不需要或者可以被本地文件替代，可以在 push 时添加 `-f` 或 `--force` 参数，会强制覆盖远程仓库的文件。但这是一个需要谨慎使用的参数，特别是在团队合作中。

<!-- 变量区 -->

[github-new-repo]: https://i.loli.net/2019/09/08/IYie7NqmvhF1Wjc.jpg

[仓库已初始化]: https://i.loli.net/2019/09/08/x2v7yieZUNnHYC1.jpg
