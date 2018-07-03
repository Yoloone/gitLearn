# Git使用
Git是一个免费开源的分布式版本管理系统

### 工作区和暂存区

- **工作区**（Working directory）：本地当前目录
- **暂存区**（stage）：文件准备提交前的缓存区，`git add`后将文件暂存于此
- **版本库** ：包括暂存区和各种分支，`git commit`后将文件提交到HEAD所指向的分支

###创建版本库
- 版本库即Repository（仓库），Git管理该目录下的所有文件
- 使用`git init`初始化仓库，得到一个空仓库
- 该目录下将出现`.git`目录，该目录是版本库，用于跟踪仓库变动
###添加文件
- `git add 文件名`，添加文件到暂存区，可一次添加多个文件
- `git commit -m '提交说明'`，提交文件到本地仓库
- Git只能跟踪文本文件的变动，无法判断图片、视频、word等二进制文件的改动
### 删除文件

- `git rm 文件名`，`git commit -m '提交说明'`，删除版本库的文件

### 提交修改
- 提交修改的操作同添加文件
- `git status`，查看工作区的状态，与本地仓库的区别（是否存在未提交的修改）
- `git diff 文件名`，查看某一文件的改动
### 版本回退
- `git log`，查看commit历史记录
- `git reset --hard HEAD^`，回退到上个版本，其中HEAD代表当前版本，HEAD^代表上个版本，HEAD^^代表上上个版本，用于回到过去
- `git reset --hard commitID`，回退到指定commitID对应的版本，常用于回到未来
- `git reflog`，查看版本操作命令的历史记录，可查看命令对应的版本号
### 撤销修改

- `git checkout -- 文件名`，将工作区修改恢复至最近一次git add 或 git commit的状态
- `git reset HEAD 文件名`，撤销暂存区的修改，把修改重新放回工作区

场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令`git checkout -- 文件名`。

场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令`git reset HEAD 文件名`，就回到了场景1，第二步按场景1操作。

场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考[版本回退]一节，不过前提是没有推送到远程库。

### 远程仓库

- 设置远程关联许可
  - `$ ssh-keygen -t rsa -C "youremail@example.com"`，获取SSH key
  - 登录Github，复制*id_rsa.pub* 的内容， 添加SSH key
- 本地项目关联远程仓库
  - `git remote add origin git@server-name:path/repo-name.git `，本地库关联至远程库，origin是远程库名，可更改
  - `git push -u origin master `， 第一次推送，将本地库master分支内容推送至远程库master分支，`-u`参数将本地master分支与远程master分支关联起来
  - `git push origin master`，推送最新修改
- 克隆远程仓库项目
  - `git clone git@server-name:path/repo-name.git `，克隆项目到本地

