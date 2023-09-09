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
