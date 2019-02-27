
---
title: 搭建属于我的静态博客
date: 2019-02-26 21:37:15 +0800
tags: []
categories: 
---
<a name="3f38a0ec"></a>
## 相关工具
* node （安装）
* ruby （安装）
* hexo （node package）
* github （githubpages 配置）
* hexo-deployer-git（node package）
<a name="88210852"></a>
## 准备工作
1.安装[node](https://nodejs.org/zh-cn/)<br />2.安装[ruby](https://rubyinstaller.org/)<br />3.安装[hexo](https://hexo.io/zh-cn/)命令行工具

```bash
npm install -g hexo-cli
```

4.[githubpage](https://pages.github.com/)配置<br />
![image.png](https://cdn.nlark.com/yuque/0/2019/png/273716/1551274000249-20d4c46d-9084-4a10-aa59-c43835840ca9.png#align=left&display=inline&height=423&linkTarget=_blank&name=image.png&originHeight=423&originWidth=952&size=55903&status=done&width=952)<br />“User or organization site”是生成username.github.io的域名静态博客（推荐这一种，逼格更高）<br />“Project site”是生成github.io/projectname的静态博客<br />其他的配置就参照githubpage的教程，就两三步。

5.安装hexo-deployer-git 博客推送到github的工具

```bash
 npm install hexo-deployer-git --save
```

<a name="f8054f64"></a>
## 生成博客

