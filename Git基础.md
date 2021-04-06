# Markdown基本语法

## 无序列表

>+ nihao
   >>+ dfjkd
   >>+ fdkdj
>+ jkdjkf

## 有序列表

1. 发货的介绍客户发
2. 数据库搭建


*斜体*
**加粗**
_斜体_

~~删除线~~
***斜体加粗***

## 分割推荐使用最先出现的，***、---、----或者****或者更多连续数目3以上的-或者*均表示分割线，尽量不要混用

****

***

---

-----

## 代码块引用

~~~ python
import sys 
sys.stdout.write("nihao")
~~~


![tupain](https://img2018.cnblogs.com/blog/1623101/201909/1623101-20190927102821851-961438687.png "yizhangtupian" )

# GIT基本操作手册

## 基础命令学习

* git init 
   * 初始化一个仓库，生成一个.git文件夹
* git add
   * 添加一个文件到提交区，此时还可以取消操作，添加之后，只显示修改的项目，但是不能显示具体的差异
* git commit (-m "表明修改原因")
   * 使用该语句则直接提交了文件，修改完成，即现在的文本为标准版本
* git status 
   * 查看这个仓库的当前状态，显示修改的文件项目
* git diff
   * 显示当前文件与标准版本的差异，即具体的修改内容，但是如果使用了add和commit操作则无法显示了
* git reset
   * 取消add的文件
* git reset --hard HEAD^(一个^代表向前一个节点的版本)
   * 回退版本
* git log
  * 查看提交历史，查找退回到哪个版本
* git reflog 
  * 查看顺序版本切换记录（可以看到commit-ID），回到未来版本，使用
    > git reset --hard \<commit-ID>
* git checkout --\<filename>
  * 回退到最近一次git add和git commit的时候的状态
* git reset HEAD \<filename>
  * 已经git add之后想要放弃修改可以使用该命令
* git rm \<filename>
  * 在版本库中删除一个文件，如果删错了可以使用
    > git checkout --\<filename>
    
    恢复

* git push <远程主机名> [<本地分支名>] :[<远程分支名>]
  * 如果省略远程分支名则默认新建一个分支，除非存在追踪关系（名字相同？）
  * 如果只有一个远程分支，则可以省略远程主机名
  * 如果省略本地分支名，则表示将一个空推送到远程，即删除该远程分支
  * 使用git branch -r 可以查看远程分支
  * 可以使用https://来代替git@（文件名称是需要去掉git）
* git branch <分支名>
  * 创建一个新的分支
  * 如果省略分支名则解释为查看所有分支
* git switch [-c] <分支名>
  * 切换到某分支
  * -c不缺省时表示创建切换分支
* git checkout [-b] <分支名> 
  * 缺省-b切换分支
  * -b存在时则表示切换创建一个分支
* git merge <分支名>
  * 合并某分支到当前分支

<del>
* 克隆远程仓库到本地，通常只能克隆一个分支
  * 可以使两个相关联，自动更新到本地（两个名字需要相同可能）
    > <del>git branch \<name> origin/ \<name></del>
  * 也可以使用（branch_name就是指定的分支名称）
    > git clone -c \<branch_name> https://github.com/Forxci/Hello 
  
  这样克隆下来的就是指定的分支了

</del>

* 克隆远程分支到本地，默认为master分支

1. 将远程分支的master分支克隆到本地并且重命名(git clone 默认克隆master分支)
    > git clone -b <分支名> <远程主机名及目录> 

2. 若要克隆远程分支，则使用如下命令：

    > git checkout -b <分支名a> <远程主机名/分支名a>

* 使用这个命令将本地分支main同步到github的forPracticeGit项目下的main分支
  
    > git push https://github.com/Forxci/forPracticeGit main:main

* 使用git pull将远程分支直接合并到本地分支

  > git pull <远程主机名及目录> <分支名> <分支名>

* git fetch 是将内容拉取到本地，但是并不进行添加和合并，需要人工操作进行
  
* 当存在冲突时，git不能进行直接合并，两个分支上的修改冲突之处都会标识在文本内，因此可以也必须手动去修改保存后在提交，最后删除不需要的分支即可，使用
    > git log --graph

  可以查看合并流程图


<hr/>
<i>注：master表示当前分支，orgin指代远程主机主目录</i>

