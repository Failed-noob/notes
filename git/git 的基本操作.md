## **git 的基本操作**



**git** 是目前最先进的分布式版本控制系统;

在windows上 需要下一个 git 相当于一个linux的模拟机 在git bash中  清楚屏幕 clear 和reset

clear 实际上是向后翻了一页 而reset 时整体刷新 但速度较慢



![](D:\QQ截图\git基本操作.PNG)

```markdown
步骤:
//1 在合适的地方创建一个空的文件夹 然后右键 git bash here;[attention: 如果你使用Windows系统，为了避免遇到各种莫名其妙的问题，请确保目录名（包括父目录）不包含中文。]

//2 git init  这个命令将目录变成git可以管理的仓库; 此时在那个空文件夹里就会有一个 .git的文件夹

//3 然后在空文件夹下或者子目录下 创建一个.txt 后缀的文件 然后随便写点什么
然后  git add 文件名及后缀

//4然后用git commit -m '文件描述'   commit可以一次性提交很多文件

```



![](D:\QQ截图\git基本操作-1.PNG)

```markdown
//5 git status 接着上面的说明 它会显示 on branch master nothing to commit 在master 分支上(master 是默认的就有的分支) 没有什么要去提交;
git status 会显示git提交的状态
当你修改过 commit 过的文件时 他会显示你修改的部分细节
//git diff Readme.txt 会显示更详细的一些细节;  然后重新add commit

```



### **版本回退:**

```markdown
当我再次修改后  这次Readme.txt 就相当于 由三个版本了
//git log命令显示从最近到最远的提交日志 此时就是出现每个版本的作者和日期和一些其他不知道的玩意儿 反正我看着同冗长的 用下面的命令来让提交日志变得更简洁;
git log --pretty=oneline
//Git必须知道当前版本是哪个版本，在Git中，用HEAD表示当前版本 上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100。
 git reset --hard HEAD^  返回到上一个版本

//cat Readme.txt 查看现在Readme.txt中的内容;
此时就恢复到上个版本了 若你还想再返回到 此版本的下一个版本 在你没有关闭 窗口的情况下 往上翻 取 commit ID的前几位 然后按照git reset --hard 3610662b 
commit 没必要写全git 会自动取查找

//git reflog用来记录你的每一次命令：
```



来说写概念性的词

**工作区和暂存区:**

工作区: 就是最初 我创建的空文件夹 当然现在不是空的 当git init后会出现一个颜色淡一点的**.git**文件夹 这个不算工作区 是版本库  .git里 最重要的 称为stage (或者 index ) 的暂存区 另外git 为我们自动创建的第一个分支 master  以及指向master的指针HEAD 



![](D:\QQ截图\git过程.PNG)



##### **撤销修改**

若 在你准备提交时 你想撤销修改  你可以 git checkout -- 文件名 将在工作区 的修改全部撤销  

若 你已经将文件add到暂存区了 可以用 git reset HEAD 文件名    git reset 不仅可以回退版本 还可以 将暂存区的内容回退到工作区;





命令`git checkout -- readme.txt`意思就是，把`readme.txt`文件在工作区的修改全部撤销，这里有两种情况：

一种是`readme.txt`自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；

一种是`readme.txt`已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。





#### **删除文件:**

若 将文件add 到暂存区后 你在在工作区 将文件删除了 此时你 git status 会让你知道 那个文件删了 此时 我想恢复 怎么办 看下面:

git checkout -- 文件名 

```markdown
// 从版本库 删除文件
git rm testThree.txt
```

