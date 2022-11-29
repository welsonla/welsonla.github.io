---
layout: post
title: "Application Transport Security"
date: 2015-07-13 09:09:45 +0800
comments: true
categories: 
---
In Xcode7 You should add follow keys in `Info.plist` to allow the http request
A detail discuss could fond here
[https://forums.developer.apple.com/thread/3544](https://forums.developer.apple.com/thread/3544)

```
<key>NSAppTransportSecurity</key>  
<dict>  
     <key>NSAllowsArbitraryLoads</key><true/>  
</dict>  
```