
# 是一种被Docker程序解释的脚本，由一条一条的指令组成，每条指令对应Linux下面的一条命令。

# Docker程序将指令翻译成真正的Linux命令

# 有自己的书写格式和支持的命令，解决这些命令间的依赖关系，类似Makefile

# 书写规则
## 忽略大小写，建议使用大写
## 每一行只支持一条指令，每条指令可以携带多个参数
## 指令分为两种：
### 构建指令：指用于构建image,其操作不会在运行image的容器上执行
```
FROM (指定基础image)
FROM <image>:<tag>

MANINTAINER (用来指定镜像创建者信息)
MANINRAINER <name>

RUN (安装软件用)                       【重点】
RUN <command>

ENV (用于设置环境变量)
ENV <key><value>

ADD (从src复制文件到container的dest路径)
ADD <src><dest>  复制过去，直接解压

COPY <src><dest> 直接复制，不会解压
```

### 设置指令：指用于设置image的属性，其指定的操作将在运行image的容器中执行
```
CMD（设置container启动时执行的操作）（docker ps 中的command） 容器默认启动命令；
CMD ["executable","param1","param2"]             【重点】

ENTRYPOINT（设置container启动时执行的操作）（跟上面差不多） 用于容器启动后要执行的一些初始化操作，可以执行shell文件
ENTRYPOINT ["executable", "param1", "param2"]

USER（设置container容器的用户）
USER daemon

EXPOSE（指定容器需要映射到宿主机器的端口）              【重点】
EXPOSE <port> [<port>...]  

VOLUME（指定挂载点)）
VOLUME ["<mountpoint>"]  

WORKDIR（切换目录）                                 【重点】
WORKDIR  /path/to/workdir  

ONBUILD（在子镜像中执行）
ONBUILD <Dockerfile关键字> 




```






















