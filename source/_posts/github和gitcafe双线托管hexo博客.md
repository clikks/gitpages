title: 'github和gitcafe双线托管hexo博客'
date: 2016-02-01 23:11:14
tags: [hexo,gitcafe,github]
categories: hexo
---
　　之前，我已经将博客托管在了gitcafe上，刚好手里有个域名，所以把博客同时托管到github上，根据国内国外线路不同，来访问github或者gitcafe上托管的我的博客。
![dns](http://7xqo9u.com1.z0.glb.clouddn.com/%E6%B7%B1%E5%BA%A6%E6%88%AA%E5%9B%BE20160201233447.png)
<!--more-->
# 修改配置文件
　　将hexo的主配置文件**_config.yml**中的**deploy**项修改为下面的形式：
![deploy](http://7xqo9u.com1.z0.glb.clouddn.com/%E6%B7%B1%E5%BA%A6%E6%88%AA%E5%9B%BE20160201231951.png)
　　在**blog/source**下为github创建CNAME文件：
```bash
touch source/CNAME
#将你的域名写进去
echo "clikks.top" > source/CNAME
```

# 配置域名解析
　　我使用[DNSPod](https://www.dnspod.cn/)来解析我的域名，配置如下：
![dns](http://7xqo9u.com1.z0.glb.clouddn.com/%E6%B7%B1%E5%BA%A6%E6%88%AA%E5%9B%BE20160201233447.png)
　　登陆到gitcafe，在项目设置内填写自定义域名：
![](http://7xqo9u.com1.z0.glb.clouddn.com/%E6%B7%B1%E5%BA%A6%E6%88%AA%E5%9B%BE20160201233944.png)
以上就完成了我们的配置，执行**hexo d**就可以把博客同时托管到github和gitcafe，然后通过自己的域名访问就可以了！