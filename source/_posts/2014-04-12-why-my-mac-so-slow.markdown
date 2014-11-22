---
layout: post
title: 你的Mac慢了么
date: 2014-04-12 12:56
comments: true
categories: 随笔
---

本子是MC700,已经陪伴我coding了三年,中间升级了内存,硬盘加了SSD,但是自从电池坏掉以后,我拆掉了电池,接电使用,发现越来越卡,经历了三个月左右的煎熬,我的mac终于又重新焕发了青春,说说遇到的问题


<!--more-->

1. 必须安装电池,电池坏掉的话,赶紧买新的装上,否则你的macbook会降频运行

	>这就是为什么我是SSD硬盘,依然感觉慢的要死的原因,之前电池坏了,本想着拆下来,裸奔运行,后来就发现本子卡的不行.检测你的macbook是否在降频运行,可以使用这个小工具[Intel(R) Power Gadget](http://software.intel.com/en-us/articles/intel-power-gadget-20)

2. 使用时间长,本子会发热,你会发现kenerl_task这个进程占用的CPU特别大,试着用一些软件为mac降温
   >推荐[Macs Fan Control ](http://www.crystalidea.com/macs-fan-control),能固定风扇的转速,防止温度飙的很高
   
3. 如果是自己加装的SSD,默认trim是不打开的,需要自己使用打开
	>推荐一个小工具[trim enables](http://www.cindori.org/software/trimenabler/)
     如果你是geek,也可以使用命令行打开trim,打开后需要重启你的电脑,看看这个gist上[trim_enabler.sh](https://gist.github.com/return1/4058659)
   

