title: 解决 Mac OS 删除文件后磁盘空间不更新的问题
comment: true
date: 2020-01-01 15:58:37
categories: Mac
---

这个问题存在了很久，一直也没有找到解决的办法，今天上网查询后发现，这个问题只存在于使用了Time Machine的用户，原因是因为Time Machine的快照自动生成造成的，于是试着按照解决方法查询了下本地快照

```
sudo tmutil listlocalsnapshots /
```

得到如下结果,确实Mac在自动的生成系统的快照
```
com.apple.TimeMachine.2019-12-31-214148.local
com.apple.TimeMachine.2019-12-31-223649.local
com.apple.TimeMachine.2020-01-01-103649.local
com.apple.TimeMachine.2020-01-01-113743.local
com.apple.TimeMachine.2020-01-01-124353.local
com.apple.TimeMachine.2020-01-01-143927.local
com.apple.TimeMachine.2020-01-01-153651.local
```

试着删除其中的一个快照
```
tmutil deletelocalsnapshots 2019-12-31-214148
```

发现系统的空间立刻就释放了，猜测就是以为Time Machine的快照自动生成导致的，不知道是Mac系统的bug还是因为备份的策略,  试着写了一个Ruby的脚本来自动的删除这些快照，希望对遇到此问题的人有帮助:

```
#/bin/bash

#diskspace info
puts "Current Diskspace info:" 
puts "---------"
puts %x[df -lh /]

#list localsnapshots
puts "\n\n---------"
list = %x[tmutil listlocalsnapshots /]
puts list

#delete snapshots
puts "\n\n---------"
puts "Start delete snapshots:"
matches = list.scan(/\d{4}-\d{2}-\d{2}-\d{6}/)
matches.each_with_index{|snapshoot,index|
    puts "delete the listlocalsnapshots #{snapshoot}"
    sh = "tmutil deletelocalsnapshots #{snapshoot}"
    system(sh)
}

#diskspace info after delete snapshot
puts puts "\n\n---------"
puts "Diskspace info after delete snapshots:"
puts %x[df -lh /]
```

将上面脚本保存为snapshots_clear.rb,或从我保存的gist上[下载](https://gist.github.com/welsonla/0e4c4a818abfae0400a4087b54e81c43)
执行. 

```shell
ruby snapshots_clear.rb
```

##### 参考资料
[Mac瘦身技巧 删除文件后可用空间还变少了？](http://nb.zol.com.cn/671/6715453.html)
[Solution: Reclaim storage back from "System"](https://forums.macrumors.com/threads/solution-reclaim-storage-back-from-system.2073174/)
