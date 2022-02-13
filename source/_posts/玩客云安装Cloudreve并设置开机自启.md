---
title: 玩客云安装Cloudreve并设置开机自启
tags: 玩客云
categories: 玩客云
abbrlink: c715e3c5
date: 2021-04-11 11:19:32
---

# 玩客云安装Cloudreve并设置开机自启

Cloudreve是一个轻量化的网盘系统，用在玩客云上就特别合适，由于玩客云安装Cloudreve的坑还是很多的，自己去网上百度信息也比较零散，今天就写一篇集合。

## 安装Cloudreve

先下载文末的链接，解压，你会得到一个名为Coludreve的文件，见下图

![crpg.png](https://ivanstar.gitee.io/markdown-photo/cr/crpg.png)

把这个文件上传到玩客云，然后设置Cloudreve的权限为0755或更高，

![0755.png](https://ivanstar.gitee.io/markdown-photo/cr/0755.png)

然后cd /你放cloudreve的文件夹，执行./cloudreve，cloudreve就会开始运行了，这里会给你账号和密码，打开玩客云的IP:5212，例如我的玩客云的ip为192.168.1.5（你们的会不一样），那我访问1921.168.1.5:5212就可以进入cloudreve的管理页面。

## 配置 

输入刚刚的账号密码登录，点击右上角的那个小人头像，再弹出来的菜单里选择管理面板。

![consle.png](https://ivanstar.gitee.io/markdown-photo/cr/consle.png)

进到管理面板里面之后，点击站点信息，再点击上传与下载，找到临时目录，这里你要设置一个文件夹当cloudreve的临时目录，这里随便你写到那里，然后找到存储策略，找到默认存储策略，点击那个笔（编辑），选择向导模式编辑，找到第一项，这里是写云盘的储存目录，假如我的硬盘挂载到/mnt/wd这个目录，那这里就填/mnt/wd，以此类推，剩下的可以不管，保存即可。

chucun.png

![chucun.png](https://ivanstar.gitee.io/markdown-photo/cr/chucun.png)

如果这里你无法保存的话，你就先上传一个文件，然后你存放cloudreve的文件夹会出现一个uploads文件夹，删掉他，然后新建一个连接，名字也要叫uploads，建立连接/快捷方式到这里写你的硬盘挂载的位置，这样子资料也能存在我们的硬盘里

![link2.png](https://ivanstar.gitee.io/markdown-photo/cr/link2.png)

![link.png](https://ivanstar.gitee.io/markdown-photo/cr/link.png)

找到用户组，把管理员的最大容量设置大一点，我这里设置成1000t，免得以后加硬盘又要改，然后保存即可。

![1000t.png](https://ivanstar.gitee.io/markdown-photo/cr/1000t.png)

到这里基本就配置好了，剩下的个性化设置你自己去摸索吧。

## 设置开机自启

配置好之后，我们就要设置开机自启动了，在SSH里执行：``vim /usr/lib/systemd/system/cloudreve.service``

然后按下i键，将下面的配置粘贴到里面（把PATH_TO_CLOUDREVE改成你存放cloudreve的文件夹）：

```text
[Unit]
Description=Cloudreve
Documentation=https://docs.cloudreve.org
After=network.target
Wants=network.target

[Service]
WorkingDirectory=/PATH_TO_CLOUDREVE
ExecStart=/PATH_TO_CLOUDREVE/cloudreve
Restart=on-abnormal
RestartSec=5s
KillMode=mixed

StandardOutput=null
StandardError=syslog

[Install]
WantedBy=multi-user.target
```

然后按esc，再输入:wq，就可以保存。

然后再在ssh里面执行下面的命令（一行一行的复制）：

```text
systemctl daemon-reload
```

```text
systemctl start cloudreve
```

```text
systemctl enable cloudreve
```

然后重启你的玩客云，你就会发现cloudreve开机后会在后台默默地运行了



## 下载链接：

[cloudreve_3.3.1_linux_arm.tar.gz (github.com)](https://github.com/cloudreve/Cloudreve/releases/download/3.3.1/cloudreve_3.3.1_linux_arm.tar.gz)

上不了github的同学用下面的链接：

[cloudreve_3.3.1_linux_arm.tar.gz (hub.fastgit.org)](https://hub.fastgit.org/cloudreve/Cloudreve/releases/download/3.3.1/cloudreve_3.3.1_linux_arm.tar.gz)

顺带一提，我下一篇文章想写写我现在在用的图床和一些图床对比，不知道有没有人感兴趣，不过就算没人感兴趣我还是会写的（doge）