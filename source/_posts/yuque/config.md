
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
![image.png](https://cdn.nlark.com/yuque/0/2019/png/273716/1551274000249-20d4c46d-9084-4a10-aa59-c43835840ca9.png#align=left&display=inline&height=423&name=image.png&originHeight=423&originWidth=952&size=55903&status=done&width=952)<br />“User or organization site”是生成username.github.io的域名静态博客（推荐这一种，逼格更高）<br />“Project site”是生成github.io/projectname的静态博客<br />其他的配置就参照githubpage的教程，就两三步。

5.安装hexo-deployer-git 博客推送到github的工具

```bash
 npm install hexo-deployer-git --save
```

<a name="61771f08"></a>
## hexo常用命令

```bash
hexo init
```
新建一个网站。如果没有设置 `folder` ，Hexo 默认在目前的文件夹建立网站。

```bash
hexo new [layout] <title>
```
新建一篇文章。如果没有设置 `layout` 的话，默认使用 [_config.yml](https://hexo.io/zh-cn/docs/configuration) 中的 `default_layout` 参数代替。如果标        题包含空格的话，请使用引号括起来。

```bash
hexo generate
```
生成静态文件。

```bash
hexo server
```
启动服务器。默认情况下，访问网址为： `http://localhost:4000/`。

```bash
hexo clean
```
清除缓存文件 (`db.json`) 和已生成的静态文件 (`public`)。<br />在某些情况（尤其是更换主题后），如果发现您对站点的更改无论如何也不生效，您可能需要运行该命令。<br />
<br />**以上仅列出我经常用到的一些命令，更多命令及配置请移步**[**hexo中文文档**](https://hexo.io/zh-cn/docs/commands)**。**


