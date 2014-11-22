---
layout: post
title: "Mac Mini开箱"
date: 2014-11-22 23:24
comments: true
categories: CodeLife
---

###背景
从3月份换了新工作，就一直在使用自己的电脑，每天背着上下班，后来自己又买了显示器和新的机械键盘。想想这时候如果上Mac mini的话，外设都已经齐全了。
一直在等9月份的Mini新版，无奈对新版确实有些失望，一直摇摆不定，恰巧双十一的前一天，发现京东的MD387已经降价到了3588，果断决定入手了。

<!--more-->

###开箱
11.11日下午收到了京东的货，用的京东白条，可以到12.10日进行还款，这个给京东点赞

![Mini](http://ww2.sinaimg.cn/large/6e8de9dbgw1emk7661ob8j21kw23u7wh.jpg =500x)

####正面照
![mini front](http://ww2.sinaimg.cn/large/6e8de9dbjw1emk8q9x5caj21kw23u7sd.jpg =500x)

####背后有丰富的插口，再也不用担心USB口不够用了
![Mini back](http://ww2.sinaimg.cn/large/6e8de9dbgw1emk78er4izj21kw23u7sd.jpg =500x)

####配件是有一个HDMI转DVI的口
![Mini support](http://ww1.sinaimg.cn/large/6e8de9dbgw1emk7a8ffzjj21kw23unj2.jpg  =500x)


###升级
如果要换内存的话，是不用拧一颗螺丝的，旋转后壳，就能取下底部的壳,内部结构太美了
![Mini inside](http://ww4.sinaimg.cn/large/6e8de9dbgw1emk7crpjh4j21kw16oqmn.jpg =400x)

###使用
#####显示特别模糊

当我接上显示器的那一刻，我感觉眼睛都要瞎了，一定是我打开方式不对，屏幕为什么这么模糊，后来上网搜了一下，很多人都有这个问题。
有人说线的问题，我换了几条线，显示效果都是一样糟糕
后来终于找到了问题，并且感谢大神给的解决方案。[Mac OSX 顯示模糊問題，完全解決辦法](http://adolfzer.blogspot.com/2013/05/mac-osx.html)

```ruby
mac的電腦如果搭配自家螢幕可能不會有這問題，

不過如果不是用Apple的螢幕，然後又是跟我一樣是用HDMI輸出的話，

那畫面就一定很難好了，
```

我把这个脚本放到了[gist](https://gist.github.com/welsonla/e43ba2ba039c7ecd475d)上面，你复制保存到本地，命名为`patch-edid.rb`
将这个patch放到你的文档下，然后运行,会生成一套显示器配置
```ruby
ruby patch-edid.rb
```

将这套配置，放到系统`/System/Library/Displays/Overrides`,重启后就会生效了。

#####打开trim，支持10.10
鉴于网上脚本众多，而trim enabler又让很多电脑出现了问题，现在终于发现一款10.10下完美的打开Trim的工具(free)
[Chameleon](http://chameleon.alessandroboschini.com/)

![Chameleon](http://ww2.sinaimg.cn/large/6e8de9dbjw1emk7zcot3oj20880d9t95.jpg)


###总结
使用中，将MC700上的8G内存换到了Mini上面，现在的配置是
1. Mac Mini DDR3 1333 8G
2. MC700 4G DDR3 1600, Sandisk SSD 128

由于近期开销比较大，这样对两台机器进行了一个互补，发现都还可以进行正常的开发，但Mini还是要比我的MC700要快很多，不知道这台MC700还能陪伴我多久。

感谢老婆，让我这次败家，有了一个一直以来梦寐以求的工作套装
