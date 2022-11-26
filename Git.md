# Git

Git属于分散性版本管理系统，是为版本管理而设计的软件。

Linux--Linus在05年开发了git原型程序

SVN，CVS集中式的版本控制系统，集中存放中央服务器的

> Git is a free and open source distributed version control system designed to handle everything from small to very large projects with speed and efficiency.
>
> Git is easy to learn and has a tiny footprint with lightning fast performance. It outclasses SCM tools like Subversion, CVS, Perforce, and ClearCase with features like cheap local branching, convenient staging areas, and multiple workflows.
>
> Git 是一个免费的开源分布式版本控制系统，旨在快速高效地处理从小型到超大型项目的所有内容。 Git 易于学习，占用空间很小，性能快如闪电。它超越了Subversion，CVS，Perforce和ClearCase等SCM工具，具有廉价的本地分支，方便的暂存区域和多个工作流程等功能。

## 安装

组件的选择，默认就可以

![image-20221126083030535](Git.assets/image-20221126083030535.png)

注册账号

[Gitee - 基于 Git 的代码托管和研发协作平台](https://gitee.com/)

https://github.com/

## 设置

### 设置姓名和邮箱

```shell
git config --global user.name "你的名字"
git config --global user.email "你的邮箱"
```

git config命令指定与git相关的配置

config配置级别：

- system：系统
- global：用户
- local：当前仓库

范围system>global>local

```shell
# 查看git配置
git config --list
```

![image-20221126092904395](Git.assets/image-20221126092904395.png)

### 提高命令输出的可读性

设置color.ui为auto，让输出有更高的可读性

```shell
git config --global color.ui auto
```

![image-20221126092855114](Git.assets/image-20221126092855114.png)

### GitHub设置

```shell
# 1、打开git bash
# 2、生成sshkey
ssh-keygen -t rsa -C "741510728@qq.com"
```

![image-20221126101755047](Git.assets/image-20221126101755047.png)

然后打开路径

`C:\Users\Administrator\.ssh`

​	![image-20221126102007932](Git.assets/image-20221126102007932.png)

分别是私钥和公钥

我们用记事本打开公钥id_rsa.pub，然后全选复制所有内容

![image-20221126102109323](Git.assets/image-20221126102109323.png)

完成设置后，邮箱会收到提示邮件，这个时候，我们就可以使用私钥和GitHub进行认证和通信了。

执行命令验证

```shell
ssh -T git@github.com
```

![image-20221126102454497](Git.assets/image-20221126102454497.png)

## 创建仓库

![image-20221126103422353](Git.assets/image-20221126103422353.png)

![image-20221126103510905](Git.assets/image-20221126103510905.png)

```bash
cd /f/tarena/授课/枣庄/VIP创新课程（行业）/code
# 把github上的仓库，克隆到本地
git clone https://github.com/waqwb/HelloWorld.git
```

![image-20221126105352918](Git.assets/image-20221126105352918.png)

```bash
Administrator@qiu MINGW64 /f/tarena/授课/枣庄/VIP创新课程（行业）/code
$ cd HelloWorld/

Administrator@qiu MINGW64 /f/tarena/授课/枣庄/VIP创新课程（行业）/code/HelloWorld (main)
$ pwd
/f/tarena/授课/枣庄/VIP创新课程（行业）/code/HelloWorld

Administrator@qiu MINGW64 /f/tarena/授课/枣庄/VIP创新课程（行业）/code/HelloWorld (main)
$ echo "# HelloWorld" >> README.md
```

![image-20221126105425085](Git.assets/image-20221126105425085.png)

```bash
git add README.md
git commit -m "first commit"
```

![image-20221126113329134](Git.assets/image-20221126113329134.png)

![image-20221126113408179](Git.assets/image-20221126113408179.png)

此时只是提交操作，并不会把我们目录中的内容上传至网站

```bash
git push -u origin main
```

第一次push的时候，会在git bash中有一个登录github的验证，大家验证即可

![image-20221126113504543](Git.assets/image-20221126113504543.png)

出现以下内容证明成功了，在浏览器中刷新GitHub中的仓库

## 番外

关注作者和star仓库

![image-20221126112155748](Git.assets/image-20221126112155748.png)

```bash
cd HelloWorld
echo "# HelloWorld" >> README.md
# 当仓库没有HelloWorld仓库的时候  .git
git init
git add README.md
git commit -m "first commit"
git branch -M main
# 指定我们要上传到的仓库的地址
git remote add origin https://github.com/waqwb/HelloWorld.git
git push -u origin main
```

## 练习

新建一个hello.java,写一段代码添加到文件中

上传至GitHub中

## Git基本操作

### 初始化仓库

```bash
git init
```

![image-20221126140521073](Git.assets/image-20221126140521073.png)

如果初始化成功，执行git init命令后会在目录下生成一个.git目录，目录中存储着管理当前目录内容所需的仓库数据。

![image-20221126140621265](Git.assets/image-20221126140621265.png)

这个目录的内容称之为“附属于该仓库的工作树”

文件的编辑等操作在工作树中进行，然后记录到仓库中，以此来管理文件的历史快照。

如果想将文件恢复到原先的状态，可以从仓库中调取之前的快照，在工作树中打开。

开发者可以通过这种方式获取以往的文件。

### 查看仓库的状态

```bash
git status	
```

显示git仓库的状态。

工作树和仓库被操作的过程中，状态会不断地发生变化，可以使用这个命令来查看当前的状态。

![image-20221126141042324](Git.assets/image-20221126141042324.png)

> 提交commit，记录工作树中所有文件的当前状态

### 向暂存区中添加文件

想让文件称为git仓库的管理对象，那么我们可以用`git add`命令将其加入暂存区，暂存区是一个临时区域。

```bash
git add .
```

![image-20221126141659103](Git.assets/image-20221126141659103.png)

> 如果想把文件移出暂存区可以使用以下命令
>
> git rm --cached <file>...

### 保存仓库的历史记录

```bash
git commit -m "FirstCommit"
```

可以将暂存区中的文件实际保存到仓库的历史记录中。通过这些记录，我们可以在工作数中复原文件。

其中`-m "FirstCommit"`称作提交信息，是对提交的概述

![image-20221126142452591](Git.assets/image-20221126142452591.png)

如果直接用git commit命令,会启动一个编辑器,在编辑器中记录要提交的信息。

![image-20221126143053687](Git.assets/image-20221126143053687.png)

当前工作树处于刚刚完成提交的状态, 结果显示没有更改

### 查看提交日志

git log可以查看以往仓库中提交的日志

可以查看什么人在什么时候进行了提交或合并,以及操作前后有怎样的差别

![image-20221126143330051](Git.assets/image-20221126143330051.png)

![image-20221126143503655](Git.assets/image-20221126143503655.png)

只显示指定目录或文件的日志

```bash
git log 文件名/目录名
```

显示文件的改动

```bash
git log -p 文件名/目录名
```

### 查看更改前后的差别

git diff

查看工作树、暂存区、最新提交之间的差别。

