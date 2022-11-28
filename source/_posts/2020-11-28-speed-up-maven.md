title: 使用阿里云加速Maven包更新
comment: true
date: 2020-11-28 21:27:05
categories:
---

阿里云maven镜像官方地址: [https://maven.aliyun.com/mvn/guide](https://maven.aliyun.com/mvn/guide)

mac用户首先建立 `~/.m2/settings.conf` 文件，然后将阿里云的Maven配置写入到文件, 然后重新加载maven配置即可, 完整配置如下

```json
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0
                      https://maven.apache.org/xsd/settings-1.0.0.xsd">
    <mirrors>
        <mirror>
            <id>aliyunmaven</id>
            <mirrorOf>*</mirrorOf>
            <name>阿里云公共仓库</name>
            <url>https://maven.aliyun.com/repository/public</url>
        </mirror>
    </mirrors>
</settings>
```


#### 参考资料
[https://developer.aliyun.com/article/78124](https://developer.aliyun.com/article/78124)