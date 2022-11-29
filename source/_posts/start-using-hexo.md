title: Blog迁移到了Hexo
date: 2015-10-10 10:58:17
categories: something
keywords: hexo, github
---


## Octopress的痛点

受不了`_deploy`文件夹的折磨，以及AutoGenerate Disable这错误导致生成问题，rake deploy靠运气成功,今天将blog迁移到了hexo

## Hexo优点

1. 更简洁的语法
```ruby
 hexo new "title"
 hexo new page
 hexo g #生成
 hexo d #部署
 hexo s #运行
```

2. 更快的生成速度

3. 直观的部署结果

## 安装

1. 安装Node  

	参考node官方 [https://nodejs.org](https://nodejs.org)


2. 安装hexo以及用到的东西  
```ruby
npm install -g hexo-cli

```

3. 创建Blog  
```ruby
hexo init blog
cd blog
npm install

#安装Server
npm install hexo-server --save
```
## 基本使用
创建文章  
```ruby
hexo new "first blog"

#创建独立页面
hexo new page "about"
```

## 为页面设置多个Tag
使用如下格式可以为文章设置多个tag
```
tags:
  - hello
  - world
```

预备部署  
```ruby
#添加github部署支持
npm install hexo-deployer-git --save


## 修改_config.yml  
deploy:
  type: git #不要再使用github作为type
  repo: git@github.com:<yourname>/<yourname>.github.io.git
  branch: master
```

## 部署静态到github
```
hexo clean && hexo deploy
```

## 修改配置
### 安装主题，推荐Next, 有详细的安装文档  

##### 安装参考
http://theme-next.iissnan.com/five-minutes-setup.html

##### 详细的配置
[https://github.com/iissnan/hexo-theme-next/wiki/主题配置参考](https://github.com/iissnan/hexo-theme-next/wiki/主题配置参考)

### 添加RSS
[](https://github.com/hexojs/hexo-generator-feed)

```js
npm install hexo-generator-feed --save
```

### 上传图片
```js
放到./source/uploads文件夹下，代码中使用
![](/uploads/xxx.png)
```

### 修改生成文件的格式
修改为Year-Month-Day-title样式，方便查找
打开`_config.yml`
```js
new_post_name: :year-:month-:day-:title.md 
```

### 开启代码高亮
其实hexo本身已经自带了代码高亮，但是我的从`2.x`的版本升级到`6.0`不知道为什么就失效了，所以使用了第三方的高亮插件来代替
https://github.com/ele828/hexo-prism-plugin

```
npm i -S hexo-prism-plugin
```

修改`_config.xml`关闭`hilight`,替换成`prism_plugin`

```
prism_plugin:
  mode: 'preprocess'
  theme: 'default'
  line_number: true
highlight:
  enable: false
```
