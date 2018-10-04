# git cheat sheet

---

## 常用命令

- `git init`: 初始化一个本地仓库
- `git status`: 查看仓库当前的状态，重度使用命令！
- `git add <file>...`: 添加到暂存区（stage）
	- `git add .`: 添加包括文件内容修改（modified）以及新文件（new），也包括被删除的文件？
	- `git add -u`: git add --update 的缩写；添加已被追踪的文件（即 tracked file），不会提交新文件（untracked file）
	- `git add -A`: git add --all 的缩写；是上面两个功能的合集
- `git commit -m "commet"`: 将缓存区的所有文件提交到本地仓库，commet 为提交信息
- `git commit -m "commet" -m "description"`: 提交信息带上详细描述 description（或者可以直接执行 git commit，然后 vim 编辑器会打开，填写提交信息 commet 后，空一行后就可以继续填写详细描述 description 了）
- `git commit --amend`: 这个命令会将暂存区中的文件提交。 如果自上次提交以来你还未做任何修改（例如，在上次提交后马上执行了此命令），那么快照会保持不变，而你所修改的只是提交信息。最终你只会有一个提交，第二次提交将代替第一次提交的结果。
- `git diff`: 顾名思义就是查看 difference
	- `git diff [file]`: 工作区和暂存区的比较
	- `git diff --cached [file]`: 暂存区和版本库最新版本的比较
	- `git diff HEAD [file]`: 工作区和版本库最新版本的比较
- `git log`: 查看提交历史
- `git log --pretty=oneline`: oneline 查看 log
- `git reflog`: 查看命令历史
- `git reset [mode] [commit]`
	- `mode 参数`
		- `--soft`: 还原 HEAD，已经 add 的缓存以及工作区的所有东西都不变。此时 HEAD != Index = Working Directory
		- `--mixed(default)`: 还原 HEAD、Index，已经 add 的缓存也丢掉，工作区的代码不变。此时 HEAD = Index ！= Working Directory
		- `--hard`: 还原 HEAD、Index、Working Directory，一切就全都恢复，本地代码全部还原。此时 HEAD = Index = Working Directory
	- `git reset [mode] HEAD^`: 回退到上一个版本（HEAD 表示当前版本，上一个版本就是 HEAD^，上上一个版本就是 HEAD^^，往上 100 个版本 HEAD~100）
	- `git reset [mode] commit_id`: 回退到一个具体版本（commit_id 版本号没必要写全，前几位就可以了，git 会自动去找)
	- `git reset --hard = git reset --hard HEAD`: 彻底丢掉本地修改但是不更改 branch 所指向的 commit
	- `git reset HEAD <file>...`: 把暂存区的修改撤销掉（unstage），重新放回工作区
- `git checkout -- <file>...`: 丢弃工作区的修改！
- `git rm <file>...`: 删除文件
- `git remote -v`: 查看远程主机信息
- `git remote show <主机名>`: 查看该主机的详细信息
- `git remote add origin git@server-name:path/repo-name.git`: 关联一个远程库
- `git pull`: 拉取远程库最新代码（if no tracking information，则说明本地分支和远程分支的链接关系没有创建 -> `git branch --set-upstream local_branch_name origin/remote_branch_name`）
- `git push -u origin branch_name`: 第一次推送 branch_name 分支的所有内容（本地新建分支，远程仓库并没有该新分支）。-u 参数的作用如下：
	- 创建远程新分支 branch_name
	- 将本地新分支与远程新分支建立联系
	- push 新分支上的文件到远程新分支
- `git push origin branch_name`: 推送最新修改
- `git push origin local_branch_name:remote_branch_name`: local_branch_name 必须为你本地存在的分支，remote_branch_name 为远程分支，如果 remote_branch_name 不存在则会自动创建分支。注意，local_branch_name 不填的话则代表删除远程 remote_branch_name 分支
- `git clone git@github.com:user-name/repo-name.git`: 从远程库克隆
- `git branch`: 查看本地分支
- `git branch -r`: 查看远程分支
- `git branch -a`: 查看所有分支
- `git branch -vv`: 查看分支追踪对应情况
- `git branch -d branch_name`: 删除 branch_name 分支
- `git checkout -b branch_name` <=> `git branch branch_name & git checkout branch_name`: 创建并切换到 branch_name 分支
- `git checkout -b branch_name origin/remote_branch_name`: 在 origin/remote_branch_name 的基础上，创建一个新分支 branch_name
- `git checkout branch_name`: 切换到 branch_name 分支
- `git checkout source_branch_name <file>...`: 指定 source_branch_name 分支的某文件强行覆盖到当前分支的对应文件
- `git merge source_branch_name`: 把 source_branch_name 分支的工作成果合并到当前分支
- `git merge --no-ff -m "merge with no-ff" source_branch_name`: 禁用 Fast forward
- `git stash`: 把当前工作区的所有改变储藏起来
- `git stash list`: 查看 stash 内容
- `git stash pop` <=> `git stash apply & git stash drop`: 恢复成功的同时会把最顶的一个 stash 删掉
- `git stash clear`: 删除所有 stash
- `git tag <tag_name>`: 打一个新标签，默认为 HEAD，也可以在最后指定一个 commit_id
- `git tag`: 查看所有标签
- `git show-ref --tag`: 查看所有远程标签
- `git show <tag_name>`: 查看标签信息
- `git push origin <tag_name>`: 推送标签到远程仓库
- `git push origin --tags`: 一次性推送全部尚未推送到远程的本地标签
- `git tag -d <tag_name>`: 删除一个本地标签
- `git push origin :refs/tags/<tag_name>` <=> `git push --delete origin <tag_name>`: 删除一个远程标签
- `git config --global alias.st status`: 配置命令别名 -> st 表示 status

## note

1. -- 的名称叫做 `double dash`(--)，是 bash 的内置命令，用来标记可选命令选项的结束。即在它后面的带 -- 的字符串，不被当做是一个命令选项。
2. Pushing a branch, tag, or other ref to a remote repository involves specifying "push where, what source, what destination?"
	> `git push where-to-push source-ref:destination-ref`

## Reference

- [git - 简明指南](http://rogerdudler.github.io/git-guide/index.zh.html)
- [廖雪峰 Git 教程](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)
- [Git 菜鸟教程](http://www.runoob.com/git/git-tutorial.html)
- [windows 配置 Git 开发环境](https://xbc.me/install-git-on-windows/)
- [An Intro to Git and GitHub for Beginners](http://product.hubspot.com/blog/git-and-github-tutorial-for-beginners)
- [Become a git guru](https://www.atlassian.com/git/tutorials/what-is-version-control)
- [如何克服解决 Git 冲突的恐惧症](https://www.zhihu.com/question/27507789)
- [Git 远程操作详解](http://www.ruanyifeng.com/blog/2014/06/git_remote.html)
