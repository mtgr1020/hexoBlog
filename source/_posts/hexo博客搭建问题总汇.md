---
title: hexo博客搭建问题总汇
date: 2018-12-27 15:24:47
tags: 
- hexo
- ccs
categories: 技术分享
---

## 前言


&nbsp;&nbsp;&nbsp;&nbsp;18年9月份的时候，我开始想写一些文章来记录自己的学习总结，最初考虑在云服务器来搭建个人的博客，but我找了一下没想好到底怎么做，就先在CSDN上开始简单写一些简单的博客。
<img src="http://pkhjrimz1.bkt.clouddn.com/smjs.jpg" width="30%" height="30%" />

光阴似箭，一晃这就来到12月中旬，终于有闲暇的时间好好研究搭建博客的事情，最终定下来用Hexo+GitHub Pages免费托管,感谢[Hank ZHU](https://zealot.top/)博主的技术分享，给予我Ctrl+C、Ctrl+V搭建博客的机会，在此总结记录下并会不断改进优化。

---

## 基础搭建

* 申请[GitHub](https://pages.github.com/)帐号
* 安装[Node](http://nodejs.cn/download/)

&nbsp;&nbsp;&nbsp;&nbsp;上边两个不做过多介绍，安装node以后在安装Hexo,安装命令`npm install hexo-cli -g`全局安装 > 找个放置博客源文件的目录`hexo init blogName` 建立博客 > `cd blogName `进入博客目录 > `npm install`安装Hexo依赖 > `hexo server` 在终端输出中看到可以在localhost:4000访问了,默认端口4000可更改。具体Hexo使用可以去[Hexo官网](https://hexo.io/zh-cn/)自己研究很简单，稍微复杂的是博客主题配置。怎么现在你就看到你的博客了，很简单吧！
<img src="http://pkhjrimz1.bkt.clouddn.com/6af89bc8gw1f8qw9oywz6j20b40b40sz.jpg" width="30%" height="30%" />

我们的最终目的，还是要所有人可以访问我们的博客，那肯定需要一个服务器来托管，这时候GitHub Pages可以满足我们的需求。登陆GitHub帐号，新建一个项目名称为`(你的GitHub用户名).github.io`

### 安装 hexo-deployer-git
```
npm install hexo-deployer-git --save
```
### 配置git发布地址
我们在上面安装的hexo-deployer-git是一个博客发布插件，具体用法稍后介绍，我们首先要找到blogName下的_config.yml配置文件配置deploy，repo粘贴你的github项目地址，如果想配置分支可以加上`branch: master`
<img src="http://pkhjrimz1.bkt.clouddn.com/WX20190102-171357@2x.png"/>
如果初次使用GitHub需要一些配置，可以参考[初次安装git配置](https://www.cnblogs.com/superGG1990/p/6844952.html),都完成以后就可以使用命令
```
hexo clean && hexo g && hexo d
```
然后在浏览器输入***.github.io,就可以看到你的博客了，会有一些延迟不要着急，先检查有没有上传到你的github上去。
<img src="http://pkhjrimz1.bkt.clouddn.com/1546421123287.jpg"/>

## 主题配置