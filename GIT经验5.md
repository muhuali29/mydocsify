# GIT经验5

1. 查看系统配置 git config --global --list

2. 查看用户配置 git config --system --list

3. 版本回退用git reset --hard commit_id，针对已commit的文件，是否把工作区和暂存区都覆盖了，带验证

4. $ git restore --staged 2.txt   从暂存区退回到工作区；同$ git checkout -- test.txt待验证

5. $ git restore 2.txt                  撤销工作区的修改同$ git chechout 1.txt  //这也能恢复

6. git rm --cached <file>仅仅删除暂存区的文件
7. 提交后，用`git diff HEAD -- readme.txt`命令可以查看工作区和版本库里面最新版本的区别：



## git push到远程仓库

1. 第1步：创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有`id_rsa`和`id_rsa.pub`这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key：

   ```
   $ ssh-keygen -t rsa -C "youremail@example.com"
   ```

   > 你需要把邮件地址换成你自己的邮件地址，然后一路回车，使用默认值即可，由于这个Key也不是用于军事目的，所以也无需设置密码。
   >
   > 如果一切顺利的话，可以在用户主目录里找到`.ssh`目录，里面有`id_rsa`和`id_rsa.pub`两个文件，这两个就是SSH Key的秘钥对，`id_rsa`是私钥，不能泄露出去，`id_rsa.pub`是公钥，可以放心地告诉任何人。

2. 第2步：登陆GitHub，打开“Account settings”，“SSH Keys”页面：填入公钥ssh

3. 安装完成后，输入设置用户名和邮箱；查看系统配置 git config --global --list

   ```
   $ git config --global user.name "Your Name"
   $ git config --global user.email "email@example.com"
   ```

   > 因为Git是分布式版本控制系统，所以，每个机器都必须自报家门：你的名字和Email地址。你也许会担心，如果有人故意冒充别人怎么办？这个不必担心，首先我们相信大家都是善良无知的群众，其次，真的有冒充的也是有办法可查的。
   >
   > 注意`git config`命令的`--global`参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址。

4. 链接到远程仓库$ git remote add origin https://gitee.com/muhuali29/wbb.git   https://github.com/muhuali29/wbb.git

5. 方式一，①本地新建仓库git init，本地库保持没有文件commit。②git pull origin master，前提是远程仓库要有文件③本地仓库提交到远程仓库git push -u origin master。

6. 直接克隆远程仓库到本地git clone 远程地址

7. git remote -v 查看远程仓库



tips：git pull origin master提示fatal: refusing to merge unrelated histories

> 	出现这个问题的最主要原因还是在于本地仓库和远程仓库实际上是独立的两个仓库。假如我之前是直接clone的方式在本地建立起远程github仓库的克隆本地仓库就不会有这问题了。
>
> 查阅了一下资料，发现可以在pull命令后紧接着使用--allow-unrelated-history选项来解决问题（该选项可以合并两个独立启动仓库的历史）。
> ————————————————
> 版权声明：本文为CSDN博主「铁乐与猫」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
> 原文链接：https://blog.csdn.net/u012145252/article/details/80628451

解决方法：$git pull origin master --allow-unrelated-histories