# GIT BRANCH RULES

> branch 命名: 
--------------------------------------------------

```
  ex: 类型_需求版本_月日
  branch name: feat_moviev1_0708  // 新功能_电影项目第一期需求_分支生成日期
```
  
  类型: 
  *  feat     功能
  *  release  发布分支
  *  fix      bug 修复分支
  *  test     测试分支


> TAG: 
--------------------------------------------------

```
git tag -a tagName -m "my tag" 
```

当有重大版本更新上线完毕后打上tag标记，备注信息标上本次分支包含的需求版本，注意事项

> git cherry-pick 
--------------------------------------------------

* 一种情况是，你需要另一个分支的所有代码变动，那么就采用合并（git merge）。
* 另一种情况是，你只需要部分代码变动（某几个提交），这时可以采用 Cherry pick。

![cherry-pick](https://www.wangbase.com/blogimg/asset/202004/bg2020042723.jpg "cherry-pick")

* 单个commit转移

```
// git cherry-pick <commitHash>

git checkout feat_moviev1_0708  // 切到feat_moviev1_0708

git log                         // 获取想要合并的commit hash ex: c1bc1f1b1

git checkout master             // 切到目标分支

 git cherry-pick c1bc1f1b1      // 将c1bc1f1b1 合并到目标分支

```

* 多个commit转移

```
 git cherry-pick A..B   // 转移从 A 到 B 的所有提交
                        // 提交 A 必须早于提交 B，否则命令将失败，但不会报错
                        // 提交 A 将不会包含在 Cherry pick中

 git cherry-pick A^..B  // 包含提交 A

```

* 代码冲突

```
git cherry-pick --continue  // 解决代码冲突后，第一步将修改的文件重新加入暂存区（git add .），第二步使用下面的命令，让 Cherry pick 过程继续执行

git cherry-pick --abort     // 放弃合并，回到操作前

git cherry-pick --quit      // 放弃合并，不回到操作前
```

* 转移到另一个代码库

```
 git remote add target git://gitUrl  // 添加远程仓库

 git fetch target                    // 将远程代码抓取到本地

 git log target/master               // 获取commit hash

 git cherry-pick <commitHash>        // 使用git cherry-pick命令转移提交
```


* [cherry-pick](http://www.ruanyifeng.com/blog/2020/04/git-cherry-pick.html)