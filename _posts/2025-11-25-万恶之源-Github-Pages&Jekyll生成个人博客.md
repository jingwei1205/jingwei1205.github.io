---
title: 万恶之源！Github Pages & Jekyll，您的第一个博客何必是博客
description: Github Pages免费服务 与 静态网站生成器Jekyll快速搭建自己的博客系统。 
author: jingwei
date: 2025-11-25 15:32:00 +0800
categories: [Blogging, Misc]
tags: [Misc]
pin: true
math: true
mermaid: true
comment: true
image:
  path: https://chirpy-img.netlify.app/commons/devices-mockup.png
  lqip: data:image/webp;base64,UklGRpoAAABXRUJQVlA4WAoAAAAQAAAADwAABwAAQUxQSDIAAAARL0AmbZurmr57yyIiqE8oiG0bejIYEQTgqiDA9vqnsUSI6H+oAERp2HZ65qP/VIAWAFZQOCBCAAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
  alt: Responsive rendering of Chirpy theme on multiple devices.
---
## 1. 安装RVM ruby
可以参考[**Yestercafe老师的视频**](https://www.bilibili.com/video/BV1C14y187Nh/?spm_id_from=333.1391.0.0)安装必须的环境，推荐使用rvm管理ruby的版本，windows系统若不想通过rvm管理，可以[**直接安装ruby**](https://rubyinstaller.org/downloads/)使用命令行进行后续操作，若想在wsl上安装rvm，可以根据[**rvm官方教程**](https://rvm.ruby-lang.org.cn/rvm/install)下载安装对应环境的rvm，使用windows的linux子系统wsl拍命令安装，安装后需要安装bundle。
## 2. 安装jekyll
安装ruby后可以使用gem命令安装jekyll与bundler
```shell
gem install jekyll bundler
```
安装成功后，可以查看jekyll版本号
```shell
$ jekyll -v
jekyll 4.3.1
```
## 3.选择喜爱的jekyll主题-以jekyll-theme-chirpy为例
在jekyll提供的[**主题网站**](https://www.jekyll.com.cn/docs/themes/)内选择不同的主题源，打开源选择喜爱的博客主题，一般跳转github仓库，可以使用fork的方式创建仓库，仓库名称需为您的github用户名.github.io，非用户名也可以创建，但是为项目页面，而非**个人页面**，本文以[**jekyll-theme-chirpy**](https://github.com/cotes2020/jekyll-theme-chirpy?tab=readme-ov-file)为例，使用其推荐的模板创建方式。

创建网站仓库时，根据需求有两种选择：  

**选项一: Starter（推荐）**
这种方法简化了升级，隔离了不必要的文件，非常适合希望专注于以最小配置写作的用户。
1. 登录GitHub，导航到[**启动**][starter]页面。
2. 点击<kbd>Use this template</kbd> button and then select <kbd>Create a new repository</kbd>
3. 请将新仓库命名为`<username>.github.io`,  替换`username` 为你的小写 GitHub 用户名。

**选项二: Fork**  
这种方法方便于修改功能或界面设计，但在升级过程中会带来挑战。所以除非你熟悉jekyll并打算大幅修改这个主题，否则别尝试这个。

1. 登录GitHub。
2. fork主题仓库。
3. 请将新仓库命名为`<username>.github.io`,  替换`username` 为你的小写 GitHub 用户名。

## 4. github pages设置  
 由于本页面使用jekyll，所以需要进入仓库设置页面中-pages，选择部署方式为Action，点击configure按钮会要求你提交一个jekyll的yml文件，commit文本最好使用<kbd>type(scope): subject</kbd>规范提交，然后项目就会自动部署，点击Action查看部署成功与否，根据第一阶段的提到的视频可以理解该步骤的操作。

 ![Build source](/assets/img/blog/20251125/start01.png)

 ![Build source](/assets/img/blog/20251125/start02.png){: width="972" height="589" .w-50 .left}  
 点击action后可以看到build 与 deploy的过程，若为❌则表示失败，可以点击查看错误原因，若为✅则表示成功，在settings中会生成你的页面地址，点击后即可到达。

**避坑指南**：  
很多主题会缺失相关样式文件，例如本主题的starter版本您直接本地运行或者github pages运行没有任何问题，但是您若是想复刻这个主题的[**demo**](https://chirpy.cotes.page/posts/getting-started/)，您会发现报错，这是因为缺少了很多样式素材与文件，使用以下命令获取本主题的gem路径，将里面的<kbd>_data _include assets</kbd>等文件复制到项目文件中（需提前将你的项目git clone到本地）。
```shell
bundle info --path jekyll-theme-chirpy
```
许多主题可以到此为止了，但是该主题需要booster，您会发现目前项目中没有这个路径，这是因为git忽略了，此外github pages需手动配置npm的手动流水线，这是我从本主题的[**讨论区**](
https://github.com/cotes2020/jekyll-theme-chirpy/discussions/1809)解决的问题，若您想复刻本主题的页面，这是必会遇到的问题，需要在<kbd>.github\workflows\pages-deploy.yml</kbd>中添加以下内容，且必须在Build Site流程前创建。
```yml
- name: npm build
  run: npm install && npm run build
- name: Build Site(在此之前！！！)
```

博客主题的后续更新可以参考[**官方wiki文档**](https://github.com/cotes2020/jekyll-theme-chirpy/wiki/Upgrade-Guide)

## 5. 自定义配置
打开配置文件<kbd>_config.yml</kbd>，修改以下内容：
```yml
# Site settings
title: Your Blog Name
email: your@email.com
description: >- # this means to ignore newlines until "baseurl:"
  Write an awesome description for your new site here. You can edit this
  line in _config.yml. It will appear in your document head meta (for
  Google search results) and in your feed.xml site description.
baseurl: "" # the subpath of your site, e.g. /blog
url: "https://yourusername.github.io" # the base hostname & protocol for your site, e.g. http://example.com
github_username: your_github_username
```
其中有一个cdn配置，若您有自己的cdn服务，则使用您的ip，若使用本地静态图片的话，必须设置为""，即不使用cdn服务，不然无法正确读取您配置的图片，切记。

## 6. 更新项目
项目修改完成后使用git提交仓库后，Action会自动读取刷新页面，无报错的话会及时生成变化的页面信息。在本地可以使用以下命令先行运行查看效果：
```shell
jekyll s
```

[starter]: https://github.com/cotes2020/chirpy-starter
