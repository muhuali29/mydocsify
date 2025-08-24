# git笔记

## 情况一文件修改后，且add到暂存区，想回退

1. git  reset HEAD 文件名   //退回到工作区
2. git checkout 文件名    //撤销修改

## 情况二文件修改后没有add到暂存区

1. git checkout 文件名   //就行



# 删除文件

1. 文件夹里右键删除文件，没add，没commit  

   ```
   git checkout -- 文件名
   git restore 文件名
   这两句都可以
   ```

   