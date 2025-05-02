##### 理解git



1、git的基本设置

创建：git init



2、git保密设置

～～ 在云端账户确认本地密匙后，基本上就相当于可以推送了，如果无法推送可能是ssh问题

ssh：通过本地创建ssh密匙，登陆后需要在云端添加密码

ssh网络端口问题：有密码却无法连接账户进行clone或者push的情形，需要设置.ssh/config使用合适的网络端口

```
# 编辑ssh配置文件
vim ~/.ssh/config

# 在文件中添加以下内容
Host github.com
  Hostname ssh.github.com
  Port 443
  User git
  IdentityFile ~/.ssh/id_rsa  # 替换为你的私钥路径

```



##### 理解Github



1、两步验证：

1）确保设备验证：在新设备上登录需要通过旧设备的验证

2）验证方式：step two软件都可以，不过需要在GitHub云端账户确认使用哪一个物理设备上的authenticator，这个需要登录GitHub账号然后设置

3）还有许多github的其他密码验证方式，基本都是和物理设备进行绑定的



2、两部验证的更改：

涉及到主要使用设备的更改，需要在原设备或者云端账户上进行设置，就比如设置authenticator的账户修改。修改完毕后新设备上的两部验证就可以作为登录时的验证。







##### git初始

```bash
git config --global user.name "wzt"
git config --global user.email "2318914031@qq.com"

# 查看全局用户信息
git config --global --list
```



##### git仓库

***仓库初始化***

```bash
mkdir learngit
cd learngit
git init
```



***本地仓库***

```bash
# 版本管理
```



***github远程仓库***

```bash
# 密钥配置
ssh-keygen -t rsa -C "winglevy" # github上名字

# 云端账户需要添加用户密匙才能确认身份

# 用户密匙添加后仍然无法使用ssh推送，可能是ssh的网络端口使用出了问题，参见上面理解git部分的处理办法
```



```bash
# 远程仓库
git remote -v
git remote add origin git@github.com:michaelliao/learngit.git

# 远程推送(先本地后远程)
git push -u origin master # -u第一次关联起来
git push origin master # 之后

# 每个项目中git init 设置remote都是独立的

# 远程下载(先远程后本地)
git clone git@github.com:michaelliao/gitskills.git
```



##### 版本管理

~~
	工作区，暂存区-chekout，版本库，远程库

```bash
## 文件
cat readme.md
git diff readme.md
git diff HEAD -- readme.txt  # 比较工作区和仓库
git checkout -- readme.txt  # 1未暂存-直接回复上次提交 2暂存-恢复上次暂存后
git rm readme.md && git commit -m "remove readme.md"  # 本地仓库中删除

## 分支
git status

## 历史命令
git log --pretty=oneline # 显示版本号
git log --graph --pretty=oneline --abbrev-commit
git reflog

## 版本切换
git reset --hard HEAD^ # 前一个，往后没有快捷设置
git reset --hard <版本号>

## 存储(覆盖删除)：工作-直接，暂存-add，仓库-commit，远程-push

```



##### 分支管理

~~
	bug, feature
	多人：推送，抓取合并再推送

```bash
# 查看分支
git branch 
# 创建分支：1定义 2切换时
git branch new && git switch/checkout new
git switch -c new# 或 git checkout -b new
# 合并分支
git checkout master && git merge new
# 删除杂支
git branch -d new
```



##### 标签管理

~~
	版本标签代替版本号

```bash
# 标签
git tag v1.0  # 当前标签
git tag v0.9 <commit_number>  # 某次提交标签
git tag -a v0.1 -m "version 0.1 released" 1094adb  # 添加描述信息
git tag -d v0.1
git tag -d v0.9 && git push origin :refs/tags/<v0.9>
# 标签查看
git tag  # 查看标签
git show v0.9  # 查看标记提交
# 标签作用
git push origin v1.0
git push origin --tags  # 全部标签
```

##### git设置

```bash
## 忽略文件 -- 编辑 .gitignore
# Windows:
Thumbs.db
ehthumbs.db
Desktop.ini
# Python:
*.py[cod]
*.so
*.egg
*.egg-info
dist
build
# My configurations:
db.ini
deploy_key_rsa
## 忽略后操作
git add -f App.class  # 强制添加
git check-ignore -v App.class  #查看为什么不能添加

## git别名 -- git配置文件：.git/config
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.ci commit
git config --global alias.br branch
# 彩色，图形，良好数据格式的log
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
```



##### git意外



无法合并分支：
	远程分支名main
	本地直接添加了分支名master，之后直接推送 —— 此时远程有两个分支，本地推送了一个，不匹配
	克隆远程到本地，重新修改在推送
