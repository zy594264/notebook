## git使用

**1. 设置git全局用户名和邮箱**

```git
git config --global user.name "your name" #设置用户名
git config --global user.email "xxxx@email.com" #设置邮箱
```

**2. 创建空目录（用于放置仓库）**

```git
mkdir zygit #创建目录
cd zygit #进入目录
```

**3. 初始化git仓库（使目录变为git能够管理的仓库）**

```git
git init #初始化仓库
```

**4. 仓库里创建文件，准备提交**

**5.提交文件到暂存区**

```
git add readme.md #提交readme.md文件到仓库暂存区，add命令可以多次暂存多个文件，等待commit命令一次全部提交
```

**6.提交文件到仓库**

```
git commit -m “描述文字” #每次提交尽量写好描述文字，commit命令一次可以提交多个文件
```

> commit可以⼀次提交很多⽂件，
> 所以你可以多次add不同的⽂件，⽐如：
> $ git add file1.txt
> $ git add file2.txt
> $ git add file3.txt
> $ git commit -m "add 3 files."

**7.查看git仓库状态**

```
git status #查看git仓库状态
```

**8.查看文件修改（变更）内容**

```
git diff file.txt
```

**9. 查看git历史记录（日志文件）**

```
git log #查看git日志文件
git log --pretty=oneline #参数pretty等于online时，日志文件一行显示
# 单行log有两部分：前面为commit id， 后面为提交的描述文字
```

> log日志模式下按Q退出

------

> git 中使用HEAD代表当前版本， HEAD^表示上一个版本， HEAD^^表示上上个版本， 往上版本多的时候使用‘HEAD~数字’表示

**10. 回滚到上一个版本**

```
git reset --hard HEAD^ #回滚到上一个版本
# --hard  强制返回到某次提交前的源码状态
```

> 但是hard强制回滚的话，想找回之前版本未commit的文件：
>
> **1**.如果通过git add命令追踪过这些文件，只是没有commit它们
>
> **2**.使用`git fsck --lost-found `命令
>
> **3**.之后可以在本地项目文件路径`.git/lost-found/other`中找到之前版本的文件，可以直接复制次目录的文件，更改名字与后缀名后，即为之前版本文件
>
> **4**.再通过`find .git/objects -type f | xargs ls -lt | sed 100q`这个命令，可以找到最近add到仓库的100个文件

**11.回滚到制定版本**

```
reset --hard xxxxxx #hard后面可以加参数HEAD或者commit id前六位回滚到制定版本
```

> `git reflog`命令查看提交记录列表(历史日志)  

> **使用git的时候，尽量多进行commit操作，否则版本回滚的时候，未commit的修改，再想找回来很麻烦**

**11.查看工作区与仓库里最新版本的区别**

```
git diff HEAD -- file.txt #查看最新版本与工作区文件的不同
```

**12.撤销工作区的所有修改**

```
git checkout -- file.txt # 撤销工作区的修改，让文件回到最后一次add或commit时的状态
```

**13.撤销暂存区的修改**

```
git reset HEAD file.txt # 把暂存区的修改，回退到工作区。再用checkout撤销工作区修改
```

**14.删除文件**

```
rm file.txt #删除本地文件
git rm file.txt #删除git仓库文件
git commit -m "描述文字" # 提交删除操作
```



**15.连接远程仓库**

1. 创建自己的SSH Key

   - ```
     ssh-keygen -t rsa -C "email@email.com" #后面是自己的邮箱
     ```

2. 在用户主目录下面的.ssh目录下有两个文件

   - id_rsa为私钥，id_rsa.pub是公钥

3. 登录github ，打开个人的 settings > SSH and GPG Keys页面

   - 右侧点击New SSH Key按钮添加SSH key， title随意写，下面粘贴进自己的公钥即可。

**16.推送文件到远程仓库**

1. 将本地仓库与远程新建的仓库相关联

   - ```
     git remote add origin git@github.com:username/new-git.git # 将本地仓库与远程仓库相关联起来
     ```

2. 推送内容到远程仓库

   - ```
     git push -u origin master #将master分支推送到远端
     # 由于远程库是空的,我们第一次推送master分支时,加上了 -u 参数,Git不但会把本地的master分支内容推送到远程新的master分支,还会把本地的master分支和远程的master分支关联起来,在以后的推送或者拉取时就可以简化命令git push origin master/git push
     ```

3. 设置推送到远程仓库不需要输入账号密码

   - > **git config  credential.helper store** #生成git-credentials文件保存账号密码

17.从远程仓库克隆一个本地库**

```
git clone git@github.com:username/git.git #克隆的地址，在github仓库页右上角有。
```

## git分支的管理和使用

**18.创建与合并分支**

