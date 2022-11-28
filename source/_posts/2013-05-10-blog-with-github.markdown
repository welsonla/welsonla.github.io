---
layout: post
title: "blog with github(1)-前期准备"
date: 2013-05-10 01:18
comments: true
categories: 技术随笔
---


##开始之前

1. [安装Git](http://git-scm.com/)
2. 使用[rbenv](http://octopress.org/docs/setup/rbenv)或者[RVM](http://octopress.org/docs/setup/rvm)安装ruby 1.9.3

安装完后确保你的ruby版本是1.9.3
```ruby
ruby -v
```


##设置Octopress

```ruby
git clone git://github.com/imathis/octopress.git octopress
cd octopress  
```

接下来安装一些依赖

```ruby
gem install bundler
rbenv rehash   
bundle install
```

安装Octopress默认主题

```ruby
rake install
```




--未完待续，哥去睡觉
