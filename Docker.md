## Docker 命令

#### 启动容器
```
docker run -it [ubuntu] /bin/bash   // 启动一个新的容器
docker start [OPTIONS] CONTAINER [CONTAINER...] // 启动一个或多个已经被停止的容器
例：docker start myrunoob 或 docker start b750bbbcfd88

// 在大部分的场景下，我们希望 docker 的服务是在后台运行的，我们可以过 -d 指定容器的运行模式。
docker run -itd --name ubuntu-test ubuntu /bin/bash
```
#### 查看运行的容器
``` 
docker ps   // 查看正在运行的容器
docker ps -l // 查看正在运行的容器的详细信息
docker ps -a // 查看所有容器
docker logs <container_id_or_name> // 替换 <container_id_or_name> 为你想要查看日志的容器ID或名称
docker attach <container_id_or_name> // 看容器的实时输出
docker top <container_id_or_name> // 查看容器内部运行的进程
```
#### 停止容器
```
docker stop [OPTIONS] CONTAINER [CONTAINER...] // 停止一个运行中的容器
例：docker stop myrunoob 即 docker stop <container_id>
```
#### 重启容器
```
docker restart [OPTIONS] CONTAINER [CONTAINER...] // 重启容器
例：docker restart myrunoob 即 docker restart <container_id>
```
#### 删除某容器
```
docker rm <container_name>
```
#### 通过镜像的id来删除指定镜像
```
docker rmi <container_id>
```
#### 删除所有镜像
```
docker rmi $(docker images -q)
```
#### 杀死所有正在运行的容器
```
docker kill $(docker ps -a -q)
```
#### 删除所有已经停止的容器
```
docker rm $(docker ps -a -q)
```
#### 宿主机重启自动启动容器
```
docker container update --restart=always php72
docker container update --restart=always mysql57
docker container update --restart=always nginx
docker container update --restart=always redis
```
#### 导出和导入容器
```
// 如果要导出本地某个容器，可以使用 docker export 命令
docker export <container_id> > <ubuntu.tar> 

// 可以使用 docker import 从容器快照文件中再导入为镜像，以下实例将快照文件 ubuntu.tar 导入到镜像 test/ubuntu:v1:
cat docker/ubuntu.tar | docker import - test/ubuntu:v1

// 此外，也可以通过指定 URL 或者某个目录来导入，例如
docker import http://example.com/exampleimage.tgz example/imagerepo
```
#### 网络端口的快捷方式
```
docker port <container_id>
```
### Docker Mysql
``` 
//拉取镜像
docker pull mysql:5.7
//进入容器 ， mysql57为别名
docker exec -it mysql57 /bin/bash
//创建并挂载到本地硬盘 –name 容器的名字
docker run -d -v E:\docker\mysql57-log:/var/log/mysql/ -v E:\docker\mysql57-conf:/etc/mysql/ -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root --name mysql57 mysql:5.7
```

### Docker php7.2
``` 
//拉取镜像
docker pull php:7.2-fpm
//进入容器
docker exec -it php72 /bin/bash
//创建并挂载到本地硬盘 --link 与另外一个容器建立起联系
#docker run -d -v E:/docker/www:/var/www/html -p 9000:9000 --link mysql56:mysql --name php72 php:7.2-fpm
docker run -d -v E:\docker\php72-conf:/usr/local/etc/php -v E:\docker\php72-log:/usr/local/var/log -v E:\docker\www:/var/www/html -p 9000:9000 --link mysql57:mysql --name php72 php:7.2-fpm

```
### Docker nginx
``` 
//拉取镜像,不跟版本号默认拉取最新的
docker pull nginx
//进入容器
docker exec -ti nginx /bin/bash
//创建并挂载到本地硬盘
docker run -d -p 80:80 --link php72:phpfpm --name nginx nginx
docker run -d -p 8080:8080 -v E:\docker\www:/var/www/html -v E:\docker\nginx-conf:/etc/nginx/conf.d -v E:\docker\nginx-log:/var/log/nginx/ --link php72:phpfpm --name nginx nginx

```
### Docker PHP扩展
``` 
//安装php扩展
docker exec -it php /bin/bash #进入php容器
```
#### 相关依赖安装
``` 
apt-get update && apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libmcrypt-dev libpng-dev
pecl install swoole-4.2.12 #安装swoole拓展
docker-php-ext-enable swoole #启用swoole拓展

Docker Ubuntu的安装
docker run -it -p 80:80 ubuntu /bin/bash
//优
docker run -it -d -p 80:80 -v E:\docker\html:/var/www/html --name ubuntu16 fac9bdaf4687
//映射多个端口
docker run -it -d -p 80:80 -p 9501:9501 -p 10022:10022 -v E:\docker\html:/var/www/html --name ubuntu16 fac9bdaf4687
 
Docker使用阿里云的镜像文件地址
docker pull registry.cn-hangzhou.aliyuncs.com/ubuntu16/ubuntu16:v2

Docker 制作ubuntu镜像
docker commit a784396dba53 my-ubuntu16
```