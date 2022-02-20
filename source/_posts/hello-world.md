---
title: github pages+hexo搭建个人博客
updated: 2019-10-27 16:32
---


参考了几篇文章 特此感谢

[使用hexo+github搭建免费个人博客详细教程](https://www.cnblogs.com/liuxianan/p/build-blog-website-by-hexo-github.html)]
[修改npm全局安装模式的路径](https://www.cnblogs.com/mxxim/p/4413884.html)
[使用hexo上传博客至github](https://www.cnblogs.com/xrblog/p/11587349.html)

# 第一步 创建github账号（略）

# 第二步 创建github仓库
## 仓库名为 (github用户名).github.io
# 第三步 安装nodeJs

<!--more-->

## 下载
官网下载 适合自己的版本 [nodejs官网](http://nodejs.cn/download/)
## 改module下载位置
```bash
$ npm config ls
```
prefix表示当前模块下载位置
然后更改位置
```bash
$ npm config set prefix (你自己设置的模块安装位置)
```
主要方便知道自己安装的hexo在哪里 在后面配置全局命令方便一些
安装完毕后使用hexo生成静态网站模板
# 第四步 安装hexo 
## 安装hexo
``` bash
$ npm install -g hexo-cli
```
注意了hexo 路径是 npm_modules下面的目录 要配置成全局命令 
要在电脑环境变量(Path)上加上hexo 命令所在路径 即npm_moudules下面hexo
## 在你想要建站的文件夹中初始化
```bash
$ cd /f/Workspaces/hexo/ # 路径修改为 你要建站的文件夹路径 
$ hexo init # 初始化
```
然后出现很多目录
有个themes适用于存放下载主题的
其实你现在就可以看你自己的网站了 只要输入启动服务命令
```bash
$ hexo s # 启动服务 
```
在 http://localhost:4000 就能看到了 但是主题是默认的
你可以在建站目录下的 _config.yml  里面搜索theme就能看到你用的主题叫啥了 跟你themes里的对应


# 第五步 下载主题
## 网上找主题 我用的是nexT 以此为例
## 然后clone到你的hexo
``` bash
$ git clone https://github.com/iissnan/hexo-theme-next themes/next
```
 这个意思是把主题包下载到你的当前目录下的themes/next目录下
 然后你进入next 里面也有 _config.ym 这里面可以配置next里面样式scheme 边栏sidebar位置
 具体参考[next](http://theme-next.iissnan.com/getting-started.html)

# 第六步 上传至github
## 安装插件
```bash
$ npm install hexo-deployer-git --save
```
## 配置 _config.yml
deploy:
  type: git
  repository: https://github.com/ShiverZm/ShiverZm.github.io
  branch: master

## 然后上传
```bash
$ hexo g #generate 生成public目录下的html
$ hexo d #deploy 部署到github
```
# 去xxxx.github.io 查看你的自己网站 xxx为你的github用户名
