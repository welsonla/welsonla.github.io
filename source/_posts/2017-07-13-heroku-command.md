title: heroku command
comment: true
date: 2017-07-13 14:55:36
categories:  工具控
---
记录一些经常使用到的一些heroku管理命令

# login
```
heroku login
```

# show apps info
展示你app的一些信息
```
heroku apps:info
```

# deploy
推送代码并部署
```
git push heroku  master
```

# ssh 
远程到你app目录项目，可以操作远程的一些文件，相当于ssh登录
```
heroku run bash
```

# log
查看实时输出的log
```
heroku logs -t
```