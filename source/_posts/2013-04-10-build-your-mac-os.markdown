---
layout: post
title: "一个码农的Mac配置"
date: 2013-04-10 14:14
comments: true
categories: 技术随笔
---


####我常用的一些Mac工具

1. [iTerm2](http://www.iterm2.com/) 一个增强的命令终端
2. [SourceTree](http://www.sourcetreeapp.com/) git代码控制工具
3. [WunderList](https://www.wunderlist.com/) 一个出色的Todo工具，提供云同步，我把它当做我的任务列表
4. [TextMate2](https://github.com/textmate/textmate/tags) 号称"The Missing Editor for Mac OS X"
5. [SublimeText2](http://www.sublimetext.com/2) 另一个特别出色的Editor
6. [Alfred](http://www.alfredapp.com/) Option+Space,唤出，提高你打开软件的效率，购买Powerpack还可以使用很多强大的拓展
7. [iFunBox](http://www.i-funbox.com/) 管理你的苹果设备的文件，可以不通过iTunes直接把文件放到程序的Documents下面
8. [坚果云](https://jianguoyun.com/) 国内一个特别出色的网盘，可以右键添加要同步的文件
9. [Evernote](http://evernote.com/) 这个大家都懂的

####安装HomeBrew
**bold**
Homebrew是一个管理Mac拓展的工具，他可以很方便的安装你所需要的软件，以及软件的一些依赖包
__bold__
比如安装mysql，你只需要

```ruby
brew install mysql	
```
Homebrew 安装特别简单，只需要键入

```ruby
ruby -e "$(curl -fsSL https://raw.github.com/mxcl/homebrew/go)"
```

相关的文档可以到官方去查看[http://mxcl.github.io/homebrew/](http://mxcl.github.io/homebrew/)


####安装oh-my-Zsh
**bold**
Zsh是Mac上面的一个命令行增强工具，他提供了关键字高亮，命令补全，以及一些命令的拓展，
__bold__

安装步骤
```ruby
curl -L https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh | sh

#备份你的.zshrc文件
cp ~/.zshrc ~/.zshrc.orig

#创建zsh配置
cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc

#设置zsh为你的默认shell
chsh -s /bin/zsh

#重启终端就会生效
```

这里还有一些主题[https://github.com/robbyrussell/oh-my-zsh/wiki/themes](https://github.com/robbyrussell/oh-my-zsh/wiki/themes)

如果你要修改zsh的默认主题
```ruby
vi ~/.zshrc

修改ZSH_THEME为你喜欢的主题名即可
```


如果不想继续使用，可以使用以下命令卸载
```ruby
uninstall_oh_my_zsh
```