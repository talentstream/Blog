---
title: github工作流
date: 2022-11-16 13:37:35
---

视频链接： [十分钟学会正确的github工作流，和开源作者们使用同一套流程](https://www.bilibili.com/video/BV19e4y1q7JJ/?share_source=copy_web&vd_source=8277fbbcfe9cfbff0708d41552ef71ab)

#### 步骤

```
1. git clone https://github.com/example/example.git 
// 克隆远程项目到本地 git clone + "github项目提供的http"
2. git checkout -b my-feature 
// 修改代码,建立新分支而不是直接往main上push代码
// "my-feature" 是这个分支的名字
// 这个命令会复制一份当前的breach到新breach
3. git diff 
// 当修改代码后,用 git diff 查看自己对代码做出的改变
4. git add <changed_file>
// 把已修改的代码告知 git ，这样 git 就可以 commit 了
5. git commit "comment(可有可无)"
// 把修改放入git中
6. git push origin my-feature
// 将当前 git 新创建的 breach 推回给github

----------------------
（当修改代码的时候发现github出现改变 , 假设是main）
1. git checkout main
// 切换回main分支
2. git pull origin master(main)
// 这样 github 的 main 就会同步到 git 的 main
3. git checkout my-feature
// 回到 my-feature
4. git rebase main
// 同步修改，先不管自己的修改，然后把 main 先放进这个分支，最后根据我的修改成新的内容
// 中途可能会出现rebase conflict，手动选择要哪一段代码
5. git push -f origin my-feature 
// 将 git 变化的分支放进github

6. github 上  (请求)pull request -> (主人)Squash and merge
// 在github中将两个分支合到mainbranch

7. 然后删掉第二个分支（如果没用的话）

8. git branch -D my-feature
// 删除 git 的分支

9. git pull origin master(main)
// git 更新 github的最新代码
```