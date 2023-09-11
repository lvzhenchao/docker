# 构建nginx：docker build 
## -f 指定dockerfile文件
## -t 指定标签
## . 上下文选项，就当成当前文件就行
### docker build -f nginx文件 -t nginx:1.17 .
```
FROM centos:7

MAINTAINER  lampol

#ADD nginx-1.17.0.tar.gz  /home/src
RUN yum install -y gcc gcc-c++ glibc make autoconf wget  openssl-devel   libxslt-devel  gd-devel  GeoIP-devel  pcre-devel  
RUN  yum clean all 
RUN groupadd  www
RUN useradd  -g www  -M -s /sbin/nologin  www
RUN wget -P /home/src  http://nginx.org/download/nginx-1.17.0.tar.gz
RUN cd /home/src  && tar xf nginx-1.17.0.tar.gz
WORKDIR  /home/src/nginx-1.17.0
RUN ./configure --user=www --group=www --prefix=/usr/local/nginx --with-http_stub_status_module --with-http_ssl_module --with-http_gzip_static_module --with-http_sub_module
RUN make && make install

EXPOSE 80

ENV PATH $PATH:/usr/local/nginx/sbin

CMD ["nginx","-g","daemon off;"]

```

# 构建php：
## docker build -f php的dockerfile文件 -t php:7.1 .

# 构建mysql：
## docker build -f mysql的dockerfile文件 -t mysql:5.6 .


















