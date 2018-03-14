# GIT提交代码到远程库

```bash
1.从已有的分支创建新的分支(如从master分支),创建一个dev分支
git checkout -b dev
相当于 $ git branch dev
$ git checkout dev两条命令

2.创建完可以查看一下,分支已经切换到dev
git branch

3.提交该分支到远程仓库
git push origin dev

4.测试从远程获取dev
git pull origin dev
或者：如果用命令行，运行 git fetch，可以将远程分支信息获取到本地，再运行 git checkout -b local-branchname
 origin/remote_branchname  就可以将远程分支映射到本地命名为local -branchname的一分支

5.我觉得现在重要的就是设置git push,pull默认的提交获取分支,这样就很方便的使用git push 提交信息或git pull获取信息

git branch --set-upstream-to=origin/dev

取消对master的跟踪git branch --unset-upstream master

6.现在随便修改一下工程文件的内容,然后git commit ,git push,之后就可以直接提交到远程的dev分支中,而不会是master
```

```bash
$ git checkout issue1
Switched to branch 'issue1'
```

#### 删除标签

```bash
git branch -d iss53
```
#### 遇到冲突时的分之合并

```
# 查看具体冲突信息
$ git status
```

### 保持分支与master sync

you just do

```
git checkout master
git pull
git checkout mobiledevicesupport
git merge master
```

to keep mobiledevicesupport in sync with master

then when you're ready to put mobiledevicesupport into master, first merge in master like above, then ...

```
git checkout master
git merge mobiledevicesupport
git push origin master
```
