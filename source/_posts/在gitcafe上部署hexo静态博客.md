title: 在gitcafe上部署hexo静态博客
date: 2016-01-30 22:07:17
categories: hexo
tags: [hexo,gitcafe]
---
　　github目前在国内访问不够稳定，所以这次选择gitcafe来托管，因为只是用来写静态博客，所以用hexo就足够了。

　　hexo是一款基于Node.js的静态博客框架，所以我们需要下载node.js，目前的LTS版本是4.2.6，我是在archlinux上使用的，所以下载的是编译好的二进制版本，当然，也可以下载源码包自行编译。
<!--more-->

# 环境准备
- 安装Node.js
　　解压下载的Node.js二进制包，将**bin**目录下的***npm***和***node***软连接到**/usr/local/bin**下

- 安装**Git**
```bash
$ sudo pacman -S git
```

- 安装hexo
```bash
npm install -g hexo
```

- 创建hexo目录
　　自定义一个目录，比如在家目录下创建**blog**目录，然后在blog目录中执行**init**命令初始化hexo：
```bash
mkdir blog
cd blog/
hexo init
```

- 安装依赖包
　　网络上很多教程只执行了***npm install***，导致我在部署的时候hexo报错，后来才发现是少装了一个依赖：
```bash
npm install
npm install hexo-deployer-git --save
```

- 本地调试hexo
　　本地调试是个非常有用的功能，在我们正式部署到gitcafe上之前，我们所有的配置、主题等都可以通过本地调试查看效果：
```bash
hexo g 
hexo s
```
　　到了这一步会出现下面的命令提示：
![hexo s](http://ww4.sinaimg.cn/large/8fee3cc7gw1f0hwzxuq4zj20fh01xwev.jpg)
　　我们可以在浏览器访问这个链接，就可以看到博客的效果。

# gitcafe设置
　　注册gitcafe之后，创建一个和用户名同名的项目：
![gitcafe](http://ww4.sinaimg.cn/large/8fee3cc7gw1f0hx72qs4oj20rq0gpabc.jpg)


- 配置ssh公钥
```bash
ssh-keygen -t rsa -C "xxx@gmail.com" #生成以你邮箱名为注释的公钥
```
这里会提示你设置密码，也可以直接回车不设置。
然后在**～/.ssh**目录下就可以看到生成的密钥，其中**id_rsa.pub**就是公钥，查看公钥，复制到gitcafe中：
```bash
cat ~/.ssh/id_rsa.pub
```
![id rsa](http://ww2.sinaimg.cn/large/8fee3cc7gw1f0hxmfq28wj20l008xq36.jpg)

- 测试ssh连接到gitcafe服务器
```bash
ssh -T git@gitcafe.com 
```
提示：**You've successfully authenticated, but GitCafe does not provide shell access.**　则代表我们已经可以连接到gitcafe。

- hexo基本配置
修改**blog**目录下的***_config.yml***文件：
```bash
vi _config.yml
```
我们需要配置的如下：
```bash
# Site
title: Blog of XXX  #你的博客名称
subtitle: Writing & Record  #副标题
description:                #描述
author: XXX                 #作者
language: zh-Hans　　#语言，对应主题下的语言文件名
timezone:
```
在最后添加下面的代码：
```bash
deploy:
  type: git
  repo: git@gitcafe.com:clikks/clikks.git
  branch: gitcafe-pages
```


# 安装配置主题
- 主题下载
我使用的是**yilia**主题：
>https://github.com/litten/hexo-theme-yilia

```bash
git clone https://github.com/litten/hexo-theme-yilia.git themes/yilia
```
　　具体的配置在github上很详细，这里不在说明，需要提示的是，主题的头像设置，图片需要放在主题目录下的***source/img/***下，然后在主题配置文件的**avatar: **后面路径写***/img/xxx.jpg***就可以了。

回到hexo的主配置文件，把**theme: **项后面改成**yilia**完成配置：
![yilia](http://ww1.sinaimg.cn/large/8fee3cc7gw1f0hyv8b4g4j208a01wjrk.jpg)

- 配置多说评论系统
　　多说是一个社会化的评论系统，我们的博客如果需要别人可以评论的话，就要在主题配置里打开多说，然后在多说注册：
```bash
vi themes/yilia/layout/_partial/post/duoshuo.ejs
#修改“<%=theme.duoshu%>”为你的多说名称
```

# 部署到gitcafe
　　现在我们就可以将博客部署到gitcafe了：
```bash
hexo g
hexo d
```
完成之后就可以访问xxx.gitcafe.io访问博客，xxx是你的用户名。

 
