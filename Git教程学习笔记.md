
## 1. Git 命令汇总

### 1.1 自报家门

- git config --global user.name "Your Name"
- git config --global user.email "email@example.com"

### 1.2 时光穿梭

- git init：初始化一个 Git 仓库
- git add <file\>，git commit -m <message\>：两步添加文件到 Git 仓库
- git status：查看工作区当前状态（文件是否被修改过）
- git diff：查看修改内容
- git log：查看提交历史，以便确定要回退到哪个版本
- git reflog：查看命令历史，以便确定要回到未来的哪个版本
- git reset --hard commit_id：在版本的历史之间穿梭
- git diff HEAD -- <file\>：查看工作区 file 和版本库里面最新版本的区别
- git checkout -- <file\>：用版本库里的版本替换工作区的版本，“一键还原”工作区的修改或删除
- git reset HEAD <file\>：把暂存区的修改撤销掉（unstage），重新放回工作区
- git rm <file\>，git commit -m <message\>：从版本库中删除该文件

### 1.3 远程仓库

- ssh-keygen -t rsa -C "youremail@example.com"：创建 SSH Key
- git remote add origin https://github.com/michaelliao/learngit.git ：本地库关联远程库
- git clone git@github.com:<username\>/< subject name\>.git：克隆远程库到本地
- git push -u origin master：第一次推送 master 分支的所有内容
- git push origin master：第一次推送以后，每次本地提交后，可以使用此命令推送最新修改

### 1.4 分支管理

- git branch：查看当前分支，当前分支前面会标一个*号
- git checkout -b <name\>：创建并切换到 <name\> 分支，相当于以下两条命令
    - git branch <name\>：创建 <name\> 分支
    - git checkout <name\>：切换到 <name\> 分支
- git merge <name\>：合并 <name\> 分支到当前分支
- git branch -d <name\>：删除 <name\> 分支
- git branch -D <name\>：强行删除没有被合并过的 <name\>分支
- git log --graph：查看分支合并图
- git merge --no-ff -m <message\> <name\>：普通模式合并，禁用 fast forward，从分支历史上可以看出分支信息
- git stash：把当前工作现场“储藏”起来，等以后恢复现场后继续工作
- git stash pop：恢复工作现场，同时删除 stash 内容。相当于以下两条命令
    - git stash apply：恢复工作现场
    - git stash drop：删除 stash 内容
- git remote -v：查看远程库详细信息
- git push origin < branch name \>：推送分支
- git pull：抓取远程分支
- git checkout -b < branch name \> origin/< branch name \>：在本地创建和远程分支对应的分支，名称最好一致
- git branch --set-upstream < branch name \> origin/< branch name \>：建立本地分支和远程分支的关联
- git rebase：变基

### 1.5 标签管理

- git tag <tagname\>：用于新建一个标签，标签默认打在最新提交的commit上
- git tag <tagname\> commit id：用于新建一个标签，标签打在指定的commit上
- git tag -a <tagname\> -m <message\>：创建带有说明的标签，-a 指定标签名，-m 指定说明文字
- git tag：查看已有的标签条目
- git show <tagname\>：查看指定标签信息
- git push origin <tagname\>：推送指定的本地标签
- git push origin --tags：推送全部未推送过的本地标签
- git tag -d <tagname\>：删除指定的本地标签
- git push origin :refs/tags/<tagname\>：删除指定的远程标签（需要先从本地删除标签）

### 1.6 多远程库使用

- git remote add < origin name \> < xxx.com \>：将本地仓库与远程库关联
- git remote rm < origin name \>： 删除与远程库的关联

### 1.7 自定义 Git

- git config --global color.ui true：让Git显示颜色
- git add -f < filename />：强制添加被 .gitignore 忽略的文件到 Git 仓库
- git config --global alias.st status：起别名，用 st 表示 status

## 2. 安装 Git

1. 在Windows上安装Git，在开始菜单里找到“Git”->“Git Bash”
2. 在命令行输入：
    - git config --global user.name "Your Name"
    - git config --global user.email "email@example.com"
    - 用了--global参数，表示当前机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址

## 3. 创建版本库（仓库，repository）

- 可以简单理解成一个目录，里面所有文件都可以被Git管理起来，每个文件的修改、删除，Git都能跟踪，以便任何时刻都可以追踪历史或者“还原”
  
  
1. 选择一个合适的地方，创建一个空目录


```python
$ mkdir learngit
$ cd learngit
# 显示当前目录
$ pwd
/Users/michael/learngit
```

2. 通过git init命令把这个目录变成Git可以管理的仓库


```python
$ git init
Initialized empty Git repository in /Users/michael/learngit/.git/
# 如果你没有看到.git目录，那是因为这个目录默认是隐藏的，用ls -ah命令就可以看见
```

## 4. 把文件添加到版本库

- 不要使用Windows记事本编辑任何文本文件。Windows记事本在每个文件开头添加了0xefbbbf（十六进制）的字符，这会使我们遇到很多不可思议的问题

- 所有的版本控制系统，其实只能跟踪文本文件的改动，比如TXT文件，网页，所有的程序代码等。图片、视频、word这些二进制文件，虽然也能由版本控制系统管理，但没法跟踪文件的变化


1. 编写一个readme.txt文件，内容如下，并把文件放到learngit目录下（子目录也行）


```python
Git is a version control system.
Git is free software.
```

2. 用命令git add告诉Git，把文件添加到仓库


```python
$ git add readme.txt
```

3. 用命令git commit告诉Git，把文件提交到仓库
    - -m后面输入的是本次提交的说明，可以输入任意内容，当然最好是有意义的，这样就能从历史记录里方便地找到改动记录
    - git commit命令执行成功后会告诉你，1 file changed：1个文件被改动（我们新添加的readme.txt文件）；2 insertions：插入了两行内容（readme.txt有两行内容）


```python
$ git commit -m "wrote a readme file"
[master (root-commit) eaadf4e] wrote a readme file
 1 file changed, 2 insertions(+)
 create mode 100644 readme.txt
```

- Git添加文件需要add，commit一共两步，因为commit可以一次提交很多文件，所以你可以多次add不同的文件，比如：


```python
$ git add file1.txt
$ git add file2.txt file3.txt
$ git commit -m "add 3 files."
```

## 5. 时光机穿梭

1. 继续工作，修改了readme.txt文件，运行git status命令看看结果
2. 可运行git diff 查看修改内容
3. git add <file\>，git commit -m <message\> 提交


```python
# Git is a distributed version control system.
# Git is free software.

$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   readme.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

### 5.1 版本回退

1. 用 git log 命令查看从最近到最远的提交日志，HEAD表示当前版本，上一个版本就是HEAD^，上上一个版本就是HEAD^^


```python
$ git log
commit 1094adb7b9b3807259d8cb349e7df1d4d6477073 (HEAD -> master)
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Fri May 18 21:06:15 2018 +0800

    append GPL

commit e475afc93c209a690c39c13a46716e8fa000c366
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Fri May 18 21:03:36 2018 +0800

    add distributed

commit eaadf4e385e865d25c48e7ca9c8395c3f7dfaef0
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Fri May 18 20:59:18 2018 +0800

    wrote a readme file
```

2. 要把当前版本append GPL回退到上一个版本add distributed，就可以使用git reset命令


```python
$ git reset --hard HEAD^
HEAD is now at e475afc add distributed
```

3. git log再看看现在版本库的状态。最新的那个版本append GPL已经看不到了！想再回去，只要上面的命令行窗口还没有被关掉，可以顺着往上找，append GPL的commit id是1094adb...，于是就可以指定回到未来的某个版本。版本号没必要写全，前几位就可以了，Git会自动去找。当然也不能只写前一两位


```python
$ git log
commit e475afc93c209a690c39c13a46716e8fa000c366 (HEAD -> master)
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Fri May 18 21:03:36 2018 +0800

    add distributed

commit eaadf4e385e865d25c48e7ca9c8395c3f7dfaef0
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Fri May 18 20:59:18 2018 +0800

    wrote a readme file
```


```python
$ git reset --hard 1094a
HEAD is now at 83b0afe append GPL
```

4. 第二天后悔了，找不到新版本的commit id怎么办？git reflog 用来记录你的每一次命令


```python
$ git reflog
e475afc HEAD@{1}: reset: moving to HEAD^
1094adb (HEAD -> master) HEAD@{2}: commit: append GPL
e475afc HEAD@{3}: commit: add distributed
eaadf4e HEAD@{4}: commit (initial): wrote a readme file
```

### 5.2 工作区和暂存区

- Git和其他版本控制系统如SVN的一个不同之处就是有暂存区的概念
- 比如learngit文件夹就是一个工作区
- 工作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库（Repository）
- Git的版本库里最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支master，以及指向master的一个指针叫HEAD
    - 用git add把文件添加进去，实际上就是把文件修改添加到暂存区
    - 用git commit提交更改，实际上就是把暂存区的所有内容提交到当前分支
    - 可以简单理解为，需要提交的文件修改通通放到暂存区，然后，一次性提交暂存区的所有修改
    
### 5.3 管理修改

- Git比其他版本控制系统设计得优秀，因为Git跟踪并管理的是修改，而非文件

### 5.4 撤销修改

- git checkout -- readme.txt：把readme.txt文件在工作区的修改全部撤销，这里有两种情况：
    - readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态
    - readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态
    - 总之，就是让这个文件回到最近一次git commit或git add时的状态
- git reset HEAD <file\>：把暂存区的修改撤销掉（unstage），重新放回工作区

### 5.5 删除文件

- 命令git rm用于删除一个文件。如果一个文件已经被提交到版本库，那么永远不用担心误删。
- 但是要小心，只能恢复文件到最新版本，会丢失最近一次提交后修改的内容

## 6. 远程仓库

- 由于本地Git仓库和GitHub仓库之间的传输是通过SSH加密的，所以需要一点设置


1. 创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有id_rsa和id_rsa.pub这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key
2. 登陆GitHub，打开“Account settings”，“SSH Keys”页面，然后点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容


```python
$ ssh-keygen -t rsa -C "youremail@example.com"
```

- 需要把邮件地址换成自己的邮件地址，然后一路回车，使用默认值即可，可以无需设置密码
- 如果一切顺利的话，可以在用户主目录里找到 .ssh 目录，里面有 id_rsa 和 id_rsa.pub 两个文件，这两个就是 SSH Key 的秘钥对，id_rsa 是私钥，不能泄露出去，id_rsa.pub 是公钥，可以放心地告诉任何人

- 为什么GitHub需要SSH Key呢？因为GitHub需要识别出你推送的提交确实是你推送的，而不是别人冒充的，而Git支持SSH协议，所以，GitHub只要知道了你的公钥，就可以确认只有你自己才能推送。
- 当然，GitHub允许你添加多个Key。假定你有若干电脑，你一会儿在公司提交，一会儿在家里提交，只要把每台电脑的Key都添加到GitHub，就可以在每台电脑上往GitHub推送了。
- 最后友情提示，在GitHub上免费托管的Git仓库，任何人都可以看到喔（但只有你自己才能改）。所以，不要把敏感信息放进去。
- 如果你不想让别人看到Git库，有两个办法，一个是交点保护费，让GitHub把公开的仓库变成私有的，这样别人就看不见了（不可读更不可写）。另一个办法是自己动手，搭一个Git服务器，因为是你自己的Git服务器，所以别人也是看不见的。这个方法我们后面会讲到的，相当简单，公司内部开发必备。

### 6.1 添加远程库

1. 登陆GitHub，在右上角找到“Create a new repo”按钮，创建一个新的仓库
2. 在Repository name填入learngit，其他保持默认设置，点击“Create repository”按钮，就成功地创建了一个新的Git仓库
3. 根据GitHub的提示，在本地的learngit仓库下运行命令


```python
$ git remote add origin https://github.com/michaelliao/learngit.git
```

- 下一步把本地库的所有内容推送到远程库上


```python
$ git push -u origin master
Counting objects: 20, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (15/15), done.
Writing objects: 100% (20/20), 1.64 KiB | 560.00 KiB/s, done.
Total 20 (delta 5), reused 0 (delta 0)
remote: Resolving deltas: 100% (5/5), done.
To github.com:michaelliao/learngit.git
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.
```

- git push 命令实际上是把当前分支master推送到远程
- 由于远程库是空的，第一次推送master分支时，加上了 -u 参数，Git 不但会把本地的 master 分支内容推送的远程新的 master 分支，还会把本地的 master 分支和远程的 master 分支关联起来，在以后的推送或者拉取时就可以简化命令
- 从现在起，只要本地作了提交，就可以通过以下命令把本地 master 分支的最新修改推送至 GitHub


```python
$ git push origin master
```

<b>SSH警告</b>

- 当第一次使用 Git 的clone或者push命令连接GitHub时，会得到一个警告。这是因为Git使用SSH连接，而SSH连接在第一次验证GitHub服务器的Key时，需要你确认GitHub的Key的指纹信息是否真的来自GitHub的服务器，输入yes回车即可。


```python
The authenticity of host 'github.com (xx.xx.xx.xx)' can't be established.
RSA key fingerprint is xx.xx.xx.xx.xx.
Are you sure you want to continue connecting (yes/no)?
```

### 6.2 从远程库克隆

- 首先登陆GitHub，创建一个新的仓库，名字叫gitskills
- 勾选Initialize this repository with a README，这样GitHub会自动为我们创建一个README.md文件
- 用命令git clone克隆一个本地库


```python
$ git clone git@github.com:michaelliao/gitskills.git
Cloning into 'gitskills'...
remote: Counting objects: 3, done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 3
Receiving objects: 100% (3/3), done.
```

- 默认的 git:// 使用 ssh，但也可以使用 https 等其他协议，使用 https 速度稍慢。在某些只开放 http 端口的公司内部无法使用 ssh 协议

## 7. 分支管理

- 你创建了一个属于你自己的分支，别人看不到，还继续在原来的分支上正常工作，而你在自己的分支上干活，想提交就提交，直到开发完毕后，再一次性合并到原来的分支上，这样，既安全，又不影响别人工作。

### 7.1 创建与合并分支

- 每次提交，Git都把各版本串成一条时间线，这条时间线就是一个分支。
- 只有一条时间线时，在Git里，这个分支叫主分支，即master分支
- HEAD严格来说不是指向提交，而是指向master，master才是指向提交的，所以，HEAD指向的就是当前分支。
- 开始时master分支是一条线，Git用master指向最新的提交，再用HEAD指向master，就能确定当前分支及当前分支的提交点
- 每次提交，master分支都会向前移动一步，随着不断提交，master分支的线越来越长


- 当创建新的分支如dev时，Git新建了一个指针叫dev，指向master相同的提交，再把HEAD指向dev，就表示当前分支在dev上
- 从现在起对工作区的修改和提交就是针对dev分支了，新提交一次后，dev指针往前移动一步，而master指针不变
- 若在dev上的工作完成了，可以把dev合并到master上。最简单的方法就是直接把master指向dev的当前提交
- 合并完分支后，甚至可以删除dev分支，就是把dev指针给删掉，删掉后就剩下了一条master分支


1. 创建dev分支，并切换到dev分支


```python
$ git checkout -b dev
Switched to a new branch 'dev'

# git checkout命令加上-b参数表示创建并切换，相当于以下两条命令
$ git branch dev
$ git checkout dev
Switched to branch 'dev'
```

2. 用git branch命令查看当前分支，当前分支前面会标一个*号。然后即可在dev分支上正常提交，比如对readme.txt做个修改，加上一行，然后提交


```python
$ git branch
* dev
  master
```


```python
Creating a new branch is quick.

$ git add readme.txt 
$ git commit -m "branch test"
[dev b17d20e] branch test
 1 file changed, 1 insertion(+)
```

3. 现在dev分支的工作完成，可以切换回master分支。切换回master分支后，再查看一个readme.txt文件，刚才添加的内容不见了！因为那个提交是在dev分支上，而master分支此刻的提交点并没有变


```python
$ git checkout master
Switched to branch 'master'
```

4. 把dev分支的工作成果合并到master分支上


```python
$ git merge dev
Updating d46f35e..b17d20e
Fast-forward
 readme.txt | 1 +
 1 file changed, 1 insertion(+)
```

- git merge命令用于合并指定分支到当前分支。合并后，再查看readme.txt的内容，就可以看到，和dev分支的最新提交是完全一样的
- Fast-forward信息，是Git告诉我们，这次合并是“快进模式”，即直接把master指向dev的当前提交，所以合并速度非常快，不是每次合并都能Fast-forward


5. 合并完成后，就可以放心地删除dev分支了。删除后，查看branch，就只剩下master分支了


```python
$ git branch -d dev
Deleted branch dev (was b17d20e).

$ git branch
* master
```

- 因为创建、合并和删除分支非常快，所以Git鼓励你使用分支完成某个任务，合并后再删掉分支，这和直接在master分支上工作效果是一样的，但过程更安全

### 7.2 解决冲突

1. 准备新的feature1分支，修改readme.txt最后一行，并在feature1分支上提交


```python
$ git checkout -b feature1
Switched to a new branch 'feature1'

# Creating a new branch is quick AND simple.

$ git add readme.txt

$ git commit -m "AND simple"
[feature1 14096d0] AND simple
 1 file changed, 1 insertion(+), 1 deletion(-)
```

2. 切换到master分支（Git还会自动提示我们当前master分支比远程的master分支要超前1个提交），在master分支上修改readme.txt文件的最后一行并提交


```python
$ git checkout master
Switched to branch 'master'
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)
    
# Creating a new branch is quick & simple.

$ git add readme.txt 
$ git commit -m "& simple"
[master 5dc6824] & simple
 1 file changed, 1 insertion(+), 1 deletion(-)
```

3. 现在，master分支和feature1分支各自都分别有新的提交，这种情况下，Git无法执行“快速合并”，只能试图把各自的修改合并起来，但这种合并就可能会有冲突。Git告诉我们，readme.txt文件存在冲突，必须手动解决冲突后再提交。git status也可以告诉我们冲突的文件


```python
$ git merge feature1
Auto-merging readme.txt
CONFLICT (content): Merge conflict in readme.txt
Automatic merge failed; fix conflicts and then commit the result.

$ git status
On branch master
Your branch is ahead of 'origin/master' by 2 commits.
  (use "git push" to publish your local commits)

You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)

    both modified:   readme.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

4. 可以直接查看readme.txt的内容，Git用<<<<<<<，=======，>>>>>>>标记出不同分支的内容。修改后再提交


```python
Git is a distributed version control system.
Git is free software distributed under the GPL.
Git has a mutable index called stage.
Git tracks changes of files.
<<<<<<< HEAD
Creating a new branch is quick & simple.
=======
Creating a new branch is quick AND simple.
>>>>>>> feature1

# Creating a new branch is quick and simple.

$ git add readme.txt 
$ git commit -m "conflict fixed"
[master cf810e4] conflict fixed
```

5. 用带参数的git log也可以看到分支的合并情况。最后，删除feature1分支


```python
$ git log --graph --pretty=oneline --abbrev-commit
*   cf810e4 (HEAD -> master) conflict fixed
|\  
| * 14096d0 (feature1) AND simple
* | 5dc6824 & simple
|/  
* b17d20e branch test
* d46f35e (origin/master) remove test.txt
* b84166e add test.txt
* 519219b git tracks changes
* e43a48b understand how stage works
* 1094adb append GPL
* e475afc add distributed
* eaadf4e wrote a readme file

$ git branch -d feature1
Deleted branch feature1 (was 14096d0).
```

### 7.3 分支管理策略

- 通常，合并分支时，如果可能，Git会用Fast forward模式，但这种模式下，删除分支后，会丢掉分支信息
- 如果强制禁用Fast forward模式，Git会在merge时生成一个新的commit，这样从分支历史上就可以看出分支信息

1. 仍然创建并切换dev分支，修改readme.txt文件，并提交一个新的commit，切换回master


```python
$ git checkout -b dev
Switched to a new branch 'dev'

$ git add readme.txt 
$ git commit -m "add merge"
[dev f52c633] add merge
 1 file changed, 1 insertion(+)
    
$ git checkout master
Switched to branch 'master'
```

2. 准备合并dev分支，请注意--no-ff参数，表示禁用Fast forward。因为本次合并要创建一个新的commit，所以加上-m参数，把commit描述写进去。合并后，用git log看看分支历史


```python
$ git merge --no-ff -m "merge with no-ff" dev
Merge made by the 'recursive' strategy.
 readme.txt | 1 +
 1 file changed, 1 insertion(+)

$ git log --graph --pretty=oneline --abbrev-commit
*   e1e9c68 (HEAD -> master) merge with no-ff
|\  
| * f52c633 (dev) add merge
|/  
*   cf810e4 conflict fixed
...
```

<b>总结：分支策略</b>

在实际开发中应该按照几个基本原则进行分支管理：

- master分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活
- 干活都在dev分支上，也就是说，dev分支是不稳定的，到某个时候，比如1.0版本发布时，再把dev分支合并到master上，在master分支发布1.0版本
- 和小伙伴们每个人都在dev分支上干活，每个人都有自己的分支，时不时地往dev分支上合并就可以了

### 7.4 bug 分支

- 当你接到修复代号101的bug的任务时，很自然地，你想创建一个分支issue-101来修复它，可当前正在dev上进行的工作只进行到一半，还没法提交，预计完成还需1天时间。但是，必须在两个小时内修复该bug，怎么办？
- 幸好，Git还提供了一个stash功能，可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作


```python
$ git status
On branch dev
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    new file:   hello.py

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   readme.txt
        
        
$ git stash
Saved working directory and index state WIP on dev: f52c633 add merge
```

- 现在，用git status查看工作区，就是干净的（除非有没有被Git管理的文件），可以放心地创建分支来修复bug


1. 首先确定要在哪个分支上修复bug，假定需要在master分支上修复，就从master创建临时分支


```python
$ git checkout master
Switched to branch 'master'
Your branch is ahead of 'origin/master' by 6 commits.
  (use "git push" to publish your local commits)

$ git checkout -b issue-101
Switched to a new branch 'issue-101'
```

2. 现在修复bug，需要把“Git is free software ...”改为“Git is a free software ...”，然后提交：


```python
$ git add readme.txt 
$ git commit -m "fix bug 101"
[issue-101 4c805e2] fix bug 101
 1 file changed, 1 insertion(+), 1 deletion(-)
```

3. 修复完成后，切换到master分支，并完成合并，最后删除issue-101分支：


```python
$ git checkout master
Switched to branch 'master'
Your branch is ahead of 'origin/master' by 6 commits.
  (use "git push" to publish your local commits)

$ git merge --no-ff -m "merged bug fix 101" issue-101
Merge made by the 'recursive' strategy.
 readme.txt | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
```

4. 现在，是时候接着回到dev分支干活了！用git stash list命令看看刚才的工作现场


```python
$ git checkout dev
Switched to branch 'dev'

$ git status
On branch dev
nothing to commit, working tree clea

$ git stash list
stash@{0}: WIP on dev: f52c633 add merge
```

5. 工作现场还在，Git把stash内容存在某个地方了，但是需要恢复一下，有两个办法：一是用git stash apply恢复，但是恢复后，stash内容并不删除，你需要用git stash drop来删除；另一种方式是用git stash pop，恢复的同时把stash内容也删了


```python
$ git stash pop
On branch dev
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    new file:   hello.py

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   readme.txt

Dropped refs/stash@{0} (5d677e2ee266f39ea296182fb2354265b91b3b2a)
```

6. 你可以多次stash，恢复的时候，先用git stash list查看，然后恢复指定的stash，用命令


```python
$ git stash apply stash@{0}
```

### 7.5 Feature 分支

- 软件开发中，总有新的功能要不断添加进来。添加一个新功能时，你肯定不希望因为一些实验性质的代码，把主分支搞乱了，所以，每添加一个新功能，最好新建一个feature分支，在上面开发完成后，合并，最后，删除该feature分支

### 7.6 多人协作

- 当从远程仓库克隆时，实际上Git自动把本地的master分支和远程的master分支对应起来了，远程仓库的默认名称是origin
- 要查看远程库的信息，用git remote，用git remote -v显示更详细的信息


```python
$ git remote
origin

$ git remote -v
origin  git@github.com:michaelliao/learngit.git (fetch)
origin  git@github.com:michaelliao/learngit.git (push)
```

#### 7.6.1 推送分支

- 推送分支，即把该分支上的所有本地提交推送到远程库对应的远程分支上
- 但是，并不是一定要把本地分支往远程推送，哪些分支需要推送，哪些不需要呢？
    - master 分支是主分支，因此要时刻与远程同步
    - dev 分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步
    - bug 分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug
    - feature 分支是否推到远程，取决于是否有和小伙伴合作在上面开发


```python
$ git push origin master

# 如果要推送其他分支，比如dev，就改成：
$ git push origin dev
```

#### 7.6.2 抓取分支

- 多人协作时，大家都会往 master 和 dev 分支上推送各自的修改。现在，小伙伴可以在另一台电脑（注意要把SSH Key添加到GitHub）或者同一台电脑的另一个目录下克隆


```python
$ git clone git@github.com:michaelliao/learngit.git
Cloning into 'learngit'...
remote: Counting objects: 40, done.
remote: Compressing objects: 100% (21/21), done.
remote: Total 40 (delta 14), reused 40 (delta 14), pack-reused 0
Receiving objects: 100% (40/40), done.
Resolving deltas: 100% (14/14), done.
```

- 当小伙伴从远程库clone时，默认情况下，只能看到本地的 master 分支。现在小伙伴要在 dev 分支上开发，就必须创建远程origin 的 dev 分支到本地，于是他用这个命令创建本地 dev 分支


```python
$ git branch
* master

$ git checkout -b dev origin/dev
```

- 现在，他可以在 dev 上继续修改，然后，时不时地把 dev 分支push到远程


```python
$ git add env.txt

$ git commit -m "add env"
[dev 7a5e5dd] add env
 1 file changed, 1 insertion(+)
 create mode 100644 env.txt

$ git push origin dev
Counting objects: 3, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 308 bytes | 308.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To github.com:michaelliao/learngit.git
   f52c633..7a5e5dd  dev -> dev
```

- 小伙伴已经向 origin/dev 分支推送了他的提交，而碰巧你也对同样的文件作了修改，并试图推送


```python
$ cat env.txt
env

$ git add env.txt

$ git commit -m "add new env"
[dev 7bd91f1] add new env
 1 file changed, 1 insertion(+)
 create mode 100644 env.txt

$ git push origin dev
To github.com:michaelliao/learngit.git
 ! [rejected]        dev -> dev (non-fast-forward)
error: failed to push some refs to 'git@github.com:michaelliao/learngit.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

- 推送失败，因为小伙伴的最新提交和你试图推送的提交有冲突，解决办法也很简单，Git 已经提示我们，先用 git pull 把最新的提交从 origin/dev 抓下来，然后，在本地合并，解决冲突，再推送


```python
$ git pull
There is no tracking information for the current branch.
Please specify which branch you want to merge with.
See git-pull(1) for details.

    git pull <remote> <branch>

If you wish to set tracking information for this branch you can do so with:

    git branch --set-upstream-to=origin/<branch> dev
```

- git pull 也失败了，由于没有指定本地 dev 分支与远程 origin/dev 分支的链接，根据提示设置 dev和origin/dev 的链接，再poll


```python
$ git branch --set-upstream-to=origin/dev dev
Branch 'dev' set up to track remote branch 'dev' from 'origin'.

$ git pull
Auto-merging env.txt
CONFLICT (add/add): Merge conflict in env.txt
Automatic merge failed; fix conflicts and then commit the result.
```

- 这回git pull成功，但是合并有冲突，需要手动解决，解决的方法和分支管理中的解决冲突完全一样。解决后，提交，再push


```python
$ git commit -m "fix env conflict"
[dev 57c53ab] fix env conflict

$ git push origin dev
Counting objects: 6, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (4/4), done.
Writing objects: 100% (6/6), 621 bytes | 621.00 KiB/s, done.
Total 6 (delta 0), reused 0 (delta 0)
To github.com:michaelliao/learngit.git
   7a5e5dd..57c53ab  dev -> dev
```

#### 7.6.3 总结

多人协作的工作模式通常是这样：

- 首先，试图用 git push origin <branch-name> 推送自己的修改
- 如果推送失败，则因为远程分支比你的本地更新，需要先用 git pull 试图合并
- 如果合并有冲突，则解决冲突，并在本地提交
- 没有冲突或者解决掉冲突后，再用 git push origin <branch-name> 推送就能成功
- 如果 git pull 提示 no tracking information，则说明本地分支和远程分支的链接关系没有创建，用命令 git branch --set-upstream-to <branch-name> origin/<branch-name>

### 7.7 Rebase

- rebase 操作可以把本地未 push 的分叉提交历史整理成直线，看啊起来更直观；缺点是本地的分叉提交已经被修改过了
- rebase 的目的是使得我们在查看历史提交的变化时更容易，因为分叉的提交需要三方对比

## 8. 标签管理

- 发布一个版本时，通常会先在版本库中打一个标签（tag），这样，就唯一确定了打标签时刻的版本。将来无论什么时候，取某个标签的版本，就是把那个打标签的时刻的历史版本取出来。所以，标签也是版本库的一个快照
- Git 的标签虽然是版本库的快照，但其实它就是指向某个 commit 的指针（跟分支很像，但是分支可以移动，标签不能移动），所以，创建和删除标签都是瞬间完成的
- 标签总是和某个 commit 挂钩。如果这个 commit 既出现在 master 分支，又出现在 dev 分支，那么在这两个分支上都可以看到这个标签


1. 首先，切换到需要打标签的分支上


```python
$ git branch
* dev
  master
$ git checkout master
Switched to branch 'master'
```

2. 然后，敲命令git tag <name\>就可以打一个新标签，可以用命令git tag查看所有标签


```python
$ git tag v1.0

$ git tag
v1.0
```

3. 默认标签是打在最新提交的commit上的。有时候，如果忘了打标签，比如，现在已经是周五了，但应该在周一打的标签没有打，怎么办？方法是找到历史提交的commit id，然后打上就可以了，比方说要对add merge这次提交打标签，它对应的commit id是f52c633


```python
$ git log --pretty=oneline --abbrev-commit
12a631b (HEAD -> master, tag: v1.0, origin/master) merged bug fix 101
4c805e2 fix bug 101
e1e9c68 merge with no-ff
f52c633 add merge
cf810e4 conflict fixed
5dc6824 & simple
14096d0 AND simple
b17d20e branch test
d46f35e remove test.txt
b84166e add test.txt
519219b git tracks changes
e43a48b understand how stage works
1094adb append GPL
e475afc add distributed
eaadf4e wrote a readme file
```


```python
$ git tag v0.9 f52c633

$ git tag
v0.9
v1.0
```

4. 标签不是按时间顺序列出，而是按字母排序的。可以用git show <tagname\>查看标签信息


```python
$ git show v0.9
commit f52c63349bc3c1593499807e5c8e972b82c8f286 (tag: v0.9)
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Fri May 18 21:56:54 2018 +0800

    add merge

diff --git a/readme.txt b/readme.txt
...
```

5. 还可以创建带有说明的标签，用 -a 指定标签名，-m 指定说明文字。用命令git show <tagname>可以看到说明文字


```python
$ git tag -a v0.1 -m "version 0.1 released" 1094adb

$ git show v0.1
tag v0.1
Tagger: Michael Liao <askxuefeng@gmail.com>
Date:   Fri May 18 22:48:43 2018 +0800

version 0.1 released

commit 1094adb7b9b3807259d8cb349e7df1d4d6477073 (tag: v0.1)
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Fri May 18 21:06:15 2018 +0800

    append GPL

diff --git a/readme.txt b/readme.txt
...
```

6. 如果标签打错了，也可以删除。如果要推送某个标签到远程，使用命令 git push origin <tagname\>。或者，一次性推送全部尚未推送到远程的本地标签


```python
$ git tag -d v0.1
Deleted tag 'v0.1' (was f15b0dd)

$ git push origin v1.0
Total 0 (delta 0), reused 0 (delta 0)
To github.com:michaelliao/learngit.git
 * [new tag]         v1.0 -> v1.0

$ git push origin --tags
Total 0 (delta 0), reused 0 (delta 0)
To github.com:michaelliao/learngit.git
 * [new tag]         v0.9 -> v0.9
```

7. 如果标签已经推送到远程，要删除远程标签就要先从本地删除。然后，从远程删除。删除命令也是push，但是格式如下


```python
$ git tag -d v0.9
Deleted tag 'v0.9' (was f52c633)

$ git push origin :refs/tags/v0.9
To github.com:michaelliao/learngit.git
 - [deleted]         v0.9
```

## 9. 使用 GitHub

- 在GitHub上，可以任意Fork开源仓库
- 自己拥有Fork后的仓库的读写权限
- 可以推送pull request给官方仓库来贡献代码

## 10. 使用码云

- 上传 SSH 公钥，用户主目录下的.ssh/id_rsa.pub文件内容
- 在本地库上使用命令 git remote add origin 把它和码云的远程库关联
- 若本地库已经关联了 GitHub 远程库，可以用命令 git remote rm origin 先删除关联，再关联码云的远程库
- 若要同时使用多个远程库，需要用不同的名称来标识不同的远程库
    - 先删除已关联的名为 origin 的远程库 git remote rm origin
    - 关联GitHub的远程库（库名由origin改为github） git remote add github git@github.com:michaelliao/learngit.git
    - 关联码云的远程库 git remote add gitee git@gitee.com:liaoxuefeng/learngit.git
- 推送到GitHub：git push github master
- 推送到码云：git push gitee master


## 11. 自定义 Git

- 让Git显示颜色 git config --global color.ui true

### 11.1 忽略特殊文件

- 在Git工作区的根目录下创建一个特殊的.gitignore文件，把要忽略的文件名填进去，Git就会自动忽略这些文件
- GitHub已经准备了各种配置文件，只需要组合一下就可以使用了https://github.com/github/gitignore
- 检验.gitignore的标准是git status命令是不是说working directory clean
- .gitignore文件本身要放到版本库里，并且可以对.gitignore做版本管理
- 强制添加被忽略的文件到 Git：git add -f < filename />

<b>忽略文件的原则</b>
- 忽略操作系统自动生成的文件，比如缩略图等
- 忽略编译生成的中间文件、可执行文件等，也就是如果一个文件是通过另一个文件自动生成的，那自动生成的文件就没必要放进版本库，比如Java编译产生的.class文件
- 忽略自己的带有敏感信息的配置文件，比如存放口令的配置文件

### 11.2 配置别名

- 用 st 表示 status：git config --global alias.st status。以后就可以用 git st 就表示 git status
- 每个仓库的 Git 配置文件都放在.git/config文件中，别名就在[alias]后面，要删除别名，直接把对应的行删掉即可
- 当前用户的 Git 配置文件放在用户主目录下的一个隐藏文件.gitconfig中，配置别名也可以直接修改这个文件，如果改错了，可以删掉文件重新通过命令配置

### 11.3 搭建 Git 服务器

......
