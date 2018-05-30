title: 将 ReactNative 的默认终端改为 iTerm2
comment: true
date: 2018-05-30 10:43:17
categories:
---

自己平时使用iTerm2作为主力的终端，ReactNative的默认打开终端是系统自带的Terminal，这样就会经常存在同时开启两个终端软件的情况，搜索了一下，解决方式很简单

```
open node_modules/react-native/scripts
```

 选中`launchPackager.command`,右键切换它的默认打开工具

 ![](/uploads/react-native-open-shell.png)

##### 致谢
 [https://stackoverflow.com/questions/37814803/how-to-get-react-native-run-ios-to-open-in-iterm-instead-of-terminal-on-a-macos](https://stackoverflow.com/questions/37814803/how-to-get-react-native-run-ios-to-open-in-iterm-instead-of-terminal-on-a-macos)
