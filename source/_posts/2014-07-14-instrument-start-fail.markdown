---
layout: post
title: "Instruments无法启动"
date: 2014-07-14 15:57
comments: true
categories: iOS
---

最近在iOS7的系统上使用Instrument想检查内存的leaks，启动时候总是提示失败，花了些时间，解决了这个问题，做下笔记。

##issue
```ruby
Error Starting Recording
At least one target failed to launch; aborting run


Target failed to run. Permisson to debug [app name] was denied. The app must be signed with a development identity (i.e. iOS Developer)
```
![http://ww4.sinaimg.cn/large/6e8de9dbgw1eice18vkrej20rs0jmgnq.jpg](http://ww4.sinaimg.cn/large/6e8de9dbgw1eice18vkrej20rs0jmgnq.jpg)

##fix
```ruby
Product-->Scheme-->Edit Scheme,将Profile那栏中的Build Configuration将Release改为Debug
```
![http://ww1.sinaimg.cn/large/6e8de9dbgw1eice66ef74j20jg0d7759.jpg](http://ww1.sinaimg.cn/large/6e8de9dbgw1eice66ef74j20jg0d7759.jpg)


##issue
1.如果发现leaks视图无法监控到任何的内存泄露，说明你开启了Zombie，将Scheme菜单中的`Enable Zombie Objects`勾去就可以了
2.检查你是否启用了环境变量，变量中是否开启了zombie设置

![http://ww4.sinaimg.cn/large/6e8de9dbgw1eiceaztirjj20ee0arq3q.jpg](http://ww4.sinaimg.cn/large/6e8de9dbgw1eiceaztirjj20ee0arq3q.jpg)
