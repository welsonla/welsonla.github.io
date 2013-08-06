---
layout: post
title: "generate new host RSA key"
date: 2013-08-06 23:34
comments: true
categories: git
---

最近oschina的git服务器进行了迁移，导致了原有的git项目push不上去，总是提示

```ruby
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@       WARNING: POSSIBLE DNS SPOOFING DETECTED!          @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
The RSA host key for git.oschina.net has changed,
and the key for the corresponding IP address 112.124.6.106
is unknown. This could either mean that
DNS SPOOFING is happening or the IP address for the host
and its host key have changed at the same time.
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that a host key has just been changed.
```

第一个问题非常简单，就是修改/etc/hosts，添加一个IP与域名的对应关系即可

第二个是要求你更新know_host中的RSA key，执行如下命令即可

```ruby
ssh-keygen -R git.oschina.net
```

```ruby
cat /.ssh/known_hosts
```
查看known_host中的数据可以看到key已经更新了