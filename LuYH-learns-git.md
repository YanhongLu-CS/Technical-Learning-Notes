# 1.主要命令

| 场景    | 命令                            | 作用             |
| ----- | ----------------------------- | -------------- |
| 初始化仓库 | `git init`                    | 在当前目录创建 Git 仓库 |
| 克隆项目  | `git clone <url>`             | 下载远程仓库到本地      |
| 查看状态  | `git status`                  | 查看文件修改、暂存情况    |
| 查看修改  | `git diff`                    | 查看尚未暂存的改动      |
| 暂存文件  | `git add <file>`              | 把指定文件加入暂存区     |
| 暂存全部  | `git add .`                   | 暂存当前目录下所有修改    |
| 提交代码  | `git commit -m "message"`     | 提交暂存区内容        |
| 查看历史  | `git log`                     | 查看提交记录         |
| 简洁历史  | `git log --oneline`           | 一行显示一个提交       |
| 查看分支  | `git branch`                  | 查看本地分支         |
| 创建分支  | `git branch <name>`           | 新建分支           |
| 切换分支  | `git switch <name>`           | 切换到分支          |
| 创建并切换 | `git switch -c <name>`        | 新建并切换分支        |
| 合并分支  | `git merge <branch>`          | 将指定分支合并到当前分支   |
| 查看远程  | `git remote -v`               | 查看远程仓库地址       |
| 添加远程  | `git remote add <name> <url>` | 添加远程仓库地址       |
| 拉取代码  | `git pull`                    | 获取远程更新并合并      |
| 获取更新  | `git fetch`                   | 获取远程更新，但不自动合并  |
| 推送代码  | `git push`                    | 将本地提交推到远程      |
| 首次推分支 | `git push -u origin <branch>` | 推送并建立远程跟踪关系    |
| 临时保存  | `git stash`                   | 暂存当前未提交的修改     |
| 恢复暂存  | `git stash pop`               | 恢复最近一次 stash   |
| 查看标签  | `git tag`                     | 查看标签           |
| 创建标签  | `git tag v1.0.0`              | 创建版本标签         |
|       |                               |                |

# 2.常见疑问
## 1.初始化仓库并连接远程
建立仓库 `git init`
关联远程 `git remote add <name> <url>`

==第一次执行 `git push -u origin main`==
这里：
```
git push -u origin main
         │   │     │
         │   │     └─ 本地 main 分支
         │   └─────── 远程仓库 origin
         └─────────── 建立 upstream 跟踪关系
```
执行以后，本地main和远程origin/main产生联系：
```
本地 main
    │
    │ tracking
    ↓
origin/main
```
后续可以直接 `git push`和 `git pull`

## 2.什么是暂存(stash)
==stash = 把修改存进临时存档==
==apply = 取出来用，但存档还留着==
==pop   = 取出来用，成功后把存档也删掉==
执行：
```
git stash
```
Git 会做两件事：
```
1. 把未提交修改临时保存起来
2. 工作区恢复到 A
```
“修改内容不见了”，不是被删了，而是被放进 stash 里了。
你可以查看：
```
git stash list
```
之后有两个类似命令：
```
git stash apply
```
和：
```
git stash pop
```
区别是：
```
git stash apply
恢复 stash
但 stash 记录还保留

git stash pop
恢复 stash
并且成功后删除这条 stash
```
## 3.刚commit，发现漏了一个文件，怎么办
先暂存：
`git add <name>`
然后amend：
`git commit --amend -m "message"` or `git commit --amend --no-edit`


