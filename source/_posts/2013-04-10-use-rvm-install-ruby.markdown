---
layout: post
title: "是用RVM安装ruby"
date: 2013-04-10 16:58
comments: true
categories: 技术随笔
---

今天突然发现ruby版本不小心又回到了1.8.7，可能是我修改了rvm的配置文件导致的，于是开始折腾安装rvm和ruby

首先还是先安装Homebrew吧
很简单，一行代码搞定

```ruby
ruby -e "$(curl -fsSL https://raw.github.com/mxcl/homebrew/go)"
```

安装RVM
```ruby
curl -L https://get.rvm.io | bash -s stable --ruby
```

走着走着发现出错了
```ruby
Missing required packages: autoconf, automake, libtool, pkg-config, libyaml, readline, libxml2, libxslt, libksba, openssl, sqlite.
RVM autolibs is now configured with mode '2' => 'check and stop if missing',
please run `rvm autolibs enable` to let RVM do it's job or run and read `rvm autolibs [help]`
or visit https://rvm.io/rvm/autolibs for more information.
There were package installation errors, make sure to read the log.
Check Homebrew requirements https://github.com/mxcl/homebrew/wiki/Installation
```

透过错误信息，发现缺少一写依赖的包，和rvm的autolibs没打开，这时候我们就通过Homebrew先安装上（具体你要看清楚你缺少的是什么）
```ruby
rvm autolibs enable
rvm reload
brew install autoconf automake libtool pkg-config libyaml readline libxml2 libxslt libksba openssl sqlite
```

漫长的等带后，依赖包终于装完了
再次安装RVM

```ruby
curl -L https://get.rvm.io | bash -s stable --ruby
```

就会安装成功，你可以rvm -v查看下版本


安装并设置1.9.3为你的默认版本
```ruby
rvm install 1.9.3
rvm use 1.9.3
rvm rubygems latest
```

Finish

