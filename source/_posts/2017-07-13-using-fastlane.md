title: 使用Fastlane
comment: true
date: 2017-07-13 13:59:36
categories: 自动化
---
# Fastlane使用
# Fastlane
![](fastlane_text.png)

## 相关介绍
Fastlane最初由KrauseFx([Github](https://github.com/KrauseFx), [Twitter](https://twitter.com/krausefx)) 发起，现在已经有649位代码贡献者，丰富的Action与Plugin可以满足众多个性化的需求，目前官方主要的工具如下(来自fastlane项目Github页面)

![](uploads/WX20170525-112539.png)


## 相关文档
[Github主页](https://github.com/fastlane/fastlane)
[Gem主页](https://rubygems.org/gems/fastlane)
[官方文档](https://docs.fastlane.tools/)

## Install
Fastlane是用ruby写的一套程序，最简单的方式是使用gem的方式来安装
```
gem install fastlane
```

## 初始化你的项目
创建Gemfile主要是为了让其他人安装的Gem保持统一，Cocoapods之后也可以用Gemfile来做统一的管理
```
bundle init
echo 'gem "fastlane"' >> Gemfile
bundle install
```

## init
init期间会让你输入AppleID，如果该应用存在，Fastlane会通过iTunesConnect拉取应用的metadata和所有的App截图，如果不存在，会提示你是否在iTunesConnect中创建一个新的App
```
fastlane init
```

安装完之后，会在项目中产生一个fastlane目录，使用`tree`命令查看结构如下
```
├── Appfile
├── Deliverfile
├── Fastfile
├── README.md
├── metadata
│   ├── some metadata file ...
├── report.xml
└── screenshots
    └── README.txt
```


**Appfile** 记录了你appid，apple id，team id等信息
**Deliverfile** 记录了bundle与appleid信息
**Fastfile** 是我们打包使用到的主要文件，这里面可以自定义你的流程
**metadata** 是通过iTunesConnect获取到的app的信息文件，包括介绍
**screenshots** 保存了所有的截图信息


## 一个简单的Fastfile流程
```
lane :beta do
  git_pull
  increment_build_number 				#build number更新
	cocoapods 							#安装cocoapods 
     gym(
       scheme: "MyScheme",          #主Target
       output_directory:"./build",  #导出目录
       export_method: "development" #导出方式
    )
	  sh "./customScript.sh" 			#执行你的脚本文件或Shell命令
end
```

更多关于gym的配置参数，可以参见 [Actions - fastlane docs](https://docs.fastlane.tools/actions/#gym)

**每个Action下面都有Example和Parameters，默认是收起状态** 

![](uploads/WX20170605-134929.png)



 通过执行`fastlane beta` 就可以进行打包，并且`dYSM`和`ipa`文件会导出到我们指定的项目下的`build`目录下面
```
fastlane beta
```


## 一些常用命令
```
# 列出现有的所有action
fastlane actions

# 列出所有lane任务
fastlane list

# 创建一个新的Action
fastlane new_action

# 打印环境变量，Fastfile中可以`ENV['PWD']`使用这些变量
fastlane env

# 显示本机Provision文件
security find-identity -v -p codesigning
```

## 常见问题可以参见或官方issues
[https://docs.fastlane.tools/codesigning/troubleshooting/](https://docs.fastlane.tools/codesigning/troubleshooting/)
[Issues · fastlane/fastlane · GitHub](https://github.com/fastlane/fastlane/issues)







