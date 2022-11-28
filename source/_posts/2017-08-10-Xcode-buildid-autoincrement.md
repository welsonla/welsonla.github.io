title: Xcode BuildNumber 自动更新
comment: true
date: 2017-08-10 16:16:29
categories: iOS
---

最近为了区分发包的id，从晚上找了一段代码
原理就是，先用PlistBuddy获取当前的buildid，之后+1，然后再更新plist文件
```ruby
buildNumber=$(/usr/libexec/PlistBuddy -c "Print CFBundleVersion" "${PROJECT_DIR}/${INFOPLIST_FILE}")
buildNumber=$(($buildNumber + 1))
/usr/libexec/PlistBuddy -c "Set :CFBundleVersion $buildNumber" "${PROJECT_DIR}/${INFOPLIST_FILE}"
```

From: [https://gist.github.com/sekati/3172554](https://gist.github.com/sekati/3172554)