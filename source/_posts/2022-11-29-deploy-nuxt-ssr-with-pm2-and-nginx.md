---
title: deploy nuxt ssr with pm2 and nginx
date: 2022-11-29 11:30:55
categories: Node
keywords: nuxt, ssr, hexo, nginx, pm2, 服务端渲染
tags:
    - Nuxt
    - pm2
    - Nginx
    - ssr
---



### Why
服务端渲染能更容易做SEO，方便每个页面单独的设置关键词以便被搜索引擎抓取，让其他人更容易在网络上搜索到。

### 测试 SEO 关键词
很多但页面应用可能不能正确的让搜索引擎抓取你的页面头部keywords，一个简单的测试方法就是使用一些第三方网站来测试抓取效果

[https://seo.chinaz.com/](https://seo.chinaz.com/)
[https://www.aizhan.com/](https://www.aizhan.com/)
[https://pagespeed.web.dev/](https://pagespeed.web.dev/)


### 切换Nuxt到ssr模式
如果你的nuxt应用之前使用的是静态站点的模式，请在nuxt.config.json里更新或删除如下配置

```
ssr: true,
target: 'server'
```

### 设置应用对应的端口
在`package.json`文件中增加
```
"config": {
    "nuxt": {
        "host": "0.0.0.0",
        "port": "3334"
    }
}
```

### 安装pm2
```
npm install pm2@latest -g
```

### 生成pm2配置文件
运行一下命令，这将会在你的项目目录下生成一个名为`ecosystem.config.js`配置文件
```
pm2 ecosystem
```


### 修改pm2配置文件, 增加apps节点
```
apps : [
    {
        name: 'blog', # 修改为您的项目名称
        exec_mode: 'cluster',
        instances: '2', # 按需设置进程数量
        script: './node_modules/nuxt/bin/nuxt.js',
        args: 'start'
    }
]
```

### 启动pm2
```
npm run pm2
```

### 查看运行实例
```
pm2 list
```

### 常用pm2命令
```
# 重启应用
pm2 restart all
pm2 restart [name]

# 删除应用
pm2 delete [name]

# 停止
pm2 stop all
pm2 stop [name]
```

### 启动pm2控制台，查看实时访问
```
pm2 monit
```

![pm2 monit](/uploads/pm2_monit.png)


### 在 `packge.json` 文件的 `scripts` 中增加pm2启动命令
```
"scripts": {
    "dev": "nuxt --hostname '0.0.0.0'",
    "build": "nuxt build",
    "start": "nuxt start",
    "generate": "nuxt generate",
    "pm2": "nuxt build && pm2 start npm --name labapps -- run start"
  },
```

### 部署到web服务器
将除了`node_modules`目录之外的所有文件复制到你的web目录下面，启动web实例
```
npm run pm2
```

### 修改nginx配置，增加反向代理

注意，反向代理的端口必须与你的`package.json`中设置的应用的端口相匹配，这样才能在同一台主机，运行多个pm2实例，并且互不影响
```
upstream labapps {
    server 127.0.0.1:3334;
    keepalive 64;
}

server {
    server_name timebot.net;  # 设置为你的域名

    add_header X-Frame-Options "SAMEORIGIN";
    add_header X-XSS-Protection "1; mode=block";
    add_header X-Content-Type-Options "nosniff";
    add_header Set-Cookie "Path=/; HttpOnly; Secure";

    #charset koi8-r;
    access_log /var/log/nginx/blog.access.log;
    error_log /var/log/nginx/blog.error.log debug;

    location / {
        access_log off;
        root /webroot/blog; # 修改为你的项目路径
        index index.html index.htm;
        try_files $uri $uri/ /index.html;
        if ($request_filename ~* .*\.(js|css|woff|png|jpg|jpeg)$) {
            expires 1d;
        }

        if ($request_filename ~* .*\.(?:htm|html)$) {
            add_header Cache-Control no-cache,no-store,must-revalidate;
        }

        location / {
            proxy_http_version 1.1;
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection "upgrade";
            proxy_set_header Host $host;
            proxy_set_header X-Nginx-Proxy true;
            proxy_cache_bypass $http_upgrade;
            proxy_pass http://labapps; #反向代理
        }
    }

    error_page 500 502 503 504 /50x.html;

    location = /50x.html {
        root /usr/share/nginx/html;
    }
}
```

### 查看访问
```
pm2 monit
```

### 查看实时日志
```
pm2 logs
```

另外，pm2还提供了`pm2 monitor`更强大的web端控制台，可以在web实时查看你的服务运行情况，只需要简单地配置即可.
https://pm2.keymetrics.io/docs/usage/monitoring/


###  参考资料
[Deploy Nuxt using PM2](https://nuxtjs.org/deployments/pm2/)
[常用的seo查询工具(有哪些seo软件网站平台)](https://zhuanlan.zhihu.com/p/398023953)
