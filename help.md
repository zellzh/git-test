# GIT教程

## ·库关系图
![库关系图](https://static.oschina.net/uploads/space/2017/1214/113901_cUBI_3375733.png)
### 1.创建工作区（本地库）

    什么是工作区（本地库）？
    可以理解成当前文件夹目录的所有文件都可以被GIT管理类起来，GIT可以对文件修改和还原。
首先，选个你想当工作区(本地库)的文件夹，通过命令$ git init 把这个文件夹变成GIT能管理的工作区（本地库）。

如果在当前文件夹多了个文件名为.git的隐藏文件夹，则说明创建成功了。

现在可以尝试创建一个a.txt的文本文件来作为第一个练习。

### 2.将文件发送至版本库

 

- 第一步，用命令$ git add a.txt 将文件添加至暂存区，说明都没提示则说明成功。

- 第二步，用命令$ git commit -m "上传说明" 将文件从暂存区添加到版本库。提示 1 file changed... 则说明成功。

- 注：因为commit可以添加很多文件，所以可以一次性add多个文件后再commit。

### 3.文件版本的还原和修改

- 版本的还原
    - 通过命令$ git status 可以查看库的当前状态，文件是否被修改和当前文件夹的文件的上传状态。

    - 通过命令$ git diff 文件名 可以查看该文件的修改情况。确认新修改后，通过步骤2.可以再次将修改后的文件上传到库。

    - 所有commit中的"上传说明"有重要的作用，提示当时的上传需求。因为commit也是上传文件时的存盘，通过命令$ git log （--pretty=oneline）可以查看历史的上传记录。（$ git log --pretty=oneline 可以仅查看版本号和上传说明）必要时就可以通过commit存盘的版本号和说明来回退文件版本。

    - 通过命令$ git reset --hard HEAD^ 可以将文件回退到上一次修改状态。HEAD 表示当前版本，^的个数表示回退多少个版本，可以写成HEAD~n.

    - 通过命令$ git reset --hard 版本号 可以指定文件到该版本号的状态。而版本号可以通过命令$ git reflog 来查询之前的操作。

- 文件的修改的撤销
    - 情况1：当你改错了当前文件的内容时，想直接放弃修改时。用命令$ git checkout -- 该文件名 (例如：$ git checkout -- a.txt) 就可以回到上个版本的状态。
    - 情况2：当你不但改错了当前文件的内容时，还添加到了暂存区，想放弃修改时：用命令$ git reset HEAD a.txt ，回到情况1，然后按情况1操作。
    - 情况3：已经提交了错误的修改到版本库时，想要放弃这次修改时。就要用到版本回退命令$ git reser --hard HEAD^ 来操作。前提是还未上传到远程服务器github上。
- 文件修改的删除
    
     当文件上传到版本库后，如果你把该文件给删除了。
     - 情况1：确实没用的话可以通过命令$ git rm <file> 来将改文件从库中也删除掉，然后再$ git commit 。
     - 情况2：删错了，可以通过命令$ git checkout -- <file> 来把误删的文件从版本库中恢复到工作区。

### 4.远程仓库Github

- 注册github账号后，通过命令 $ ssh-keygen -t rsa -C "youremail@example.com" 来创建属于你github账号的SSH KEY。输入指令后，在电脑用户主目录找到.ssh文件夹。里面有id_rsa和id_rsa.pub两个文件，

- 登录github，找到设置中的SSH and GPG keys项，点击New SSH key，将id_rsa.pub文件中的密匙复制到key中后点击Add Key按钮即可。**添加SSH key后的第一次传输文件git出现的提示输入yes即可。**

- 在github中点new repository创建一个新的库。根据提示在git中输入相应的命令完成版本库master和远程库master的关联。之后通过命令$ git push origin master 就能将版本库数据传给github了。
 
 - 多人开发时可以通过命令$ git clone git@github.com:yourgithub.git 来克隆一个本地库进行合作开发。