# 基本概念

## **正确理解Git四个工作区域**

**Workspace**：工作区，即个人克隆项目到本地后,项目所在的文件夹目录

**Index / Stage**：暂存区，用于储存工作区中的变更(增删改等改动)的文件的地方.操作时使用git add会将本地所有的变更提交到暂存区中

**Repository**：仓库区（或版本库），用于储存工作区和暂存区中提交上来的文件,使用git commit -m '提交内容的描述'，这里面有你提交到所有版本的数据，其中HEAD指向最新放入仓库的版本

**Remote**：远程仓库，当进行到这里的时候即一个人的开发完毕的时,需要将自己开发的功能合并到主项目中去,但因为是多人开发,要保管好主项目中存储的代码和文件的话,就需要放在搭建好的远程git仓库中,即远程仓库。具体操作:git push origin 远程分支名即可。

git管理的文件有三种状态：已修改（modified）,已暂存（staged）,已提交(committed)

## 新建仓库

```bash
# 1.建立远程库(远程库最好为空)

# 2.本地新建文件夹(最好与远程仓库同名的文件夹)
mkdir testgit
cd testgit

# 3.初始化仓库,当前目录下多了一个.git的目录，这个目录是Git来跟踪管理版本库的
git init  

# 注：上面两步可合并
# 新建一个目录，将其初始化为Git代码库
# git init [project-name] 

# 关联远程库
# git remote add origin(默认origin，可修改) branch_Name(为空时默认为master) url
# 感觉origin理解为远程仓库在本地的标签或者别名，便于使用罢了
git remote add origin https://github.com/1783247180/git-test.git
# 两个地方的仓库名不需要相同，因为通过在本地仓库目录下执行这条
# 命令（命令中包含远程库的名字）已经将两者建立了联系

# 新增文件
touch README.md

# 添加文件到暂存区
git add .

# 提交文件到本地库
git commit -m "msg(提交日志)"

# 注：上面两步可合并（git commit -am "msg"）

# 把本地库的所有内容推送到远程库上
git push -u origin master 
# 加上了-u参数(推送和关联)，Git不但会把本地的master分支内容推送到远程新的master分支，
# 还会把本地的master分支和远程的master分支关联起来
# 以后即可直接用git push代替git push origin master
```

## 克隆远程仓库

```bash
git clone https://github.com/1783247180/git-test.git
```

## 常用查看命令

```bash
# 查看仓库当前的状态
git status 
# 查看历史提交信息
git log
```

**比较文件不同-diff**

```bash
# 查看对文件做什么修改，比较工作区和暂存区
git diff 文件名
# 看两个版本的差异的文件列表（版本号是git log查出来的,前7为就可以了）
git diff 版本号1 版本号2 --stat
# git diff bf326a16 276b4a14 --stat
# docs/v2.8.76/README.md            | 10 ----------
# docs/v2.8.76/mysql_ddl.sql        |  6 ------
# 2 files changed, 16 deletions(-)
```

## 常用修改命令

```bash
# 添加，但是不提交（必须要有readme.txt）
git add readme.txt

# 提交，只有add后提交才有效。
# “改文件->add文件->再改->提交”，则第二次修改无效,不会被提交，只会成功提交第一次的修改。
git commit -m "提交描述"
```

## 撤销修改和版本回退

```bash
# 本地回退
# 回退到具体commit id
# hard与soft的区别 hard重置会修改Workspace，而soft重置不会修改Workspace
git reset --soft 0b3a6dbf02c8d03969577cb7fe0e200cf8303c63
git reset --hard 0b3a6dbf02c8d03969577cb7fe0e200cf8303c63
################################
# 远程回退
git push [remote] [banch] --force
```

## 拉取

```bash
# pull将代码直接合并，造成冲突等无法知道
git pull orgin master
# git fetch + git merge == git pull
```



## 远程库操作-remote

```bash
# 删除该远程库
git remote remove 远程库名 
# 例：git remote remove origin(一般都是叫origin)

# 添加另外远程库
git remote add 远程库名 远程库地址
# 例：git remote add origion https://...

# 改变远程库的名字
git remote rename 旧名称 新名称（）
# 例：git rename origin origin1(把origin改成origin1)

# 查看远程库的信息
git remote 

# 查看远程库的信息地址，显示更为详细的信息，显示对应的克隆地址
git remote -v

# 更改remote地址
git remote set-url origin git@github.com:username/repository-name.git
```

## git分支

```bash
## 创建新分支，创建新分支时会把master分支的文件复制一份到新分支
git branch [branchName]

## 创建并切换到新分支
git checkout -b [branchName]

## 切换到新分支
git checkout [branchName]

# 更新远程分支列表
git remote update origin --prune

# 查看所有分支
git branch -a

# 删除远程分支
git push origin --delete [branchName]

# 删除本地分支 
git branch -d  [branchName]

#提交新分支到远程
git push origin master
```

# IDEA集成Git

## 分享项目到GitHub上

在菜单上选择VCS，在下拉列表中选择Import into Version Control，再选择Share project on Github

![img](git-hand\20170815220857133.pnghand)

输入仓库的描述信息，点击Share

![img](https://raw.githubusercontent.com/1783247180/Markdown4Zhihu/master/Data/git-hand/20170815220909941.png)

选择要提交的文件，忽略不需要提交的文件，填写注释，点击OK

![img](https://raw.githubusercontent.com/1783247180/Markdown4Zhihu/master/Data/git-hand/20170815220920421.png)

勾选，不添加vcs.xml，选择No

![img](https://raw.githubusercontent.com/1783247180/Markdown4Zhihu/master/Data/git-hand/20170815220929381.png)

## git基本操作

![GitHub提交代码图](https://raw.githubusercontent.com/1783247180/Markdown4Zhihu/master/Data/git-hand/20170928081608018.png)

### 提交代码到本地

![image-20200713194347379](https://raw.githubusercontent.com/1783247180/Markdown4Zhihu/master/Data/git-hand/image-20200713194347379.png)

### 将提交的代码push到远程GitHub

把代码提交到了本地Git仓库中，最后将提交的代码push到远程仓库，这样本地代码提交到远程就完成了。
项目上右键——>Git——>Repository——>push(将本地代码push到远程)，这样远程的代码就和本地同步了。有时候在push的时候会失败，原因之一是本地代码与远程代码不同步，所以在push之前，要在本地将远程代码pull一下：项目上右键——>Git——>Repository——>pull(将远程代码pull到本地)。如图：
![pushAndPull](https://raw.githubusercontent.com/1783247180/Markdown4Zhihu/master/Data/git-hand/20170928095349761.png)

| 1    | 2     | 3    |

| ---- | ----- | ---- |

| 4    | 5     | 6    |

| 12   | 12312 | 323  |

| 1    |       | 23   |


