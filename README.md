[**MYSQL安装 Manual**](https://blog.csdn.net/weixin_47406082/article/details/131867849?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522171660092916800197070475%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=171660092916800197070475&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-2-131867849-null-null.142^v100^pc_search_result_base5&utm_term=mysql%E5%AE%89%E8%A3%85&spm=1018.2226.3001.4187)

[**MySQL实现局域网访问**](https://blog.csdn.net/m0_67906358/article/details/131985937)
```bash
# 在ubuntu中还要进行如下前置操作
sudo vim /etc/mysql/mysql.cnf
sudo systemctl restart mysql

[mysqld]
bind-address = 0.0.0.0

```
[**PostgreSQL安装**](https://github.com/liyinred/Conda/blob/main/postgres.md)

[**右键cmd**](https://blog.csdn.net/qq_46068864/article/details/122884290)

[**PowerShell权限**](https://blog.csdn.net/weixin_41194129/article/details/140538410)

```bash
# 克隆仓库
git config --global http.proxy http://127.0.0.1:7890

git config --global https.proxy http://127.0.0.1:7890

git clone https://github.com/liyinred/ccyy.git

# 进入仓库目录
cd ccyy

# 初始化本地Git仓库
git init

git checkout -b add_lwh

# 配置Git用户信息
git config --global user.name "你的用户名"
git config --global user.email "你的邮箱地址"

# 拉取最新更改
git pull origin main   # 如果主分支是main

# 添加当前目录下所有文件到Git暂存区
git add .

# 提交更改到本地仓库
git commit -m "$(date) Commit"

# 连接到GitHub仓库，这里需要替换成你自己的GitHub仓库URL
git remote add origin https://github.com/你的用户名/你的仓库名.git

# 推送到GitHub，默认推送到master分支，如果是main分支则需修改为main
git push -u origin main

# 将本地的master分支 push 到remote中的 Wenhao 分支中
git push origin master:Wenhao

git push --force origin main  # 慎用!!!
```
你遇到的错误是由于远程仓库包含本地仓库没有的更新，导致推送被拒绝。这种情况通常发生在其他人已经向远程仓库推送了他们的更改，而你的本地仓库还没有这些更改。为了避免覆盖别人的工作，Git 阻止了你的推送操作。

解决这个问题的步骤如下：

拉取远程更改:
首先，你需要将远程仓库中的最新更改拉取到你的本地仓库中。使用以下命令：

```bash
git pull origin main

#放弃所有本地更改
git reset --hard HEAD

git fetch origin
git merge origin/main

git push origin main

git clean -n
git clean -f
```

另外一种方法是使用```git pull --rebase```命令，这样可以避免在历史记录中生成额外的合并提交：

```bash
git pull --rebase origin main

git push origin main
```
error: Your local changes to the following files would be overwritten by merge

```bash
git stash  # 暂存本地更改

git pull origin main

git stash pop  # 恢复暂存的更改：在pull操作完成后，恢复暂存的更改。
```

Git保存所有的提交，包括已经删除的分支上的提交。你可以使用以下命令找到丢失的提交：
```bash
## Git保存所有的提交，包括已经删除的分支上的提交。
git reflog

# 恢复到指定的提交
git checkout 668c50f

# 创建一个新分支保存恢复的数据
git checkout -b restore_branch

# 合并恢复的数据到主分支
git checkout main
git merge restore_branch

# 删除临时恢复的分支
git branch -d restore_branch
```
### Git_change_commit_email
```bash
git filter-branch -f --env-filter '
OLD_EMAIL="ubuntu@localhost.localdomain"
CORRECT_NAME="wenhao-pc"
CORRECT_EMAIL="liyinred@foxmail.com"
if [ "$GIT_COMMITTER_EMAIL" = "$OLD_EMAIL" ]
then
    export GIT_COMMITTER_NAME="$CORRECT_NAME"
    export GIT_COMMITTER_EMAIL="$CORRECT_EMAIL"
fi
if [ "$GIT_AUTHOR_EMAIL" = "$OLD_EMAIL" ]
then
    export GIT_AUTHOR_NAME="$CORRECT_NAME"
    export GIT_AUTHOR_EMAIL="$CORRECT_EMAIL"
fi
' --tag-name-filter cat -- --branches --tags
```
