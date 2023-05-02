## git学习

### 1.安装

 官网下载，无脑点击下一步即可

  git gui  : 图形界面的git，不建议初学者使用

  git bash : 使用风格与Linux相似

  git cmd : Windows风格的命令

### 2.git环境配置

设置用户名与密码： git config --global user.name "***"

​                                    git config --global user.email "***@qq.com"

### 3.基本理论

1）工作区域 ： 工作目录（Working Directory）、暂存区（Stage / Index）、资源库（Repository / Git Directory) 、

​                             远程git仓库（Remote Directory）

> 前三个是本地工作区域，第四个是远程工作区域
>
> > 工作区存放项目代码、暂存区临时存放改动、仓库区有提交的所有版本的数据，其中HEAD指向最新放入仓库的版本

----

2）          Working Directory   ----git add files---->   Stage / Index

​                          Stage / Index  ----git commit---->   Repository / Git Directory

​     Repository / Git Directory  ----  git push  ---->    Remote Directory

---

​                Remote Directory  ----- git pull----> Repository / Git Directory 

​    Repository / Git Directory ---- git reset----->   Stage / Index 

​                      Stage / Index   ---- git checkout---->  Working Directory 

----

### 4.项目搭建

1）本地搭建仓库 ：   git init       设置当前目录为git托管

2） 远程克隆仓库  ：    git clone 地址       ------>          克隆远程仓库

### 5.文件状态

1）文件的四种状态

+ Untracked : 未跟踪，此文件在文件夹中, 但并没有加入到git库, 不参与版本控制. 通过git add 状态变为Staged.
+ Unmodify: 文件已经入库, 未修改, 即版本库中的文件快照内容与文件夹中完全一致. 这种类型的文件有两种去处, 如果它被修改, 而变为Modified. 如果使用git rm移出版本库, 则成为Untracked文件
+ Modified: 文件已修改, 仅仅是修改, 并没有进行其他的操作. 这个文件也有两个去处, 通过git add可进入暂存staged状态, 使用git checkout 则丢弃修改过, 返回到unmodify状态, 这个git checkout即从库中取出文件, 覆盖当前修改 !
+ Staged: 暂存状态. 执行git commit则将修改同步到库中, 这时库中的文件和本地文件又变为一致, 文件为Unmodify状态. 执行git reset HEAD filename取消暂存, 文件状态为Modified

2）查看文件状态

``git status [filename] ``  :   查看指定文件状态

``git status``  :  查看所有文件状态

``git add .``    :   添加所有文件到暂存区

``git commit -m “消息内容”``  :   添加暂存区的文件到本地仓库

### 6.命令

#### 基础命令

1. cd     改变目录

   > 以在桌面为例， cd test -------进入桌面上的test目录

2. cd ..    返回上一级目录

3. pwd      显示当前所在的目录路径

4. clear      清屏

5. ls      列出当前目录的所有文件

   > 白色的是文件  绿色的是程序   蓝色的是目录

6. touch    在当前目录下新建文件

7. rm    删除当前目录下的文件

8. mkdir    在当前目录下新建目录

9. rm -r     删除当前目录下的子目录

10. mv      移动文件

    > 若aaa为文件，test为一个目录（aaa文件与test文件夹在同一目录下）
    >
    > mv aaa test  表示将aaa文件移入test目录中去

11. history    查看使用过的命令

12. help     帮助

13. exit     退出

#### git命令

1. git  add

   > 后跟文件名（文件需在git托管的目录或子目录内），将文件放入暂存区

2. git commit -m "说明内容"

   > 添加暂存区的所有文件到本地仓库，说明内容用来标识每一次的修改

3. git log

   > 查看版本号低于当前版本的所有版本

4. git reflog

   > 查看所有版本以及对版本的操作记录

5. cat 

   > 后跟文件名，查看文件内容

6. git reset --hard 

   > 读档操作
   >
   > > 后跟HEAD^为回退一版本， 后跟HEAD^^为回退两版本，后跟HEAD~100为回退100版本
   > >
   > > 后跟版本号可实现前进版本

7. git checkout --

   > 后跟文件名，可实现撤销对文件的修改
   >
   > > 若文件修改了但未用add提交到缓存区，则可用该语句直接撤销文件的修改
   > >
   > > 若文件已经提交到缓存区，需先用 ==git reset HEAD 文件名==把暂存区的修改回退到工作区，再用该语句

8. git rm 

   > 后跟文件名，实现删除文件
   >
   > > 用法与git add相同，git rm实现删除文件，并将删除操作写入暂存区，再用git commit提交修改，至此，删除完成
   > >
   > > git rm 与 rm 不同，rm执行删除操作，但是未将删除操作写入暂存区
   > >
   > > > git rm删除的（未commit）文件，若要恢复，先git reset HEAD ，再用git checkout -- （同第7条撤销修改操作）
   > > >
   > > > rm删除的文件，若要恢复，直接用git checkout --

9. git branch

   > 单独使用，查看当前分支情况
   >
   > 后跟分支名，创建新分支
   >
   > 后跟  -d 表示删除分支，后跟 -D 表示强行删除（为合并的分支要删除只能强行删除）
   >
   > > git branch dev    创建dev分支
   > >
   > > gitbranch -d dev  删除dev分支

10. git checkout

    > 后跟分支名，切换分支，==不推荐此方法==
    >
    > > git checkout -b dev    等价于  git branch dev  +  git checkout dev

11. git switch

    > 用于切换分支，==推荐使用此方法==
    >
    > git switch  dev
    >
    > git switch -c dev 创建dev分支并

12. git merge

    > 后跟分支名，将指定分支合并到当前分支下

13. git stash

    > 储藏当前工作现场
    >
    > > git stash list  查看当前储藏的所有工作现场

14. git stash pop 与 git stash apply

    > 恢复储藏的工作现场
    >
    > > pop 恢复之后即清楚stash list内容，apply不清理，apply需配合 git stash drop使用
    > >
    > > 当list中只有一条记录时，直接使用上述命令即可，当有多条时，需指明恢复哪一条

15. git cherry-pick 

    > 后跟commit编号，可以复制提交到当前分支

16. git tag

    > 查看所有标签，后跟标签名用于新建标签，标签与commit相连
    >
    > > git tag v1.0   在当前分支的最新提交创建标签 v1.0
    > >
    > > git tag v1.0 f52c633  在指定id的commit下创建标签
    > >
    > > git tag -a v1.0 -m "说明文字" f52c633  创建带说明文字的标签
    > >
    > > > git tag -d 标签名：删除本地标签

17. git show

    > 后跟标签名，可查看标签相关信息

### 7.远程仓库

#### 连接远程仓库

1. ssh-keygen -t rsa -C "yangxz18@outlook.com"命令创建SSH密钥

2. 在主目录（C:\Users\Zhao\）生成 .SSH目录，里面有id_rsa和id_rsa.pub两个文件，id_rsa是私钥，id_rsa.pub是公钥

3. github添加SSH　Key（公钥）

   > 为什么GitHub需要SSH Key：GitHub需要识别出你推送的提交确实是你推送的，而不是别人，而Git支持SSH协议，所以，GitHub只要知道了公钥，就可以确认只有你自己才能推送。GitHub允许添加多个Key。假定有若干电脑，一会儿在公司提交，一会儿在家里提交，只要把每台电脑的Key都添加到GitHub，就可以在每台电脑上往GitHub推送

4. git remote add origin git@github.com:yangxiaozhao/testforzhao.git  命令创建github远程库 origin为远程库默认名字(可指定其他名字)

5. git remote rm origin 命令删除远程库

#### 与远程仓库交互

1. git push origin master ：推送master分支最新提交到远程库（第一次推送用git push -u origin master）

2. git push origin 标签名 ： 推送指定标签到远程

   git push origin --tags ：推送所有未推送过的本地标签

   git push origin :refs/tags/标签名：删除远程标签

3. git clone git@github.com:yangxiaozhao/testtwo.git 将github中yangxiaozhao的testtwo仓库内容克隆到本地仓库

### 8.分支

> 初始一条主分支：master
>
> HEAD指向当前分支（初始：master），master指向最新的提交
>
> > 即，HEAD确定当前分支，当前分支名确定提交对象

1. master指向最新提交，每次提交，master分支向前移动
2. 创建新分支时（分支名为dev），产生新指针的v，指向当前master相同的提交（即当前的最新提交），此时若将HEAD指向dev则表示当前分支在dev上，此后有新的提交，dev指针向前移动，master不变
3. 当dev的工作完成，将dev与master合并，则master指向dev的当前提交