# Docker

## Docker命令

### Docker服务相关命令

1. 启动docker服务

   **systemctl start docker**

2. 停止docker服务

   **systemctl stop docker**

3. 重启docker服

   **systemctl restart docker**

4. 查看docker服务状态

   **systemctl status docker**

5. 开机启动docker服务

   **systemctl enable docker**

### Docker镜像相关命令

1. 查看镜像

   **docker images**

2. 搜索镜像

   **doucker search** 

3. 拉取镜像

   **docker pull**

4. 删除镜像

​       **docker rmi**

### Docker容器相关命令

1. 查看容器

   **docker ps**：查看正在运行的容器

   **docker ps -a**：查看历史容器

2. 创建容器

   **docker run [ 参数 ]**

   ![image-20230502200109874](C:\Users\Zhao\AppData\Roaming\Typora\typora-user-images\image-20230502200109874.png)

   > docker run -it --name c1 centos

3. 进入容器

   **docker exec **

   > 退出后容器不会停止运行

4. 启动容器

   **docker start**

5. 停止容器

   **docker stop**

6. 删除容器

   **docker rm**

7. 查看容器信息

   **docker inspect**

## Docker容器的数据卷

### 数据卷的概念

![image-20230502224416398](C:\Users\Zhao\AppData\Roaming\Typora\typora-user-images\image-20230502224416398.png)

#### 数据卷

- 数据卷是宿主机中的一个目录或文件（与容器中的目录挂载的目录）
- 当容器目录与数据卷目录绑定后，对方的修改会立即同步
- 一个数据卷可以被多个容器同时挂载
- 一个容器可以被挂载多个数据卷

#### 配置数据卷

**创建启动容器时，使用-v参数 设置数据卷**

docker run … -v 宿主机目录（文件）: 容器内目录（文件）

![image-20230502224814658](C:\Users\Zhao\AppData\Roaming\Typora\typora-user-images\image-20230502224814658.png)

- 目录必须是绝对路径
- 如果目录不存在，会自动创建 

#### 数据卷容器

> 多容器进行数据卷交换
>
> > 数据卷容器
> >
> > ![image-20230502225935604](C:\Users\Zhao\AppData\Roaming\Typora\typora-user-images\image-20230502225935604.png)

**配置数据卷容器**

1. 创建启动c3数据卷容器，使用-v参数，设置数据卷

   **docker run -it --name=c3 ==-v /volume== centos:7 /bin/bash**

2. 创建启动c1、c2容器，使用 --volumes-from 参数，设置数据卷

   **docker run -it --name=c1 ==--volumes-from c3== centos:7 /bin/bash**

   **docker run -it --name=c2 ==--volumes-from c3== centos:7 /bin/bash**

## Docker应用部署

### MySQL部署

1. 搜索mysql镜像

```shell
docker search mysql
```

2. 拉取mysql镜像

```shell
docker pull mysql
```

3. 创建容器，设置端口映射、目录映射

```shell
# 在/root目录下创建mysql目录用于存储mysql数据信息
mkdir ~/mysql
cd ~/mysql
```

```shell
docker run -id -p 3307:3306 --name=c_mysql \
-v $PWD/conf:/etc/mysql/conf.d \
-v $PWD/logs:/logs \
-v $PWD/data:/var/lib/mysql \
-e MYSQL_ROOT_PASSWORD=123456 \
mysql
```

- 参数说明：
  - **-p 3307:3306**：将容器的 3306 端口映射到宿主机的 3307 端口。
  - **-v $PWD/conf:/etc/mysql/conf.d**：将主机当前目录下的 conf目录挂载到容器的 /etc/mysql/conf.d。<u>配置目录</u>
  - **-v $PWD/logs:/logs**：将主机当前目录下的 logs 目录挂载到容器的 /logs。<u>日志目录</u>
  - **-v $PWD/data:/var/lib/mysql** ：将主机当前目录下的data目录挂载到容器的 /var/lib/mysql 。<u>数据目录</u>
  - **-e MYSQL_ROOT_PASSWORD=123456：**初始化 root 用户的密码。



4. 进入容器，操作mysql

```shell
docker exec –it c_mysql /bin/bash
```

5. 使用外部机器连接容器中的mysql

![1573636765632](C:\Users\Zhao\Desktop\资料\imgs\1573636765632.png)



## Dockerfile

### Docker镜像原理

![image-20230503001559111](C:\Users\Zhao\AppData\Roaming\Typora\typora-user-images\image-20230503001559111.png)

### 镜像制作

#### 容器转为镜像

![image-20230503001844600](C:\Users\Zhao\AppData\Roaming\Typora\typora-user-images\image-20230503001844600.png)

**docker ==commit== 容器id 镜像名称:版本号**

> 新的镜像包含部分改变内容（目录挂载的<--数据卷-->部分不会包含在新镜像中）

**docker ==save== -o 压缩文件名称 镜像名称:版本号**

**docker ==load== -i 压缩文件名称**

----

#### dockerfile

-  Dockerfile 是一个文本文件
- 包含了一条条的指令
- 每一条指令构建一层，基于基础镜像，最终构建出一个新的镜像
- 相关指令如下：

| 关键字      | 作用                     | 备注                                                         |
| ----------- | ------------------------ | ------------------------------------------------------------ |
| FROM        | 指定父镜像               | 指定dockerfile基于那个image构建                              |
| MAINTAINER  | 作者信息                 | 用来标明这个dockerfile谁写的                                 |
| LABEL       | 标签                     | 用来标明dockerfile的标签 可以使用Label代替Maintainer 最终都是在docker image基本信息中可以查看 |
| RUN         | 执行命令                 | 执行一段命令 默认是/bin/sh 格式: RUN command 或者 RUN ["command" , "param1","param2"] |
| CMD         | 容器启动命令             | 提供启动容器时候的默认命令 和ENTRYPOINT配合使用.格式 CMD command param1 param2 或者 CMD ["command" , "param1","param2"] |
| ENTRYPOINT  | 入口                     | 一般在制作一些执行就关闭的容器中会使用                       |
| COPY        | 复制文件                 | build的时候复制文件到image中                                 |
| ADD         | 添加文件                 | build的时候添加文件到image中 不仅仅局限于当前build上下文 可以来源于远程服务 |
| ENV         | 环境变量                 | 指定build时候的环境变量 可以在启动的容器的时候 通过-e覆盖 格式ENV name=value |
| ARG         | 构建参数                 | 构建参数 只在构建的时候使用的参数 如果有ENV 那么ENV的相同名字的值始终覆盖arg的参数 |
| VOLUME      | 定义外部可以挂载的数据卷 | 指定build的image那些目录可以启动的时候挂载到文件系统中 启动容器的时候使用 -v 绑定 格式 VOLUME ["目录"] |
| EXPOSE      | 暴露端口                 | 定义容器运行的时候监听的端口 启动容器的使用-p来绑定暴露端口 格式: EXPOSE 8080 或者 EXPOSE 8080/udp |
| WORKDIR     | 工作目录                 | 指定容器内部的工作目录 如果没有创建则自动创建 如果指定/ 使用的是绝对地址 如果不是/开头那么是在上一条workdir的路径的相对路径 |
| USER        | 指定执行用户             | 指定build或者启动的时候 用户 在RUN CMD ENTRYPONT执行的时候的用户 |
| HEALTHCHECK | 健康检查                 | 指定监测当前容器的健康监测的命令 基本上没用 因为很多时候 应用本身有健康监测机制 |
| ONBUILD     | 触发器                   | 当存在ONBUILD关键字的镜像作为基础镜像的时候 当执行FROM完成之后 会执行 ONBUILD的命令 但是不影响当前镜像 用处也不怎么大 |
| STOPSIGNAL  | 发送信号量到宿主机       | 该STOPSIGNAL指令设置将发送到容器的系统调用信号以退出。       |
| SHELL       | 指定执行脚本的shell      | 指定RUN CMD ENTRYPOINT 执行命令的时候 使用的shell            |

### Dockerfile案例

> 需求：自定义centos镜像，要求默认登陆路径为/usr、可以使用vim

- 实现步骤（编写douckerfile文件）

  1. 定义父镜像：==FROM== centos:7

  2. 定义作者信息：==MAINTAINER== yangxz\<yangxz1100@163.com\>

  3. 执行安装vim命令：==RUN== yum install **-y** vim

     > 安装软件时一般都会弹出提示让用户选择y / n，加上-y 就不需要选择

  4. 定义默认的工作目录：==WORKDIR== /usr

  5. 定义容器启动执行的目录： ==CMD== /bin/bash

- 通过dockerfile文件构建自己的镜像文件

  `docker build -f ./centos_dockerfile -t yangxz_centos:1 .`

  - 使用build命令
  - -f 后面跟dockerfile文件路径（以在当前目录下为例）
  - -t 后面跟构建的镜像名称即版本号
  - **.** 表示构建上下文的路径（此处是当前路径）



## Docker服务编排

###   服务编排概念

>  微服务架构的应用系统中一般包含若干个微服务，每个微服务一般都会部署多个实例，如果每个微服务都要手动启停，维护的工作量会很大。

- 要从Dockerfile build image或者去dockerhub拉取image
- 要创建多个container
- 要管理这些container(启动停止删除)

==服务编排==：按照一定的业务规则批量管理容器

### Docker Compose

>   编排多容器分布式部署的工具，提供命令集管理容器化应用的完整开发周期
>
> 1. 利用Dockerfile定义运行环境镜像
> 2. 使用docker-compose.yml 定义组成应用的各服务
> 3. 运行docker-compose up 启动应用



## Docker私有仓库

### 搭建私有仓库

> 一般私有仓库都搭建在非当前工作的服务器
>
> 假设当前服务器为A，私有仓库搭建在B服务器

```shell
# 1、拉取私有仓库镜像（私有仓库本质也是个容器）
docker pull registry

# 2、启动私有仓库容器 
docker run -id --name=myregistry -p 5000:5000 registry

# 3、打开浏览器 输入地址http://B服务器ip:5000/v2/_catalog，看到{"repositories":[]} 表示私有仓库 搭建成功

# 4、在服务器A中修改daemon.json   
vim /etc/docker/daemon.json    

# 在上述文件中添加一个key，保存退出。此步用于让 docker 信任私有仓库地址；注意将私有仓库服务器ip修改为自己私有仓库服务器真实ip 
{"insecure-registries":["B服务器ip:5000"]} 

# 5、重启docker 服务 
systemctl restart docker
docker start registry
```

###  将镜像上传到私有仓库   

```shell
# 1、标记镜像为私有仓库的镜像     
docker tag centos:7 B服务器IP:5000/centos:7
 
# 2、上传标记的镜像     
docker push B服务器IP:5000/centos:7
```

### 从私有仓库拉取镜像 

```shell
#拉取镜像 
docker pull 私有仓库服务器ip:5000/centos:7
```



























