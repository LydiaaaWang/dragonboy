

# git
c语言有什么用？c语言开发了git.

####名字和邮箱
设置:

git config --global user.name "you name"

git config --global user.email "15313168617@163.com"
>待修改：
这里的名字是不是显示到仓库提交那里的名字？我改成功了吗？
没有，并没有成功。不，修改成功了。（有点懵，不知道是修改这里name的作用还是修改阿里巴巴资料的作用）（最后发现是因为阿里巴巴的资料改了，所以才修改了名字）

要随时掌握工作区的状态：
使用git status命令
如果git status 告诉你文件被修改过，用git diff 可以查看修改内容

想要查看commit的记录，使用 git log
想要让每一次提交在一行内显示：git log --pretty=oneline
这样看起来比在很多行上看更容易知道自己提交记录，提交记录是最晚提交的在最上边，类似于栈。

###git版本
git中使用head表示当前版本。上一个版本就是head^,上上一个版本就是head^^.版本多了之后就可以使用波浪号：head~100,表示前100个的版本。
head^==head~1
head^^==head~2

回退到上一个版本的命令：`git reset --hard head^`
如果后悔了，觉得不应该回退，那么还可以根据之前的sha码再将版本回退到刚刚的样子。`git reset --hard a4sse`
最后的指的是sha码，从前往后写个5、6位一般就够了，具体写到几位根据现有的log去看看。只要没有重复的、能让git识别出来就可以。

git版本回退非常快是因为git内部有个指向当前版本的head指针，当回退版本的时候，git仅仅是把head从指向一个commit到另一个commit.

有一个命令可以看到自己的每一次提交：git reflog
如果想要版本修改的话，那么可以看到每一个版本的sha值。有了这个值，就可以随意切换版本到哪一个了。因为在git中，总是有后悔药可以吃的。

关于版本的总结：
head指向的版本是当前版本，因此，git允许我们在版本的历史之间穿梭，使用命令git reset --hard commit_id;
穿梭前，用git log查看提交历史，可以确定回退到哪一个版本
要重返未来的某一个版本，用git reflog查看命令历史，去寻找要回去版本的sha值。

###工作区working directory和暂存区stage
工作区是当前看到的目录(不算上.git,因为.git代表仓库),暂存区是git add后将文件提交到的地方。commit之后就提交到了当前分支上。

有人说，git比其他版本管理系统设计的优秀的原因是git跟踪并管理的是修改，而不是文件。

自己要提交了，所以最好查看一下当前的修改再提交(git add/git commit),那么如何知道本地修改了哪些呢？
git diff HEAD -- readme.txt

一个实践：只有git commit了才能pull下来新的东西，仅仅只是git add是不行的。

git status 可以查看当前工作区的状态。查看之后会发现对方提醒了两个内容：
```
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   readme.txt

no changes added to commit (use "git add" and/or "git commit -a")
```
意思是接下来你要么使用git add 去添加到暂存区，要么使用git checkout 丢弃刚刚工作区的修改。并且当前没有内容是使用了git add 但是没有git commit 的。
一个感想：现在慢慢理解了为什么说英语是一个关卡了，如果懂英语，那么按照字面的意思都能猜测这些命令是啥意思。

回到上一次git commit后的状态。

如果git add了自己不应该提交的内容，那么可以使用git reset HEAD <file>把暂存区的内容撤销掉。

git reset 命令既可以回退版本，也可以把暂存区的修改回退到工作区。

####几个场景【待完善】
1. 场景一：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令`git checkout -- file`
2. 场景二：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令`git reset HEAD <file>`,第二步就回到了场景一，第二部按场景1操作。
3. 场景三：已经提交了不合适的修改到版本库，想要撤销本次提交：
`git log`查看历次提交，想要回退到哪一个版本就使用 `git reset --hard commit_id`.这针对的是没有提交到远程仓库的回退。

一个感悟：突然意识到了为什么.git是隐藏文件，是用来防坏人的，如果别人不小心给修改了，那么可以使用git命令轻松恢复。能使用git命令的前提是这得是一个git仓库。

git checkout本质做的是替换，用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以一键还原。

但是从来没有被添加到版本库的内容被删除或者被修改了，想要恢复，是不可能的。所以要勤commit.

突然对ssh-key的理解感觉就彻底理解了：
为什么一般情况下要给远程的仓库加上自己的公钥呢？因为远程仓库当自己提交的时候得识别一下自己的身份，那么怎么创建的这个身份呢？每个电脑的用户主目录下都会存一个ssh目录，如果没有可以使用命令`$ ssh-keygen -t rsa -C "youremail@example.com"`生成 ,然后一路enter就可以。生成后会有id_rsa和id_rsa.pub两个文件，带pub(public)后缀的是公钥，不带的是私钥。最终添加到仓库的ssh那里的也是公钥。

github允许使用多个key,所以可以在很多台电脑上推送向一个仓库。

github创建仓库那里其实一直都是很清晰明白的提醒，只是以前从来没有去读过。还好，现在越来越好了。我能看懂了。才发现原来提醒这么友好。

git clone:
如果有多个人协作开发，那么每个人各自从远程克隆一份就可以了。
这样就可以当有新成员加入的时候直接克隆一份，并且把他的公钥放到本仓库的ssh中，那么就可以让对方也提交了。

###git分支
分支在实际中有什么用呢？假设你准备开发一个新功能，但是需要两周才能完成，第一周你写了50%的代码，如果立刻提交，由于代码还没写完，不完整的代码库会导致别人不能干活了。如果等代码全部写完再一次提交，又存在丢失每天进度的巨大风险。

现在有了分支，就不用怕了。你创建了一个属于你自己的分支，别人看不到，还继续在原来的分支上正常工作，而你在自己的分支上干活，想提交就提交，直到开发完毕后，再一次性合并到原来的分支上，这样，既安全，又不影响别人工作。

并且git分支还很快，别人想要切换到分支也可以切换到分支。

查看分支：git branch
创建分支：git branch <name>  eg:git branch popout 就创建了一个名字叫popout的分支
切换分支: git checkout <name> eg:git checkout popout 就从当前master分支切换到了popout分支上了，如果此时git add /git commit 那么就是提交到了本分支上
创建+切换分支：git checkout -b <name> eg:git checkout -b popout = git branch popout->git checkout popout 

合并某分支到当前分支：git merge <name> eg:如果想要合并某个分支到主分支上，那么先git checkout master，然后 git merge popout,那么就能把这个分支合并到master分支上了。

删除分支：git branch -d <name>  eg:当分支合并到主分支上之后，那么该分支就没有用了，就可以直接删除了，git branch -d popout 但是删除的时候需要在哪个上边删除呢？【待定】