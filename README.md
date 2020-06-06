 

# git

## 1.git简介

### 1.1 谁创建了git，为了什么？

- `linux`的创始人在壮大`linux`的时候需要收到各地上传的代码，需要版本控制系统，最初有公司免费支持。后来社区有人试图破解别人的系统，公司停用要求破解者道歉。然后大牛拒绝道歉，就自己写了个源码管理，就是现在的`git`。
- 总结：牛逼的人就是牛逼

### 1.2 git是什么？

- 分布式版本管理系统
  - 分布式：就是不管你身在何地，都可以通过计算机使用`git`管理你的文件
  - 版本：我们在开发的时候，会有不同的版本。（就像你写一篇文章、初稿、检查、润色，每一步都是一个版本）
  - 管理系统：就是一个管理工具

![](C:\Users\Administrator\Desktop\git学习\imgs\版本控制.png)

### 1.3 git的特点

- 版本控制：支持多人同时开发代码，解决找回历史代码的问题。（可以使用git快乐多人运动，并且不用担心因为版本更新出现问题无法找到历史代码产生问题）
- 分布式：可以存储在一个仓库中，然后多台计算机可以同时在各个地方进行开发操作。
- 史上最大的同性交友网站：GitHub（技术就是用的人越多，就会发现更多的问题，然后修复后变得更加强大）



## 2.安装配置

### 2.1 安装配置

- 在`linux/ubuntu`上安装

  ```
  sudo apt-get install git
  ```

- 在`windows`上安装

  - 推荐使用国内源 https://npm.taobao.org/mirrors/git-for-windows/
  - 找到一个简易的安装版本 `Git-2.25.0.rc2.windows.1-64-bit.exe   `(个人使用的是带`exe`后缀的版本)
  - 简单操作，直接重复点击下一步，直至安装完毕。

- 检查`git`是否安装好
  - ``linux/ubuntu``上直接使用命令`git`查看
  - `windows`点击右键，看是否出现了两个关于`git`的操作命令

### 2.2 配置仓库

- 指定管理的目录

  - ``linux/ubuntu``上直接在需要管理的文件夹下使用终端输入初始化命令
  - `windows`上在需要管理的目录下点击右键，然后点`git bash here`输入初始化命令
  
  ```
  git init # 初始化命令
  ```

- 隐藏文件`.git`
  - 里面存储了大量关键信息，**请勿轻易修改或者删除**。

### 2.3 了解工作区

- 工作区是指我们刚才指定管理目录下的区域，管理目录下的所有文件。
- 文件的状态分为两种：
  - 已管理，没有修改并非新增的文件。（**我习惯性的用一个非专业词汇工作区静态文件表示**）
  - 已修改或者新增的文件。（`modified`）

![](C:\Users\Administrator\Desktop\git学习\imgs\工作区.png)

## 3.git简单的操作

### 3.1 创建第一个文件并且提交到版本库

- **第一次提交时：**进行全局邮箱配置，否则会在提交版本库的时候报错。	

```
git add 文件名 # 提交指定的文件到暂存区
git add . # 提交所有`modified`状态文件到暂存区
git config --global user.email 配置邮箱
git config --global user.name 配置用户名
git commit -m '版本信息' # 提交暂存区的文件到版本库
```

### 3.2 检测|检查

```
git status # 检测文件状态
git log # 查看当前日志记录
git reflog # 查看所有的日志记录
```

### 3.3 更新版本库

- 有了第一个版本之后，我们后续的操作是在第一个版本的基础上进行改动。
- 我们增加或修改的东西，会在当前版本的基础下记录下来，提交到版本库生成新的版本。
- 新版本只会记录改动|新增部分，另外会生成一个指针指向上一个版本的地方。（这个指针是我理解`git`抽象出来的，具体待考证！）

```
修改文件
git add . # 提交所有的修改到暂存区
git commit -m '版本信息' # 提交暂存区内容到版本库，生成新的版本
```

### 3.4 对比文件的不同

- 工作区与版本库相同的文件对比

  ```
  git diff HEAD -- 文件
  # 显示信息用`+ -`区别各自独有内容
  # `+`表示工作区文件独有内容
  # `-`表示HEAD（当前使用版本）独有内容
  ```

- 版本库之间相同文件的比较

  ```
  git diff HEAD HEAD~2 -- 文件 # 比较当前版本与前两个版本之间的区别
  # `+`当前版本的独有内容
  # `-`表示前两个版本独有的内容
  ```



## 4.git三大区域

### 4.1 工作区

- 参考`2.3`处内容
- 日常本地用于开发，可见的区域。（一般是指我们进行`git`管理的文件夹）

### 4.2 暂存区

- 介于工作区与版本库之间的缓冲区

### 4.3 版本库

- 保留所有已提交的版本

### 4.5 三大区域日常操作

- 工作区进行日常开发
- 开发完成后添加至暂存区
- 暂存区提交到版本库
- 同时三个区域也可以进行回滚操作

![](C:\Users\Administrator\Desktop\git学习\imgs\7.png)



## 5.回滚操作

### 5.1 从工作区动态到工作区静态

```
git checkout
```

### 5.2 从暂存区回滚到工作区的动态

```
git reset HEAD
```

### 5.3 从版本库回滚到暂存区

```
git reset --soft 版本号
```

### 5.4 从版本库回滚到工作区动态

```
git reset --mix 版本号
```

### 5.5 从版本库回滚到工作区静态

```
git reset --hard 版本号
```

### 5.6 版本号怎么查？

```
git reflog # 查询版本信息
# 结果开头部分就是版本号
```



## 6.分支

### 6.1 什么是分支？

- 我们的提交的新版本，会在之前版本基础上仅保存改动（新增|修改|删除）了的部分内容。
- 这些版本可以抽象成串在一条线上，我们一般把这个成为主支。（`master`是主支的默认名）
- 而在某一个版本上，我们创建一个新的支线进行其他开发处理，就叫做分支。
- **形象的说明：**工厂有一条主流水线，我们在某个节点可以拿主干线的东西到其他的分流水线进行工作，工作完毕后将东西放回主流水线。

![](C:\Users\Administrator\Desktop\git学习\imgs\6.png)

### 6.2 分支的特点

- 隔离环境，避免开发流程对主干线产生不必要的污染。
- 分工协作，每个分支进行不同的工作，提高效率。

### 6.3 分支的基本操作

- 查看当前的分支

  ```
  git branch
  ```

- 创建分支

  ```
  git branch <name>
  ```

- 切换分支

  ```
  git checkout <name>
  ```

- 快速创建并切换到分支

  ```
  git checkout -b <name>
  ```

- 删除分支

  ```
  git branch -d <name>
  ```

### 6.4 合并分支

- 合并分支:将两条支线的内容进行合并，并且生成新的版本。

  ```
  git checkout <name> # 切换到要进行合并的分支
  git merge <name1> # 将<name1>合并到<name>上
  ```

### 6.5 分支冲突

- 两个分支对相同文件相同位置进行了不同的操作，提交到版本库，然后进行合并的时候系统无法判断保留哪一个修改。

- 实际开发中，每个部门或者不同的人在分支上进行操作会产生分支冲突。这个时候需要我们与产生分支冲突的协作对象商量，并手动解决分支冲突。

### 6.6 解决分支冲突

- 找到产生冲突的分支管理者，进行协商手动编写更改冲突，重新提交新的版本。

  ```
  git log --graph 查看带有分支示意图的日志
  ```

- 有时候合并分支不会成功，但是它也不会产生冲突。

- 我们可以禁用`fast-forward`禁用快速合并进行提交

  ```
  git merge --no--ff -m '版本信息' # 禁用快速提交
  ```

### 6.7 保存工作状态

- 当我们编辑一半的时候，需要切换到其他分支工作，需要保存当前工作状态，以便切换回来之后继续工作。

  ```
  git stash # 保存工作状态
  git stash list # 获取保存的工作状态
  git stash pop # 恢复工作现场
  ```

  

## 7.GitHub

### 7.1 GitHub的作用

- 充当最大的同性交友平台
- 充当一个分布式的中央服务器（我们之前的版本都是保存在本地）
- 多台计算器可以通过中央服务器，进行代码的交换。

### 7.2 如何使用`github`

- 注册登录账号

- 创建仓库

- 添加`ssh`仓库

  - 在电脑中生成`SSHKey`

    ```
    ssh-keygen -t ras -C "注册邮箱"
    ```

  - 到`user/adminstor`中找到文件`.ssh/`下的`id_rsa.pub`
  - 复制文件下的内容，粘贴到`github`的`ssh`配置中

### 7.3 推送本地项目到`github`

- 推送时，若远程仓库不为空仓库时

  ```
  git pull --rabse origin master # 合并远程仓库与本地库
  ```

- 一般推送

  ```
  # 将我们的远程地址加一个别名
  git remote add origin https://xxxx
  # 从本地推送到远端仓库地址
  git push -u origin 需要推送的分支名称
  -u # 默认提交到origin地址的指定分支
  # 不使用-u就是手动指定
  ```

### 7.4 下载远程仓库项目到本地

- 克隆代码

  ```
  # 克隆代码（第一次本地没有需要拉取的代码）
  git clone https://xxxxxx （内部已经实现了 别名添加）
  ```

- 更新代码

  ```
  # 更新代码
  git pull origin dev
  # 上面更新代码相当于下面两句
  git fetch origin dev
  git merge orgin/dev
  ```

- 克隆出错时，可尝试下列代码

  ```
  eval "$(ssh-agent -s)"
  ssh-add
  ```

### 7.5 上传分支

```
git push origin 分支名称
```

### 7.6 本地分支跟踪远程

```
git branch --set-upstream-to=origin/远程分支 本地分支
```

### 7.7 从远程分支拉取代码

```
git pull origin 分支名
```





 