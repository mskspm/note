<p style="text-align:right;color:red;font-style:italic" >2023年7月5日</p>

# 通过`git`实现文件上传到`GitHub`仓库

> 详细的Git教程：[Git教程 - 廖雪峰的官方网站 (liaoxuefeng.com)](https://www.liaoxuefeng.com/wiki/896043488029600)

# 自己的一些主要操作

1. 用命令`git add`告诉Git，把文件添加到仓库：

   ```
   $ git add readme.txt //readme.txt is a file
   ```

   执行上面的命令，没有任何显示，说明添加成功。

2. 用命令`git commit`告诉Git，把文件提交到仓库：

   ```
   $ git commit -m "wrote a readme file"
   ```

   `git commit`命令，**`-m`后面输入的是本次提交的说明**，可以输入任意内容，当然最好是有意义的，这样你就能从历史记录里方便地找到改动记录。

3. 把本地`master`分支的最新修改推送至GitHub

   ```
   $ git push origin master
   ```

   
   
   
   