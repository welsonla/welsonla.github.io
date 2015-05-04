---
layout: post
title: "Rails code snippets"
date: 2015-04-12 12:55:48 +0800
comments: true
categories: ruby
---
(摘录来自: persie. “Ruby on Rails 教程”)

###short key
```ruby
g   generate
d   destory
s   server
```


###脚手架以及一些常用的变量类型
```ruby
rails g scaffold user name:string age:int email:string description:text cash:float
```

###删除脚手架生成的代码
```ruby
rails d scaffold Users
```

### 生成Controller与action
```ruby
rails g controller TodoList list delete index
```

###删除Controller
```ruby
rails d controller TodoList list delete index
```


###生成Model
```ruby
rails g model User name:string email:string
```

###删除Model
```ruby
rails d model User name:string email:string
```


###添加字段到表
```ruby
“rails generate migration add_password_digest_to_users password_digest:string”
```

###根据Model生成数据库表
```ruby
rake db:migrate
```



