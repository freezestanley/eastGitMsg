# GIT MESSAGE RULES

> git commit msg 规范
--------------------------------------------------

*  feat     新功能（feature）
*  fix      修补bug
*  docs     文档（documentation）
*  style    格式（不影响代码运行的变动）
*  refactor 重构（即不是新增功能，也不是修改bug的代码变动）
*  test     增加测试
*  revert   回滚
*  config   构建过程或辅助工具的变动
*  chore    其他改动

```
git commit -m 'feat: 功能描述 备注'

ex:
git commit -m 'feat: develop movie_seat_choose feature 1.6需求'
```

- 功能描述  简短明了控制在。50字以内，用_分割
- 备注     标注对应的需求版本，以及备注信息的文字表述 控制在100字内