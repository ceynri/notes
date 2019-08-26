# 上传至 Github

1. 初始化仓库

    在想要创建 git 仓库的地方打开git窗口（Windows系统下 右键-Git Bash Here），输入 `git init`。

    ```
    $ git init
    Initialized empty Git repository in /Users/michael/learngit/.git/
    ```

1. `git add <file>` 和 `git commit -m <message>` 
   
    ```
    $ git add file1.txt
    $ git add file2.txt file3.txt
    $ git commit -m "add 3 files."
    ```

    当 message 只有一个单词时可以不用引号包起来。

3. 在 Github 上创建仓库

    根据指示输入指令：

    ![github-new-repo](pics/github-new-repo.jpg)

    ```
    git remote add origin https://github.com/HazeAcc/tmp-repo.git
    git push -u origin master
    ```
    其中第一行的url换成你对应的url即可。

4. `git push`

    以后上传文件无需再使用` git push -u origin master`，因为 `-u` 参数已经指定了 `origin` 作为默认远程仓库，在没有其他分支的情况下，直接使用 `git push` 指令即可完成远程仓库与本地仓库的同步。

## 常见问题

1. 如果远程仓库已经有了文件怎么办？

    ![仓库已初始化](pics/q-pull.jpg)

    原因：

    远程库存在文件，需要先 pull 下来。

    解决方法：
    ```
    $ git pull origin master --allow-unrelated-histories
    ```
    然后在vim编辑器模式下编写完 commit 信息后保存即可重新push。

