---
title: hexo 快速搭建个人博客
date: 2021-01-07 22:49:52
tags:
---
一直想要搭建一个个人博客，但是兴趣大抵都被计算机导论课程的无理要求消磨殆尽了，最近又拾起这个项目，就是希望能督促自己定期写一些有用的东西，在毕业时也好做个回忆。看到杨栋爷搭的个人博客还挺美观，一点到power发现是如此简单的框架，便心血来潮快速搭建了一个。过程出乎意料的简单（由于是基于静态网易），结果还算满意，也记录下搭建的过程以便自己回忆以及他人搭建使用。

<!--more-->

以下是对Hexo的简单介绍。



Welcome to [Hexo](https://hexo.io/)! 

Hexo是一个简单、快速、强大的基于 Github Pages 的博客发布工具，支持Markdown格式，有众多优秀插件和主题。

官网： [http://hexo.io](http://hexo.io/)
		github: https://github.com/hexojs/hexo



##　1.准备工作

- 注册一个github账号
- 安装git bash



## 2.搭建博客

###  2.1创建仓库

新建一个名为`你的用户名.github.io`的仓库，比如说，如果你的github用户名是test，那么你就新建`test.github.io`的仓库（必须是你的用户名，其它名称无效），将来你的网站访问地址就是 [http://test.github.io](http://test.github.io/) 了。

每一个github账户最多只能创建一个这样可以直接使用域名访问的仓库。



### 2.2配置SSH Key

> 若本小节存在问题（可能较多），可以搜索‘配置SSH Key’自行解决。



使用ssh key来解决本地和服务器的连接问题。

```bash
$ cd ~/. ssh #检查本机已存在的ssh密钥
```

如果提示：No such file or directory 说明你是第一次使用git。

```bash
ssh-keygen -t rsa -C "邮件地址"
```

然后连续3次回车，最终会生成一个文件在用户目录下，打开用户目录，找到`.ssh\id_rsa.pub`文件，记事本打开并复制里面的内容，打开你的github主页，进入个人设置 -> SSH and GPG keys -> New SSH key：

![img](http://image.liuxianan.com/201608/20160818_143914_495_9084.png)

将刚复制的内容粘贴到key那里，title随便填，保存。

```
$ ssh -T git@github.com # 注意邮箱地址不用改
```

如果提示`Are you sure you want to continue connecting (yes/no)?`，输入yes，然后会看到：

> Hi free1ze! You've successfully authenticated, but GitHub does not provide shell access.

看到这个信息说明SSH已配置成功！

此时你还需要配置：

```bash
$ git config --global user.name "liuxianan"// 你的github用户名，非昵称
$ git config --global user.email  "xxx@qq.com"// 填写你的github注册邮箱
```

至此ssh key配置结束。



### 2.3安装并初始化hexo

```bash
$ npm install -g hexo
```

在本地新建一个文件夹用于存储全部文件，在该目录下启动`git bash	`

```bash
$ cd /f/Workspaces/hexo/
$ hexo init  # 初始化目录
$ hexo g 	 # 生成
$ hexo s 	 # 启动服务
```

至此，博客就通过github搭建起来了。你可以通过本地端口http://localhost:4000](http://localhost:4000/)进行查看。hexo已经预置了一篇`Hello World`示例文档。



## 3.写些博客

### 3.1 生成博文

在根目录下执行：

```bash
$ hexo new 'my-first-blog'
```

hexo会帮我们在`_posts`下生成相关md文件,你可以在/source/_posts目录下看到新生成的markdown文档。

在文档内，你可以配置其属性

```css
---
title: New Blog 添加分类及标签
author: Free1ze
date: 2020-04-01 15:40:24
categories: 
           - Hexo
tags:
           - 博客
---
```

这行属性将配合页面显示出来。

完场上面的配置，你就可以在文档内写下博客的内容了。

  

### 3.2 上传到github

首先，确保`ssh key`配置无误。

其次，配置根目录下`_config.yml`中有关deploy的部分：

```
deploy:
  type: git
  repository: git@github.com:liuxianan/liuxianan.github.io.git
  branch: master
```

当你完成改动时，在根目录下执行：

```bash
$ hexo c     # 清除分支
$ hexo g -d	 # 生成并提交改动
$ hexo s 	 # 启动服务
```

现在登录[https://free1ze.github.io/](https://free1ze.github.io/)就可以看到自己的博客页面啦！(注意将free1ze替换为自己的github用户名)

是不是超级简单呢~



## 4.更换主题

本博客使用了[keep](https://github.com/XPoet/hexo-theme-keep)主题。具体更换方式如下：

在根目录下执行:

```bash
$ npm install hexo-theme-keep
```

或者你也可以直接克隆整个代码库：

```bash
$ git clone https://github.com/XPoet/hexo-theme-keep themes/keep
```

完成安装后，打开根目录下的`_config.yml` 文件，更改`theme`选项为`keep`.

```yml
theme: keep
```

再次执行：

```bash
$ hexo c     # 清除分支
$ hexo g -d	 # 生成并提交改动
$ hexo s 	 # 启动服务
```

登录自己的博客，就可以看到效果啦~



注意：有些主题需要其他的依赖包，请根据主题本身的安装指导进行安装！（一般在repo页面的README文档中。）

  

## 5.开启其它功能

### 5.1一些常用功能

博客主题一般自带页面统计、评论、代码高亮等功能，需要在主题目录下`/theme/keep/_config.yml`中设置并开启。具体功能见说明文档：[Keep 主题使用指南](https://xpoet.cn/)。

  

### 5.2如何让博文列表不显示全部内容

默认情况下，生成的博文目录会显示全部的文章内容，如何设置文章摘要的长度呢？

答案是在合适的位置加上`<!--more-->`即可，例如：

```markdown
# 前言

使用github pages服务搭建博客的好处有：

1. 全是静态文件，访问速度快；
2. 免费方便，不用花一分钱就可以搭建一个自由的个人博客，不需要服务器不需要后台；
3. 可以随意绑定自己的域名，不仔细看的话根本看不出来你的网站是基于github的；

<!--more-->

4. 数据绝对安全，基于github的版本管理，想恢复到哪个历史版本都行；
5. 博客内容可以轻松打包、转移、发布到其它平台；
6. 等等；
```

最终效果：

![img](http://image.liuxianan.com/201608/20160823_184633_653_1893.png)



## 6.常用命令

```bash
$ hexo new "postName" #新建文章
$ hexo new page "pageName" #新建页面
$ hexo generate #生成静态页面至public目录
$ hexo server #开启预览访问端口（默认端口4000，'ctrl + c'关闭server）
$ hexo deploy #部署到GitHub
$ hexo help  # 查看帮助
$ hexo version  #查看Hexo的版本
```

缩写：

```bash
$ hexo n == hexo new
$ hexo g == hexo generate
$ hexo s == hexo server
$ hexo d == hexo deploy
```

组合命令：

```bash
$ hexo s -g #生成并本地预览
$ hexo d -g #生成并上传
```

  

## 7.来源

博客搭建教程：https://www.cnblogs.com/liuxianan/p/build-blog-website-by-hexo-github.html

主题来源：https://github.com/XPoet/hexo-theme-keep

