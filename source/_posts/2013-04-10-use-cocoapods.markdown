---
layout: post
title: "Cocoapods 使用"
date: 2013-04-10 16:48
comments: true
categories: iOS 
---


```ruby
gem install cocoapods
```

cd到你的项目的根目录，就是跟project文件同级,建立Podfile文件
```ruby
touch Podfile
```

加入平台版本，（5.1可以省略，但是最好在podfile中加入，因为一些ARC相关的类库不加的话，会提示错误）
```ruby
platform :ios,'5.1'
```


搜索第三方的oc库

```ruby
pod search fmdb

-> FMDB (2.0)
   A Cocoa / Objective-C wrapper around SQLite.
   - Homepage: https://github.com/ccgus/fmdb
   - Source:   https://github.com/ccgus/fmdb.git
   - Versions: 2.0, 1.5.1, 1.5 [master repo]
```

通过搜索，我们已经找到了该类库的版本的名字，只需要将这些内容加入到podfile文件中即可

```ruby
platform :ios, '5.1'
Pod 'FMDB','2.0'
```

然后执行下面的命令，将这些类库加到到本地

```ruby
pod install
```

之后将会生成一个workspace文件，以后我们打开项目的时候，就打开workspace文件即可，项目和其所需要的类库都以sub project的方式加到了这个workspace下面
