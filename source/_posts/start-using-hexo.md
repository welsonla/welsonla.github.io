title: Blog迁移到了Hexo
date: 2015-10-10 10:58:17
tags: something
---

####Octopress的痛点

受不了`_deploy`文件夹的折磨，以及AutoGenerate Disable这错误导致生成问题，rake deploy靠运气成功,今天将blog迁移到了hexo

####Hexo优点
######更简洁的语法
```ruby
 hexo new
 hexo g
 hexo d
 hexo s
```


####安装
1. 安装Node
```ruby
https://nodejs.org
```

2. 安装hexo以及用到的东西
```ruby
npm install -g hexo-cli

```

3. 创建Blog
```ruby
hexo init blog
```

4. 创建文章
```ruby
cd blog
hexo new "first blog"
```

5. 预备部署
```ruby
#添加github部署支持
npm install hexo-deployer-git --save


#修改_config.yml
deploy: 
  type: git #不要再使用github作为type
  repo: git@github.com:welsonla/welsonla.github.com.git
  branch: master
```
