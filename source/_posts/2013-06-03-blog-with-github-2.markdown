---
layout: post
title: "blog with github(2)-部署到github"
date: 2013-06-03 13:20
comments: true
categories: 
---


###使用github pages

如果想使用 http://username.github.io的域名作为你的blog地址的话，首先要创建一个仓库，名字为你的用户id.github.io（比如我的是welsonla.github.io）



用户使用的是Github Pages的master版本下面的public作为你的网站主目录，你可以通过浏览http://username.github.io来查看。如果你想在source这个版本上面维护代码，并且把内容提交到master分支，Octopress有一个命令来帮助你完成这些

```ruby
rake setup_github_pages
```

然后，他将 

1. 询问你的github pages的url
2. 将远程的重‘origin’重命名为‘octopress’
3. 在远程的origin讲你的github pages仓库添加进去
4. 切换当前branch从master切换到source
5. 根据你的仓库名，重新配置你的blog地址
6. 在_deploy目录下面设置master分支，用于部署



接下来执行
```ruby
rake generate
rake deploy

```

这将生成你的blog，并将生成的文件copy到_deploy目录下面,并添加到git，将他们commit和push到master分支上面，稍后，你会收到一份来自github的email告诉你，你的提交已经收到，并且很快将发不到你的web上面


并且，不要忘记提交你的代码到source分支

```ruby
git add .
git commit -m 'your message'
git push origin source
```



####自定义域名绑定


首先你要source目录下面创建一个CNAME，

```ruby
echo 'your-domain.com' >> source/CNAME
```


之后去你的域名服务商或者你的dns服务商那里创建一条CNAME记录，记录指向的IP为
(不要使用顶级域名指向到pages,要使用二级域名)
```ruby
207.97.227.245
```