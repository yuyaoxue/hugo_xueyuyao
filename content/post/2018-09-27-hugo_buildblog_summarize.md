---
title: "使用 hugo+github pages 搭建个人博客"
date: 2018-09-27T14:10:24+08:00
draft: false
---

# 前言

[hugo](https://gohugo.io) 是基于 Go 语言的静态网站生成器，前几天将自己的博客迁移到 hugo 上，记录下过程。

## 搭建环境

OS：Windows 10

git：[安装 Git](https://git-scm.com/downloads/);

hugo：[hugo_0.48_Windows-64bit](https://github.com/gohugoio/hugo/releases);

## 安装 Hugo

从 Hugo 的 [GitHub 仓库]((https://github.com/gohugoio/hugo/releases))下载安装。当前最新的是 hugo_0.48_Windows-64bit.zip 这个版本。下载解压后添加到 Windows 的系统环境变量的 PATH 中即可，不需安装。

## 配置 Hugo

### 初始化项目

使用 hugo new site xxx 来初始化项目，xxx 是自定义文件名。
以下是我的项目初始化过程

    C:\Users\user>hugo new site xueyuyao
    Congratulations! Your new Hugo site is created in C:\Users\user\xueyuyao.

    Just a few more steps and you're ready to go:

    1. Download a theme into the same-named folder.
    Choose a theme from https://themes.gohugo.io/, or
    create your own with the "hugo new theme <THEMENAME>" command.
    2. Perhaps you want to add some content. You can add single files
    with "hugo new <SECTIONNAME>\<FILENAME>.<FORMAT>".
    3. Start the built-in live server via "hugo server".

    Visit https://gohugo.io/ for quickstart guide and full documentation.

上面的提示信息是下载主题、添加内容后，之后在本机启动 hugo 自带的服务器调试博客。

命令执行后创建项目目录，其中的目录结构为：

    ├─archetypes //Hugo 查找原型文件(内容模板)的目录
    ├─content    // 放 markdown 文章
    ├─data       //目录放数据
    ├─layouts    //目录放网站模板文件
    ├─static     //目录放图片、css、js 等静态资源
    ├─themes     //放置下载的主题
    └─config.toml  //网站的配置文件

### 下载主题

[Hugo 主题网站](https://themes.gohugo.io/)选择你看中的主题后，点击下载链接从 GitHub 下载到 themes 目录中。也可以使用 git 命令 [git clone] 到 themes 目录下

    C:\Users\user>cd xueyuyao/themes

    C:\Users\user\xueyuyao\themes>git clone https://github.com/keichi/vienna.git
    Cloning into 'vienna'...
    remote: Enumerating objects: 511, done.
    remote: Total 511 (delta 0), reused 0 (delta 0), pack-reused 511
    Receiving objects: 100% (511/511), 2.37 MiB | 126.00 KiB/s, done.
    Resolving deltas: 100% (285/285), done.

#### 检查 themes 目录下是否成功下载主题

    C:\Users\user\xueyuyao\themes>tree
    卷 Windows 的文件夹 PATH 列表
    卷序列号为 3472-27CA
    C:.
    └─vienna
    ├─archetypes
    ├─images
    ├─layouts
    │  ├─partials
    │  └─_default
    └─static
        ├─css
        ├─fonts
        ├─images
        └─js

### 添加内容

在项目目录中执行 hugo new XX.md 命令，会在 content 目录中创建这个 XX.md 文件

    hugo new post/first_blog.md

这个文件的默认内容如下：

    ---
    title: "About"
    date: 2018-09-27T15:32:14+08:00
    draft: true
    ---

文件默认内容在，draft 表示是否是草稿，编辑完成后请将其改为 false，否则编译会跳过草稿文件。具体的博客内容在下面写：

    ---
    title: "First_blog"
    date: 2018-09-27T15:45:11+08:00
    draft: true
    ---

    hello world!

### 本机启动 hugo 自带的服务器

在项目根目录下，通过 hugo server 命令可以使用 hugo 内置服务器调试预览博客。--theme 选项可以指定主题，--watch 选项可以在修改文件后自动刷新浏览器，--buildDrafts 包括标记为草稿（draft）的内容

    C:\Users\user\xueyuyao>hugo server --theme vienna --watch
    Building sites …
                       | EN
    +------------------+----+
      Pages            |  7
      Paginator pages  |  0
      Non-page files   |  0
      Static files     | 14
      Processed images |  0
      Aliases          |  1
      Sitemaps         |  1
      Cleaned          |  0

    Total in 34 ms
    Watching for changes in C:\Users\user\xueyuyao\{content,data,layouts,static,themes}
    Watching for config changes in C:\Users\user\xueyuyao\config.toml
    Serving pages from memory
    Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
    Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
    Press Ctrl+C to stop

访问 http://localhost:1313/ 就能看到刚才添加的文章了

如果在 config.toml 中配置了固定的主题，命令可不加 --theme。

### theme 设定

config.toml

    baseURL = "http://www.xueyuyao.com"  这 baseURL 是部署后的访问地址。
    languageCode = "en-us"
    title = "My New Hugo Site"
    theme = "vienna"  // 你使用的theme 名称

vienna 文件夹里的 README 文件里包含着该主题的设置说明。

## 部署到GitHub

### 创建 Github Pages

通过 [github pages 使用指南](https://pages.github.com/)，创建自己的个人博客站点

### 绑定域名

把网站托管到 GitHub Pages 上，也可以自定义域名。[github 自定义域名](https://www.xueyuyao.com/2018/05/29/2018-05-29-githubcustomdomain/)

### 开始部署

在 hugo 的项目根目录下，执行以下命令：

    C:\Users\user\xueyuyao> hugo --theme=vienna --buildDrafts --baseUrl="http://www.xueyuyao.com"
    Building sites …
                       | EN
    +------------------+----+
      Pages            | 11
      Paginator pages  |  0
      Non-page files   |  0
      Static files     | 14
      Processed images |  0
      Aliases          |  1
      Sitemaps         |  1
      Cleaned          |  0

    Total in 304 ms

--buildDrafts 不加会生成无内容的网站
--baseUrl 要和 config.toml 的地址一致。

根目录下创建 public 文件（里面的内容就是你要上传的静态网站的文件。）

把 public 文件里的内容添加到你的 Github 的博客站点上并推送；过几分钟，访问网站地址就可以看到网站内容了。

## 配置过程中遇到的问题

1.hugo server、hugo new xx.md 命令 要在创建的项目根目录下才会生效。

2.生成静态网站时，hugo 会忽略所有通过 draft: true 标记为草稿的文件。必须改为 draft: false 才会编译进 HTML 文件。
