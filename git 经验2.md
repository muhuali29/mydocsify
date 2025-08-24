

# git 经验

1. 官网下载安装程序

2. 安装完成后，在开始菜单里找到“Git”->“Git Bash”，蹦出一个类似命令行窗口的东西，就说明Git安装成功！或右键菜单有Git Bash。

3. 打开Git Bash输入

   ```
   $ git config --global user.name "Your Name"
   $ git config --global user.email "email@example.com"
   ```

   

4. 注意`git config`命令的`--global`参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址。

5. Git Bash中进入目标目录，或cd 拖入文件夹，通过`git init`命令把这个目录变成Git可以管理的仓库：

## 实战步骤

```
$ git add readme.txt  //添加到工作区
```

```
$ git commit -m "说明文字"  //提交到仓库
```

```
$ git status    //查看工作区文件状态
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   readme.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

```
$ git diff readme.txt  //查看文件修改的内容 
```

```
$ git log --pretty=oneline  //显示提交记录、id
```

> 首先，Git必须知道当前版本是哪个版本，在Git中，用`HEAD`表示当前版本，也就是最新的提交`1094adb...`（注意我的提交ID和你的肯定不一样），上一个版本就是`HEAD^`，上上一个版本就是`HEAD^^`，当然往上100个版本写100个`^`比较容易数不过来，所以写成`HEAD~100`。
>
> 现在，我们要把当前版本`append GPL`回退到上一个版本`add distributed`，就可以使用`git reset`命令：

```
$ git reset --hard HEAD^
$ git reset --hard 1094a
```

> 现在，你回退到了某个版本，关掉了电脑，第二天早上就后悔了，想恢复到新版本怎么办？找不到新版本的`commit id`怎么办？
>
> 在Git中，总是有后悔药可以吃的。当你用`$ git reset --hard HEAD^`回退到`add distributed`版本时，再想恢复到`append GPL`，就必须找到`append GPL`的commit id。Git提供了一个命令`git reflog`用来记录你的每一次命令：

```
$ git reflog
e475afc HEAD@{1}: reset: moving to HEAD^
1094adb (HEAD -> master) HEAD@{2}: commit: append GPL
e475afc HEAD@{3}: commit: add distributed
eaadf4e HEAD@{4}: commit (initial): wrote a readme file
```

现在总结一下：

- `HEAD`指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令`git reset --hard commit_id`。
- 穿梭前，用`git log`可以查看提交历史，以便确定要回退到哪个版本。
- 要重返未来，用`git reflog`查看命令历史，以便确定要回到未来的哪个版本。

![git-repo](https://www.liaoxuefeng.com/files/attachments/919020037470528/0)



```
$ git checkout -- readme.txt  //撤销修改
git checkout -- file命令中的--很重要，没有--，就变成了“切换到另一个分支”的命令，我们在后面的分支管理中会再次遇到git checkout命令。
```

> 命令`git checkout -- readme.txt`意思就是，把`readme.txt`文件在工作区的修改全部撤销，这里有两种情况：
>
> 一种是`readme.txt`自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
>
> 一种是`readme.txt`已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。
>
> 总之，就是让这个文件回到最近一次`git commit`或`git add`时的状态。



------

## 如果已添加到暂存区，还没commit，可撤销

1. ```
   $ git reset HEAD readme.txt   //用命令git reset HEAD <file>可以把暂存区的修改撤销掉（unstage），重新放回工作区
   ```

2. `git reset`命令既可以回退版本，也可以把暂存区的修改回退到工作区。当我们用`HEAD`时，表示最新的版本。

   再用`git status`查看一下，现在暂存区是干净的，工作区有修改：

3. ```
    git checkout -- readme.txt  //再撤回工作区的修改       测试直接来这一步试试
   ```

4. ==直接来上一步试试==



> 现在，假设你不但改错了东西，还从暂存区提交到了版本库，怎么办呢？还记得[版本回退](https://www.liaoxuefeng.com/wiki/896043488029600/897013573512192)一节吗？可以回退到上一个版本。不过，这是有条件的，就是你还没有把自己的本地版本库推送到远程。还记得Git是分布式版本控制系统吗？我们后面会讲到远程版本库，一旦你把`stupid boss`提交推送到远程版本库，你就真的惨了……





### 小结

又到了小结时间。

场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令`git checkout -- file`。

场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令`git reset HEAD <file>`，就回到了场景1，第二步按场景1操作。

场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考[版本回退](https://www.liaoxuefeng.com/wiki/896043488029600/897013573512192)一节，不过前提是没有推送到远程库。





### 实验

添加到暂存区后又做了修改，如何解决

1. 测试一、git checkout -- readme.txt 
2. 测试二、先$ git reset HEAD readme.txt   后git checkout -- readme.txt 



### 删除

1. 鼠标右键删除文件，或rm 文件名
2. 确定要删除git rm 文件名；再提交git cmmit；就从版本库中删除了。
3. 如果第一步误删了，因为版本库中还有，git checkout -- 文件名即可恢复。



## 远程仓库

1. 由于你的本地Git仓库和GitHub仓库之间的传输是通过SSH加密的，所以，需要一点设置：创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有`id_rsa`和`id_rsa.pub`这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key：

   ```
   $ ssh-keygen -t rsa -C "youremail@example.com"
   ```

   

2. 如果一切顺利的话，可以在用户主目录里找到`.ssh`目录，里面有`id_rsa`和`id_rsa.pub`两个文件，这两个就是SSH Key的秘钥对，`id_rsa`是私钥，不能泄露出去，`id_rsa.pub`是公钥，可以放心地告诉任何人。

3. 登陆GitHub，打开“Account settings”，“SSH Keys”页面：

   然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴`id_rsa.pub`文件的内容：

   > 为什么GitHub需要SSH Key呢？因为GitHub需要识别出你推送的提交确实是你推送的，而不是别人冒充的，而Git支持SSH协议，所以，GitHub只要知道了你的公钥，就可以确认只有你自己才能推送。
   >
   > 当然，GitHub允许你添加多个Key。假定你有若干电脑，你一会儿在公司提交，一会儿在家里提交，只要把每台电脑的Key都添加到GitHub，就可以在每台电脑上往GitHub推送了。
   >
   > 最后友情提示，在GitHub上免费托管的Git仓库，任何人都可以看到喔（但只有你自己才能改）。所以，不要把敏感信息放进去。
   >
   > 如果你不想让别人看到Git库，有两个办法，一个是交点保护费，让GitHub把公开的仓库变成私有的，这样别人就看不见了（不可读更不可写）。另一个办法是自己动手，搭一个Git服务器，因为是你自己的Git服务器，所以别人也是看不见的。这个方法我们后面会讲到的，相当简单，公司内部开发必备。
   >
   > 确保你拥有一个GitHub账号后，我们就即将开始远程仓库的学习。

4.  为了验证是否成功，在git bash下输入：$ ssh -T git@github.com ,如果是第一次的会提示是否continue，输入yes就会看到：You've successfully authenticated, but GitHub does not provide shell access 。这就表示已成功连上github。



------

# 第二次经验

### 在Windows上安装Git

1. 在Windows上使用Git，可以从Git官网直接[下载安装程序](https://git-scm.com/downloads)，然后按默认选项安装即可。

安装完成后，在开始菜单里找到“Git”->“Git Bash”，蹦出一个类似命令行窗口的东西，就说明Git安装成功！



![install-git-on-windows](https://www.liaoxuefeng.com/files/attachments/919018718363424/0)

2. 安装完成后，输入设置用户名和邮箱

   ```
   $ git config --global user.name "Your Name"
   $ git config --global user.email "email@example.com"
   ```

   > 因为Git是分布式版本控制系统，所以，每个机器都必须自报家门：你的名字和Email地址。你也许会担心，如果有人故意冒充别人怎么办？这个不必担心，首先我们相信大家都是善良无知的群众，其次，真的有冒充的也是有办法可查的。
   >
   > 注意`git config`命令的`--global`参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址。

------



### 创建版本库

1. 选择一个合适的地方，创建一个空目录或手动新建一个目录：

   ```
   $ mkdir learngit
   $ cd learngit
   $ pwd   //显示当前目录
   /Users/michael/learngit
   ```

2. 第二步，通过`git init`命令把这个目录变成Git可以管理的仓库：

   ```
   $ git init
   Initialized empty Git repository in /Users/michael/learngit/.git/
   ```

   

3. 在新建的目录下创建一个测试文本文件，写入内容

   - 第一步用命令`git add`告诉Git，把文件添加到仓库：

     ```
     $ git add readme.txt
     ```

   - 第二步，用命令`git commit`告诉Git，把文件提交到仓库

     ```
     $ git commit -m "wrote a readme file"
     [master (root-commit) eaadf4e] wrote a readme file
      1 file changed, 2 insertions(+)
      create mode 100644 readme.txt
     ```

     > 简单解释一下`git commit`命令，`-m`后面输入的是本次提交的说明，可以输入任意内容，当然最好是有意义的，这样你就能从历史记录里方便地找到改动记录。
     >
     > 嫌麻烦不想输入`-m "xxx"`行不行？确实有办法可以这么干，但是强烈不建议你这么干，因为输入说明对自己对别人阅读都很重要。实在不想输入说明的童鞋请自行Google，我不告诉你这个参数。
     >
     > `git commit`命令执行成功后会告诉你，`1 file changed`：1个文件被改动（我们新添加的readme.txt文件）；`2 insertions`：插入了两行内容（readme.txt有两行内容）。

   - ### 小结

     现在总结一下今天学的两点内容：

     初始化一个Git仓库，使用`git init`命令。

     添加文件到Git仓库，分两步：

     1. 使用命令`git add <file>`，注意，可反复多次使用，添加多个文件；
     2. 使用命令`git commit -m <message>`，完成。

------



### 查看工作区状态与修改的内容

#### 小结

- 要随时掌握工作区的状态，使用`git status`命令。
- 如果`git status`告诉你有文件被修改过，用`git diff`可以查看修改内容。

------



### 版本回退，==针对每次add并commit到版本库==

```
$ git log --pretty=oneline   //美化显示在一行上
1094adb7b9b3807259d8cb349e7df1d4d6477073 (HEAD -> master) append GPL
e475afc93c209a690c39c13a46716e8fa000c366 add distributed
eaadf4e385e865d25c48e7ca9c8395c3f7dfaef0 wrote a readme file
$ git log   //查看提交到版本库的日志
```

> 首先，Git必须知道当前版本是哪个版本，在Git中，用`HEAD`表示当前版本，也就是最新的提交`1094adb...`（注意我的提交ID和你的肯定不一样），上一个版本就是`HEAD^`，上上一个版本就是`HEAD^^`，当然往上100个版本写100个`^`比较容易数不过来，所以写成`HEAD~100`。

```
$ git reset --hard HEAD^
HEAD is now at e475afc add distributed
```

```
$ git reset --hard 1094a     //返回到指定版本1094a
HEAD is now at 83b0afe append GPL
```

版本号可用命令git reflog查看

```
$ git reflog
e475afc HEAD@{1}: reset: moving to HEAD^
1094adb (HEAD -> master) HEAD@{2}: commit: append GPL
e475afc HEAD@{3}: commit: add distributed
eaadf4e HEAD@{4}: commit (initial): wrote a readme file
```

现在总结一下：

- `HEAD`指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令`git reset --hard commit_id`。
- 穿梭前，用`git log`可以查看提交历史，以便确定要回退到哪个版本。
- 要重返未来，用`git reflog`查看命令历史，以便确定要回到未来的哪个版本。



------

### 工作区和暂存区

1. #### 工作区（Working Directory）

   就是你在电脑里能看到的目录，就是自己新建的文件夹，比如我的`learngit`文件夹就是一个工作区：

2. #### 版本库（Repository）

   工作区有一个隐藏目录`.git`，这个不算工作区，而是Git的版本库。

   Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支`master`，以及指向`master`的一个指针叫`HEAD`。

   ![git-repo](https://www.liaoxuefeng.com/files/attachments/919020037470528/0)

   > 分支和`HEAD`的概念我们以后再讲。
   >
   > 前面讲了我们把文件往Git版本库里添加的时候，是分两步执行的：
   >
   > 第一步是用`git add`把文件添加进去，实际上就是把文件修改添加到暂存区；
   >
   > 第二步是用`git commit`提交更改，实际上就是把暂存区的所有内容提交到当前分支。
   >
   > 因为我们创建Git版本库时，Git自动为我们创建了唯一一个`master`分支，所以，现在，`git commit`就是往`master`分支上提交更改。
   >
   > 你可以简单理解为，需要提交的文件修改通通放到暂存区，然后，一次性提交暂存区的所有修改。

------



### 管理修改

1. 用`git diff HEAD -- readme.txt`命令可以查看工作区和版本库里面最新版本的区别：

   ```
   $ git diff HEAD -- readme.txt 
   diff --git a/readme.txt b/readme.txt
   index 76d770f..a9c5755 100644
   --- a/readme.txt
   +++ b/readme.txt
   @@ -1,4 +1,4 @@
    Git is a distributed version control system.
    Git is free software distributed under the GPL.
    Git has a mutable index called stage.
   -Git tracks changes.
   +Git tracks changes of files.
   ```

------

### 撤销修改

`git checkout -- file`可以丢弃工作区的修改：

> 命令`git checkout -- readme.txt`意思就是，把`readme.txt`文件在工作区的修改全部撤销，这里有两种情况：
>
> 一种是`readme.txt`自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
>
> 一种是`readme.txt`已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。
>
> 总之，就是让这个文件回到最近一次`git commit`或`git add`时的状态。==上面两种是同一个意思==

`git checkout -- file`命令中的`--`很重要，没有`--`，就变成了“切换到另一个分支”的命令，我们在后面的分支管理中会再次遇到`git checkout`命令



1.修改文件后已add到暂存区，或未add到暂存区。用命令`git checkout -- readme.txt`撤销

2.修改文件后add、未commit到版本库

```
用命令git reset HEAD -- <file>可以把暂存区的修改撤销掉（unstage），重新放回工作区：
再用$ git checkout -- readme.txt把工作区的需改丢弃
```

又到了小结时间。

场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令`git checkout -- file`。

场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令`git reset HEAD <file>`，就回到了场景1，第二步按场景1操作。==场景2错误：git reset HEAD -- <file>从暂存区放到工作区，没问题，但再执行$ git checkout -- readme.txt把工作区的需改丢弃，不起作用==，因为暂存区没有了，所以无法checkout,checkout是比对暂存库的

场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考[版本回退](https://www.liaoxuefeng.com/wiki/896043488029600/897013573512192)一节，不过前提是没有推送到远程库。





### 删除文件文件已commit

1. 通常直接在文件管理器中把没用的文件删了，或者用`rm`命令删了：

```
$ rm test.txt  //注意不带git
```

2. 现在你有两个选择，一是确实要从版本库中删除该文件，那就用命令`git rm`删掉，并且`git commit`：

   ```
   $ git rm test.txt
   rm 'test.txt'
   
   $ git commit -m "remove test.txt"
   [master d46f35e] remove test.txt
    1 file changed, 1 deletion(-)
    delete mode 100644 test.txt
   ```

3. 另一种情况是删错了，因为版本库里还有呢，所以可以很轻松地把误删的文件恢复到最新版本：

   ```
   $ git checkout -- test.txt  //git checkout其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。  注意：从来没有被添加到版本库就被删除的文件，是无法恢复的！
   ```

   ```
   $ git restore 1.txt  //这也能恢复
   ```

4. git rm --cached <file>仅仅删除暂存区的文件







原来的git checkout 可以使用 git restore 代替

原来的git reset HEAD 可以使用 git restore --staged 代替

最新版的git提示都已经更换成了restore

# 第3次经验

$ git restore --staged 2.txt   从暂存区退回到工作区

$ git restore 2.txt                  撤销工作区的修改





## 远程仓库

1. 第1步：创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有`id_rsa`和`id_rsa.pub`这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key：

   ```
   $ ssh-keygen -t rsa -C "youremail@example.com"
   ```

   > 你需要把邮件地址换成你自己的邮件地址，然后一路回车，使用默认值即可，由于这个Key也不是用于军事目的，所以也无需设置密码。
   >
   > 如果一切顺利的话，可以在用户主目录里找到`.ssh`目录，里面有`id_rsa`和`id_rsa.pub`两个文件，这两个就是SSH Key的秘钥对，`id_rsa`是私钥，不能泄露出去，`id_rsa.pub`是公钥，可以放心地告诉任何人。

2. 第2步：登陆GitHub，打开“Account settings”，“SSH Keys”页面：添加后试了几次，最后成功了

`id_rsa.pub`文件内容如下

```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDcYF+2ZZ0jGrviMeUrpoi0j+KHa0zUqZKOma/HK7fldVA64WOVBlXLMe5zHsfZEfeXvHubMHLBrXfWwg365NBUnsxHIPjkW8cGyViOHSXziC1MrlKtDRL4HPiNlj5xBCRcQjN9xYVxr18GTlXVsDROE+kIJ8WL2MzwQnYa/WYtILe6UQVCfEMcw/PDC3czUeicUqKDBOKgCxdull28bUaTBp5hHkQ/cTGy6tmzCYDIj8AKWzr22cvKeDaUFeHo3g7/fWbmgV3WvevKPy1qodxrm3uejuZHtb0+m6gP2AGb+X5ePUG1wvOBjOAAc4x+HHCmFAh8AZVfIWCq0Fp9o78FrVUDwKGp4O5CD0MrMpj2Xa4bFslX+zGhaqG/yhXt8USwMKWTDF4dJlnIVsdT4byIbozFGyMs79VyrQvjGqRMYg03vAa/Uy/4lRP2AR3H4d6aMFHPWJjcJeCRIwnEpXi7O24AUW5T8Ksf1Jbt35uLqeihSoCEdlSFe8KzjFTIbCM= muhuali29@163.com

```

查看是否连接成功：ssh -T git@github.com

> wbb@DESKTOP-UUURTBR MINGW64 ~/Desktop
> $ ssh -T git@github.com
>
> git@github.com: Permission denied (publickey).
>
> wbb@DESKTOP-UUURTBR MINGW64 ~/Desktop
> $
>
> wbb@DESKTOP-UUURTBR MINGW64 ~/Desktop
> $ ssh -T git@github.com
> ssh: connect to host github.com port 22: Connection refused
>
> wbb@DESKTOP-UUURTBR MINGW64 ~/Desktop
> $ ssh -T git@github.com
> ssh: connect to host github.com port 22: Connection refused
>
> wbb@DESKTOP-UUURTBR MINGW64 ~/Desktop
> $ ssh -T git@github.com
> Hi muhuali29! You've successfully authenticated, but GitHub does not provide shell access.







## 码云

#### 简易的命令行入门教程:

Git 全局设置:

```
git config --global user.name "王彬镔"
git config --global user.email "8089133+muhuali29@user.noreply.gitee.com"
```

创建 git 仓库:

```
mkdir wbb
cd wbb
git init
touch README.md
git add README.md
git commit -m "first commit"
git remote add origin https://gitee.com/muhuali29/wbb.git
git push -u origin master
```

已有仓库? https://gitee.com/muhuali29/wbb.git

```
cd existing_git_repo
git remote add origin https://gitee.com/muhuali29/wbb.git
git push -u origin master
```

###  自己经验

1. 在码云上创建仓库后$ git clone git@gitee.com:muhuali29/wbb.git  克隆仓库，使本地与远程仓库保持同步

2. 我们用`git remote -v`查看远程库信息，可以看到两个远程库

3. 先删除已关联的名为`origin`的远程库：git remote rm origin

4. 添加关联远程库git remote add origin https://gitee.com/muhuali29/wbb.git  或 git remote add origin git@gitee.com:muhuali29/wbb2.git

5. git@gitee.com:muhuali29/wbb2.git

6. 第一次git push -u origin master 会出错，改成git push -f origin master

7. $ git pull origin master  从远程库拉取

8. ```
   git remote rm origin 删除远程仓库的关联
   ```

### 自己经验2

1. 添加到暂存区git add 文件名或   git add .

2. 暂存区添加到版本库git commit -m  "说明"

3. 撤销工作区的修改，回到暂存区里的内容

4. **git rm --cached <file>** 命令时，会直接从暂存区删除文件，工作区则不做出改变。

5. 当执行 **git checkout .** 或者 **git checkout -- <file>** 命令时，会用暂存区全部或指定的文件替换工作区的文件。这个操作很危险，会清除工作区中未添加到暂存区的改动。

6. 当执行 **git checkout HEAD .** 或者 **git checkout HEAD <file>** 命令时，会用 HEAD 指向的 master 分支中的全部或者部分文件替换暂存区和以及工作区中的文件。这个命令也是极具危险性的，因为不但会清除工作区中未提交的改动，也会清除暂存区中未提交的改动。

7. 从暂存区删除后，在从版本起退回git restore --staged 1.txt，此时工作区的内容不变。如果工作区和暂存区代码内容不一致用git checkout -- <file>  或--省略。注意与第6条的区别。

8. 版本库里的修改可任意回退，参照上面的版本回退。

   

## 自己经验3

1. git add 1.txt 到暂存区后，git rm --cached 1.txt,从暂存区删除。删除的前提是工作区没有修改过。

2. 如果1.txt在工作区修改了，要撤销修改用git restore 1.txt，取消修改，回到和暂存区一样的内容。

   ------

3. commit 提交后，rm 1.txt文件后或右击删除了文件，执行git restore 1.txt可恢复文件到工作区

4. 再执行git rm 1.txt就把暂存区里也删除了，可执行git restore --staged <file>..." to unstage，版本库里还在；git restore --staged 1.txt是git rm 1.txt的反操作





## 自己经验4

1. 如果删除了或修改了文件，可用git restore 1.txt可恢复文件到工作区
2. rm 1.txt删除工作区文件，在执行git rm 1.txt删除暂存区文件，再git commit。就把文件从工作区和暂存区都删除了。但版本库中还存在。
3. 针对上面第二种情况，从版本库中恢复；git reset --hard 'commitid'
4. 如果rm 1.txt删除工作区文件，在执行git rm 1.txt删除暂存区文件，没有commit。用git restore --staged  1.txt恢复。git restore --staged  1.txt与git rm 1.txt是反操作
5. git restore --staged 1.txt与git rm --cached 1.txt是反操作
6. git rm 1.txt与git rm --cached 1.txt的区别。





## 自己经验5

1. 工作区修改了文件或者新增了文件，git status后以红色字体表示。

![image-20210525204129209](E:\笔记经验\imageMd\image-20210525204129209.png)

2. git restore 1.txt可撤销modified :1.txt的修改。

3. git add . 后执行git status，颜色变绿表明都在暂存区了。

   

![image-20210525204435128](E:\笔记经验\imageMd\image-20210525204435128.png)

4. 此时执行 git restore --staged 1.txt,从暂存区退到工作区。

5. 如果第3步后又修改了1.txt，显示状态如下：此时执行git restore 1.txt，就撤销了工作区1.txt的修改。

   ![image-20210525205059216](E:\笔记经验\imageMd\image-20210525205059216.png)

6. git commit -m  "说明"，提交后用git log显示。用git log --pretty=oneline美化显示

   ![image-20210525205834485](E:\笔记经验\imageMd\image-20210525205834485.png)

7. git reset --hard 17ac55,直接使工作区回到17ac555那时候的状态

8. 暂存区文件commit后，暂存区是不是没有了？

9. rm  1.txt  在 git rm  1.txt后，再commit 就彻底删除了

   

![image-20210525211342948](E:\笔记经验\imageMd\image-20210525211342948.png)

10. 如果再上图执行git restore --staged 1.txt就回到git rm 1.txt的状态，即绿色字体变成了红色。
11. 变成红色之后执行 git restore 1.txt,即又把他放到了工作区。
12. git restore 1.txt是rm 1.txt的后悔药；git restore --staged 1.txt是git rm 1.txt的后悔药。
13. git rm 1.txt与git rm --cached 1.txt的区别。git rm --cached 1.txt执行后工作区文件还存在；git rm 1.txt后工作区就不存在了。
14. git reset --hard "commitid"会情况暂存区，使工作区回到提交时的状态。