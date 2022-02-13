---
title: 玩客云重启后MAC地址更改的解决办法
tags: 玩客云
abbrlink: 8d4ac757
date: 2021-03-25 20:50:52
---

## 观前提醒

本方法是作者在powersee大佬的[【玩客云】疑难杂症大汇合（持续更新）_哔哩哔哩 (゜-゜)つロ 干杯~-bilibili](https://www.bilibili.com/video/BV1kT4y1P7RL)这个视频的评论区看到的，感谢@[JamesYYM](https://space.bilibili.com/353496393)

## 解决方法

先用SSH连接玩客云，输入nano /etc/network/interfaces

找到hwaddress那一行，在那一行前面加#注释掉。

<!--more-->  

再在下面那一行添加 pre-up ifconfig eth0 hw ether xx:xx:xx:xx:xx（xx:xx:xx:xx:xx为你想更改的MAC地址）

![photo.png](https://ivanstar.gitee.io/markdown-photo/wky-mac/fbK5WpDRTI2gmQG.png)





