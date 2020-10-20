[toc]



#### 初始化git本地库

```bash
git init   # Initialized empty Git repository in path

ls -la     # 显示隐藏目录.git/;该目录存放的是本地库相关的子目录和文件 
```

#### 设置签名

- 形式

  * 用户名：
  * Emai地址：

- 作用：**区分不同开发人员的身份**

- 命令：

  * 项目级别/仓库级别：仅在当前本地库范围内有效

  ```bash
  git config user.name xxx
  git config user.email xxx
  ```

  

  * 系统用户级别：登录当前操作系统的用户范围

  ```bash
  git config --global user.name xxx
  git config --global user.email xxx
  ```

  

  * 级别优先级：
    * 就近原则：项目级别优先于系统用户级别，二者都有时采用项目级别的签名
    * 如果只有系统用户级别，就以系统用户级别签名为准
    * 二者都没有不允许
  * 签名信息保存在 .git/config 目录

  ```bash
  cat .gitconfig #查看签名信息
  ```

#### 添加提交及查看状态操作

```bash
git status #查看工作区和暂存区状态

git add  file/folder #提交到缓存区后退

git rm --cached file/folder #从暂存区撤销

git commit file/folder #进入 "提交说明" 编辑器
#或者
git commit -m "提交说明" file/folder
```

#### 查看版本记录

```bash
git log

git log --pretty=oneline #以更简洁的方式查看版本记录

git log --oneline         #更更简洁

git reflog                #更更简洁 + 信息丰富

```

#### 控制版本前进后退

* 基于索引值

```bash
git reset --hard [局部索引值]    #索引值即哈希值

```



* 使用^符号：只能后退
* 使用~符号：只能后退

```bash
git reset --hard HEAD^ # 后退一个版本
git reset --hard HEAD^^^^  #后退四个版本
git reser --hard HEAD~n  #后退n步
```

* reset命令的三个参数

```bash
--soft  :1. 仅仅在本地库移动HEAD指针 
--mixed ：1.在本地库移动HEAD指针 2.重置暂存区
--hard ： 1.在本地移动暂存区 2.重置暂存区 3.重置工作区
```

#### 比较文件差异

```bash
git diff file/folder      #指修改过的文件与本地库文件进行比较，会出结果；但把修改过的文件提交到暂存区                           后则没有区别，这时是修改过的文件与暂存区进行比较，
git diff HEAD^ file/folder #这是暂存区与本地库之前的版本进行比较

```

#### 分支管理

* 分支:在版本控制过程中，使用多条线同时推进多个任务
* 好处：
  * 同时并行推进多个功能开发，提高开发效率
  * 各个分支在开发过程中，如果某一个分支开发失败，不会对其他分支有任何影响
* 命令

```bash
git branch -v #查看当前分支
git branch [新的分支名] #创建新的分支
git checkout [已存在的分支名] #切换分支
```

* 合并分支

  * 第一步：切换到接受修改的分支（被合并，增加新内容）上
  * 第二部：执行merge命令

  ```bash
  git merge [要合并过来的分支]
  ```

* 解决冲突

  * 第一步：编辑文件，删除特殊符号

  * 第二步：把文件修改到满意程度，保存退出

  * 第三步：git add [文件名]

  * 第四步：git commit -m "日志信息"

    *注意：此时 commit 一定不能带具体文件名

#### 在本地创建远程库地址别名

```bash
git remote -v #查看已存在的远程库地址别名
git remote add origin [github远程库地址链接] #给远程库取个origin的别名
```

#### 推送和克隆操作

```bash
git push origin master #推送
git clone [远程库地址]  #克隆远程库

#pull操作抓取
fetch + merge = pull # fetch和pull都是读取操作，不修改 
git fetch origin master #抓取远程库origin的master分支  ，不会对工作区的相同名称文件进行修改
git checkout origin/master  #切换到远程库master分支
#推荐先fetch后merge，之后push
```

#### SSH登录

* cd~,先回到家目录

```bash
ssh-keygen -t rsa -C [邮箱地址]#系统会自动生成ssh key
cd .ssh/#切换到ssh目录
cat id_rsa.pub #查看密钥
 
 #将密钥复制到github

git remote add [远程库别名] [远程库ssh形式链接] #创建免密登录远程库别名
git push [远程库ssh类型的别名] master


```

