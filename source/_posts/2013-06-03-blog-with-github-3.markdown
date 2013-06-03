---
layout: post
title: "blog-with-github(3)-Octopress的一些配置"
date: 2013-06-03 13:46
comments: true
categories: 
---


Octopress的配置相当的简单，并且一般配置完成后，你不需要再对Rakefile和_config文件进行修改，下面这些是Octopress的配置文件

```ruby
_config.yml       # Main config (Jekyll's settings)
Rakefile          # Configs for deployment
config.rb         # Compass config
config.ru         # Rack config

```

Rakefile大多是与部署相关的配置,如果不需要同步的话，你就不需要进行修改

####Blog配置

_config.yml有三部分配置,你必须修改url，并且title，subtitle和author也要修改，还有一些第三方的服务需要启用


#####主配置
```ruby
url:                # For rewriting urls for RSS, etc
title:              # Used in the header and title tags
subtitle:           # A description used in the header
author:             # Your name, for RSS, Copyright, Metadata
simple_search:      # Search engine for simple site search
description:        # A default meta description for your site
date_format:        # Format dates using Ruby's date strftime syntax
subscribe_rss:      # Url for your blog's feed, defauts to /atom.xml
subscribe_email:    # Url to subscribe by email (service required)
category_feeds:     # Enable per category RSS feeds (defaults to false in 2.1)
email:              # Email address for the RSS feed if you want it.
```


#####Jekyll&Plugins

```ruby
root:               # Mapping for relative urls (default: /)
permalink:          # Permalink structure for blog posts
source:             # Directory for site source files
destination:        # Directory for generated site files
plugins:            # Directory for Jekyll plugins
code_dir:           # Directory for code snippets (for include_code plugin)
category_dir:       # Directory for generated blog category pages

pygments:           # Toggle python pygments syntax highlighting
paginate:           # Posts per page on the blog index
pagination_dir:     # Directory base for pagination URLs eg. /blog/page/2/
recent_posts:       # Number of recent posts to appear in the sidebar

default_asides:     # Configure what shows up in the sidebar and in what order
blog_index_asides:  # Optional sidebar config for blog index page
post_asides:        # Optional sidebar config for post layout
page_asides:        # Optional sidebar config for page layout
```


#####第三方配置
```ruby
Github - List your github repositories in the sidebar
Twitter - Setup a sidebar twitter feed, follow button, and tweet button (for sharing posts and pages).
Google Plus One - Setup sharing for posts and pages on Google’s plus one network.
Pinboard - Share your recent Pinboard bookmarks in the sidebar.
Delicious - Share your recent Delicious bookmarks in the sidebar.
Disqus Comments - Add your disqus short name to enable disqus comments on your site.
Google Analytics - Add your tracking id to enable Google Analytics tracking for your site.
Facebook - Add a Facebook like button

```