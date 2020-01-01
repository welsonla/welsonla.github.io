title: Mac OS 安装 配置Laravel开发环境
comment: true
date: 2020-01-01 12:57:25
categories: PHP
---


### 使用Homebrew安装PHP 7.3
实用brew的好处就是PHP版本可以不被系统升级而改变，从而保证升级系统不会影响PHP环境
```
brew install php@7.3
brew link php@7.3
```

### 安装Composer
```
wget https://getcomposer.org/installer
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('sha384', 'composer-setup.php') === 'baf1608c33254d00611ac1705c1d9958c817a1a33bce370c0595974b342601bd80b92a3f46067da89e3b06bff421f182') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php
php -r "unlink('composer-setup.php');"
```

### 添加到全局
```
mv composer.phar /usr/local/bin/composer
```

### 设置国内镜像
```
composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/  
```

### 安装Composer多线程下载支持
```
 composer global require hirak/prestissimo
```

### 安装laravel
```
composer global require laravel/installer
```
