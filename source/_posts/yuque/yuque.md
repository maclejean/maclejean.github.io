
---
title: 语雀加持
date: 2019-03-04 21:55:55 +0800
tags: []
categories: 
---
<a name="88210852"></a>
## 准备工作
- yuque-hexo （node package）
- 已经搭建好了hexo博客（可参考上一篇[文章](https://maclejean.github.io/2019/02/26/yuque/config/)）
- [语雀](https://www.yuque.com/dashboard)注册，并新建**公开**知识库（必须公开，会有个知识库路径**命名**）
- 文章部分内容参考[乱码](https://luan.ma/post/yuque2blog/)
<a name="224e2ccd"></a>
## 配置
在你的项目根目录的package.json追加一下内容
```json
//假设json可以添加注释
{
  "yuqueConfig": {
    "baseUrl": "https://www.yuque.com/api/v2", //api配置，无需更改
    "login": "maclejean", //用户名
    "repo": "luan.ma",  //知识库的命名
    "mdNameFormat": "slug", 
    "postPath": "source/_posts/yuque" //同步下来，文章的存放路径，这里拷贝默认即可
  }
}
```

<a name="6f7e90ea"></a>
## 语雀常用命令

```bash
yuque-hexo sync
```
同步上面配置的知识库的文章，到本地目录，并更新yuque.json<br />

```bash
yuque-hexo clean
```
删除**yuque.json，**清理掉上面配置的postPath里面的文章（比如你删除了语雀的文章，重命名等，本地也要相应的删除，要不然会出现重复的文章，我就碰到这个坑）

常用的就这两个，其他的我也没用过，没研究过，剩下的就是发布博客，推送到远端什么的，就是hexo那一套了<br />因为clean跟sync 一般是一起执行，这里我是把命令写在scripts配置里面执行的。

```json
"scripts":{
    "update":"yuque-hexo clean && yuque-hexo sync",
}
```
下一篇介绍下，搭配ci怎么做到自动化构建，发布等

