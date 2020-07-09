> git rebase
--------------------------------------------------

* 基于远程分支"origin"，创建一个叫"mywork"的分支

```
git checkout -b mywork origin  // 新分支

vim file.txt                   // 开发改动

git commit                     // 提交

git rebase origin
```
![rebase](http://gitbook.liuhui998.com/assets/images/figure/rebase3.png "rebase")

* 会把你的"mywork"分支里的每个提交(commit)取消掉，并且把它们临时 保存为补丁(patch)(这些补丁放到".git/rebase"目录中),然后把"mywork"分支更新 到最新的"origin"分支，最后把保存的这些补丁应用到"mywork"分支上

![rebase](http://gitbook.liuhui998.com/assets/images/figure/rebase4.png "rebase")

* 详细说明[rebase](http://gitbook.liuhui998.com/4_2.html)