# 拉去镜像
## docker pull nginx:1.17
## docker pull php:7.3-fpm
## docker pull mysql:5.7

# 启动容器
## 启动mysql 
## docker run -d  --name  lnmp_mysql   -e MYSQL_ROOT_PASSWORD=123456   mysql:5.7

## 启动PHP
## docker run -d  --name  lnmp_php  --link lnmp_mysql:mysql  -v /Users/lvzhenchao/home/www:/usr/share/nginx/html  php:7.3-fpm

## 启动nginx
## docker run -d --name lnmp_nginx -p 80:80  -v /Users/lvzhenchao/home/www:/usr/share/nginx/html  --link lnmp_php:php  nginx:1.17

# 修改配置Nginx
## 1、docker exec -it lnmp_nginx /bin/bash
## 2、cd /etc/nginx/conf.d，配置 vi default.conf
## 3、apt-get install vi 

```
nginx配置
location ~ \.php$ {
    root           /usr/share/nginx/html;
    fastcgi_pass   php:9000;  这个PHP 就是【--link lnmp_php:php】，可以看看etc/hosts
    fastcgi_index  index.php;
    fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
    include        fastcgi_params;
}

nginx的容器ID：6c3ee0ae2cc2
nginx的hosts
127.0.0.1	localhost
    ::1	localhost ip6-localhost ip6-loopback
    fe00::0	ip6-localnet
    ff00::0	ip6-mcastprefix
    ff02::1	ip6-allnodes
    ff02::2	ip6-allrouters
    192.168.215.3	php c41824e562c3 lnmp_php 【重点】
    192.168.215.4	6c3ee0ae2cc2
    
php的容器ID：c41824e562c3
php的hosts
    127.0.0.1	localhost
    ::1	localhost ip6-localhost ip6-loopback
    fe00::0	ip6-localnet
    ff00::0	ip6-mcastprefix
    ff02::1	ip6-allnodes
    ff02::2	ip6-allrouters
    192.168.215.2	mysql 7cb23988cb7d lnmp_mysql 【重点】
    192.168.215.3	c41824e562c3
    
mysql的容器ID：7cb23988cb7d
mysql的hosts
    127.0.0.1	localhost
    ::1	localhost ip6-localhost ip6-loopback
    fe00::0	ip6-localnet
    ff00::0	ip6-mcastprefix
    ff02::1	ip6-allnodes
    ff02::2	ip6-allrouters
    192.168.215.2	7cb23988cb7d
```

# 如果nginx的容器配置错误，并且重启失败，还进不去容器内docker exec解决方法
### find / -name 'default.conf'
### 尝试查看每个文件，是哪个；
### 宿主机都会将这些容器文件存起来

# php下载扩展 mysqli
## 1、进入到php容器内
## 2、执行docker-php-ext-install  mysqli
## 补充：单独docker-php-ext-install，可以查看有哪些扩展可以使用这个命令下载
## 3、pecl install redis 不用编译参数的下载
## 4、docker-php-ext-enable redis

# 部署discuz

