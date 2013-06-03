---
layout: post
title: "生成 github SSH keys"
date: 2013-04-10 22:16
comments: true
categories: 技术随笔
---


本文主要来自github官方，Generating SSH Keys


```ruby

cd ~/.ssh

创建一个文件夹来备份你原来的

mkdir backup

mv id_rsa* backup

ssh-keygen -t rsa -C "your_email@example.com"
# Creates a new ssh key using the provided email

# Generating public/private rsa key pair.

这里直接回车就会生成一个默认名为id_rsa
# Enter file in which to save the key (/Users/you/.ssh/id_rsa): [Press enter]


这里需要你输入一个你加密的key（一定要记住）
Enter passphrase (empty for no passphrase): [Type a passphrase]
Enter same passphrase again: [Type passphrase again]


Your identification has been saved in /Users/wanyc/.ssh/id_rsa.
Your public key has been saved in /Users/wanyc/.ssh/id_rsa.pub.
The key fingerprint is:
30:e8:aa:08:ee:bc:76:88:2c:3f:83:39:b0:6e:95:cc wyc.jar@gmail.com
The key's randomart image is:
+--[ RSA 2048]----+
|                 |
|     .           |
|    . o          |
|   .   o         |
|  o o   S        |
|.  E             |
|=++              |
|%*o.             |
|OO+o             |
+-----------------+


看到这个界面说明生成成功



copy加密字符到剪切板

pbcopy < ~/.ssh/id_rsa.pub




打开你的github

1. 点击 Account Settings
2. 点击左侧 "SSH Keys" 
3. 点击 "Add SSH key"
4. 粘贴你的可以到 "Key" 输入框
5. 点击 "Add key"
6. 输入你的github密码确认

```

