---
title: SVN服务器搭建/ubuntu-14.04
toc: false
date: 2017-05-16 17:05:05
updated: 2017-05-16 17:05:05
description:
tags:
categories:
---

系统环境 Ubuntu 14.04, svn server建立过程
<!-- more -->

1. 安装svn
```cmd
sudo apt-get install subversion  
```

2. 创建代码仓库
```cmd
svnadmin create /home/svn/project
cd project
ls
```

3. 修改文件执行权限
```cmd
chmod +x /home/svn/project/conf/authz
chmod +x /home/svn/project/conf/passwd
chmod +x /home/svn/project/conf/svnserve.conf
```

4. 配置权限
```cmd
vim /home/svn/project/conf/svnserve.conf

// 以下项取消注释
anon-access=none
auth-access=write
password-db=passwd
authz-db=authz
```

5. 配置账户和密码
```cmd  
vim /home/svn/project/conf/passwd

[user]
user=123456
```

6. 启动/查看/终止服务
```cmd
svnserve -d -r /home/svn/project/
sudo netstat -antp|grep svnserve
pkill svnserve
```

7. client访问
```cmd
svn://xxx.xxx.xxx.xxx/project
```

- 注意事项：
  1. svn默认端口3690是否开启，否则client连接阻塞，后报错
  2. [user]下配置的用户名密码和等号间不要空格
  3. authz配置用户/用户组访问权限，否则client报authentication failed
