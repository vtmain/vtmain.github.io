---
title: hexo常用命令参考
date: 2017-04-13 16:09:05
updated:
description:
tags: [Syntax]
categories: [Guides]
toc: false
---
Hexo安装，初始化，和常用命令。
<!-- more -->

#### hexo
```cmd
npm install hexo -g            #安装
hexo init                      #初始化
hexo new [layout] <title>      #新建
```

#### 常用简写
```cmd
hexo n "postName" == hexo new "postName"  #新建文章(default layout post)
hexo p == hexo publish                    #发布草稿(_draft->_post)
hexo g == hexo generate                   #生成
hexo s == hexo server                     #启动服务预览
hexo s -g == hexo server --generate       #启动服务预览前生成
hexo d == hexo deploy                     #部署
hexo d -g == hexo deploy --generate       #部署前生成
hexo g -d == hexo d -g                    #部署前生成
```

#### 服务器
```cmd
hexo server                 #启动服务预览(默认端口4000，Ctrl+C关闭)
hexo server -s              #静态模式
hexo server -p 5000         #更改端口
hexo server -i 192.168.1.1  #自定义IP

hexo clean                  #清除缓存(网页正常情况下可以忽略此条命令)
hexo generate               #生成静态网页至public目录
hexo generate --watch       #监视文件变动
hexo server --generate      #启动预览前生成
hexo deploy                 #开始部署(将.deploy目录部署到GitHub)
hexo deploy --generate      #部署前生成
```

#### 模板
```cmd
hexo new [layout] <title>
```
##### 示例
```cmd
hexo new "postName"
hexo new page "pageName"
hexo new photo "My Gallery"
hexo new "Hello World" --lang tw
```

### 前置声明
*  `title:` 标题，必须
*  `date:` 创建时间
*  `updated:` 修改时间
*  `description:` 首页文章列表中显示概要
*  `comments:` 是否开启评论(true/false)
*  `tags:` 文章标签(支持多级)
*  `categories:` 文章分类(支持多级)
*  `toc:` 是否显示文章目录结构(true/false)  

多级分类示例
```cmd
categories:
- Sports
- Baseball
tags:
- Injury
- Fight
- Shocking
```
