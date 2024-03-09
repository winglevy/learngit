



##### git初始

```bash
git config --global user.name "wzt"
git config --global user.email "2318914031@qq.com"
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

***github仓库***

```bash
# 密钥配置
ssh-keygen -t rsa -C "winglevy" # github上名字
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

