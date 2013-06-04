---
layout: post
title: "blog with github(4)-开始写吧，骚年"
date: 2013-06-03 13:57
comments: true
categories: 
---


Octopress提供很多的Rake任务去创建post和pages，他还会根据你的posts来生成Category，你可以在atom.xml或者blog/categories/\<category\>/atom.xml中找到这些内容


####Post

这些Post页面必须存放在Source/_posts目录下面，并且命名方式和jekyll的命名方式一样，会转换成YYYY-MM-DD-Post-title.markdown，这个文件的名字就是你的blog的url slug，日期帮助你排序这些文章


```ruby
rake new_post["Title"]
```

在使用了ZSH的话，你要这样创建

```ruby
rake new_post或者rake new_post[\"Title\"]
```

例如

```ruby
rake new_post["Zombie Ninjas Attack: A survivor's retrospective"]
 Creates source/_posts/2011-07-03-zombie-ninjas-attack-a-survivors-retrospective.markdown
```
or

```ruby
~/Code/rails/octopress(branch:source) » rake new_post                        
Enter a title for your post: blog-with-github-4
mkdir -p source/_posts
Creating new post: source/_posts/2013-06-03-blog-with-github-4.markdown
```


生成的内容大致如下

```ruby
---
layout: post
title: "Zombie Ninjas Attack: A survivor's retrospective"
date: 2011-07-03 5:59
comments: true
external-url:
categories:
---
```

你可以关闭comments，或者为他添加categories的tag，并且你还可以添加`author: Your Name`与`published: false`来控制是否发布


####Page

生成Page的命令

```ruby
rake new_page[super-awesome]
# creates /source/super-awesome/index.markdown

rake new_page[super-awesome/page.html]
```

如果使用了zsh的话，方法要参照post的创建方式

生成的pages的默认内如大致如下

```ruby
---
layout: page
title: "Super Awesome"
date: 2011-07-03 5:59
comments: true
sharing: true
footer: true
---
```

####Content

如果列表中不想显示全文内容的话，可以添加`<!-- more -->`标签，这将在文章下面生成一个“Continue →” 链接，链接到全文的地址




###Generate & Preview

```ruby
rake generate   # Generates posts and pages into the public directory
rake watch      # Watches source/ and sass/ for changes and regenerates
rake preview    # Watches, and mounts a webserver at http://localhost:4000
```

本地使用http://localhost:4000就可以访问了







