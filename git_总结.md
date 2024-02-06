

##### 0 git功能



##### git初始化

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
# 远程下载(先远程后本地)
git clone git@github.com:michaelliao/gitskills.git
```

~
	https://www.liaoxuefeng.com/wiki/896043488029600/897013573512192

##### 版本管理

```bash

```



##### 分支管理



##### 标签管理



