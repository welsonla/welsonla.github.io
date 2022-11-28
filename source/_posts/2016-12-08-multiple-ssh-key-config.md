title: 配置多个SSH Keygen
comment: true
date: 2016-12-08 10:16:06
categories:
---

```ruby
ssh-keygen -t rsa -C "YourMail@github.com" -f ~/.ssh/github_rsa
```

## 添加到私钥列表
```ruby
ssh-add ~/.ssh/id_rsa
ssh-add ~/.ssh/github_rsa
```

## 查看私钥列表
```ruby
# 可以通过 ssh-add -l 来确私钥列表
ssh-add -l

# 可以通过 ssh-add -D 来清空私钥列表
ssh-add -D
```

## 添加配置
```ruby
cd ~/.ssh
touch config
```

## 添加配置内容
```ruby
Host github.com
    HostName github.com
    PreferredAuthentications publickey #认证类型为私钥
    IdentityFile ~/.ssh/github_rsa
```

## 添加github_rsa.pub内容到github的SSH KEY列表
```ruby
cat ~/.ssh/github_rsa.pub
```

## 测试
```ruby
⇒  ssh -T git@github.com

# 会提示， 说明已经配置成功
Hi welsonla! You've successfully authenticated, but GitHub does not provide shell access.
```

### 参考资料
[https://my.oschina.net/stefanzhlg/blog/529403](https://my.oschina.net/stefanzhlg/blog/529403)  
[http://riny.net/2014/git-ssh-key/](http://riny.net/2014/git-ssh-key/)
