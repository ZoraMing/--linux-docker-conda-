[TOC]
# docker基础操作


|命令|语法|说明|
|----|----|----|
|docker [command] --help|查看command命令用法|例：docker images --help|
|docker search [镜像名]|搜索镜像在仓库中的版本信息|例：docker search nginx|
|docker pull [镜像名:版本号]|拉取仓库的镜像到本地，不指定版本号默认latest|例：docker pull nginx 拉取最新版nginx|
|docker run [-一堆参数] --name 容器名 镜像名：版本号|--name唯一容器名 -e环境变量：变量值（一些必须有） -d后台运行 -it 可用终端直接使用 -p端口宿主：容器 -v数据卷映射，宿主容器数据双向绑定 --network该容器局域网段名 -w指定工作目录（容器内地址）--restart=always总是自启动|常用：docker run -dit -p 宿主映射端口：容器端口 --name 容器名 -e 环境变量：变量值 -v 宿主机映射卷：容器卷 镜像名：tag|
|docker ps|查看容器运行情况 -a显示所有容器|例：docker ps -a|
|docker stop（start restart） 容器名|停止，启动，重启该容器，可用容器名或者id指定|例：docker stop nginxd|
|docker exec 容器名|||
|docker export 打包包名.tar 容器名|将此容器作为基础镜像归档提交|会删除镜像历史记录和元数据例：docker export nginx.tar nginxd|
|docker import 归档包.tar 新镜像名|将归档的包作为镜像导入|docker import  my_ubuntu_v3.tar ubuntu:v4  |
|docker save -o 打包得到的包名 镜像名：tag 镜像名：tag|将一个或多个镜像打包|docker save -o my_ubuntu_v3.tar ubuntu:v3|
|docker load -i 打包.tar|导入包中的所有镜像|docker load -i fedora.tar|
|docker push 镜像：tag|上传镜像到仓库|docker push myapache:v1|
|docker rm 容器|删除一个或多个容器，-f强制删除，-v删除容器数据卷|删除所有已经停止的容器docker rm $(docker ps -a -q)|
|docker rmi 镜像名：tag|要停止使用该镜像的容器才能删除，也可以-f强制删除|docker rmi -f ubuntu:v4|
|docker inspect 容器名或者镜像名|获取容器元数据，-s指定为json格式|docker inspect mysql:8.0|
|docker logs 容器名|显示容器日志，-f追踪日志，--since显示日志开始日期，-t显示时间戳，--tail前n条日志|查看2024年3月1日之后的最新10条日志 docker logs --since="2024-03-01" --tail=10 mynginx|
|docker images|显示本地镜像，-a全部镜像，-q只显示ID，--format格式化|显示格式化后的所有镜像信息docker ps --format "table {{.ID}}\t{{.Image}}\t{{.Ports}}\t{{.Status}}\t{{.Names}}" -a|
|docker volume ls|显示docker数据卷||
|docker volume prune|删除所有未使用的volume||
|docker volume rm 数据卷名|删除某数据卷||
|docker volume create 名字|创建一个数据卷，-v可以直接绑定到这个名字上||
|docker cp 当前目录文件 容器名:数据卷|将文件从宿主机复制到容器内的数据卷中||
|docker network create 网络名 -v bridge|创建网络，使用桥接模式||
|docker container update [-命令] 容器名或id|run时忘记使用参数，使用update进行更新添加|docker container update --restart=always nginx|

例如创建mysql容器
```bash
docker run --name mymysql -e MYSQL_ROOT_PASSWORD=123456 -dit -p 3306:3306 -v mysql_data:/var/lib/mysql --network mynetwork mysql

docker container update --restart=always mymysql 
```



## docker run后容器未启动，可能原因：
- 某些镜像要求环境变量必须要有，要写对，如：MYSQL_ROOT_PASSWORD=123
- 可能端口占用，使用sudo netstat -tupln | grep 端口号检查端口。使用kill杀掉进程号pid
- 查看docker daemon进程是否正常运行，可使用systemctl restat daemon重启


# dockerfile

## 基础语法，FROM RUN
FROM：定制的镜像都是基于 FROM 的基础镜像，这里的 nginx 就是定制需要的基础镜像。后续的操作都是基于 nginx。

RUN：用于执行后面跟着的命令行命令。有以下俩种格式：

shell 格式：

```bash
RUN <命令行命令>
# <命令行命令> 等同于，在终端直接操作 shell 命令。
```
exec 格式：
```bash
RUN ["可执行文件", "参数1", "参数2"]
# 例如：
RUN ["./test.php", "dev", "offline"] 
等价于 RUN ./test.php dev offline
```
注意：Dockerfile 的指令每执行一次都会在 docker 上新建一层。所以过多无意义的层，会造成镜像膨胀过大。
如果要执行多条指令可以使用`&&`进行多条命令连接执行。如：
```bash
FROM centos
RUN yum -y install wget
RUN wget -O redis.tar.gz "http://download.redis.io/releases/redis-5.0.3.tar.gz"
RUN tar -xvf redis.tar.gz

改写为
FROM centos
RUN yum -y install wget \
    && wget -O redis.tar.gz "http://download.redis.io/releases/redis-5.0.3.tar.gz" \
    && tar -xvf redis.tar.gz
```


当创建的容器没有找到运行指令时,要指定运行程序和代码

使用`CMD`运行指定程序
类似于 `RUN` 指令，用于运行程序，但二者运行的时间点不同:

- CMD 在docker run 时运行。
- RUN 是在 docker build。
```bash
# Dockerfile
FROM python:3.9.16

WORKDIR /code/app

COPY ./app /code/app/

RUN pip install --no-cache-dir -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple

EXPOSE 5001

ENTRYPOINT ["python3","restful_api.py"]

```


相关配置也应提前写好,复制到对应位置
```bash

FROM nginx:latest

WORKDIR /usr/share/nginx/html
COPY ./dist/ /usr/share/nginx/html/

COPY ./nginx.conf /ect/nginx/nginx.conf
COPY ./conf.d/ /ect/nginx/conf.d/

EXPOSE 80

CMD ["nginx","-g","daemon off";]

```


## 创建镜像
编写dockerfile文件创建打包自己的镜像

`docker build -t 镜像名:版本号默认latest [dockerfile所在地址，在当前路径用 . ]`


|指令|说明|实例|
|-|-|-|
|FROM|指定某一镜像为基础镜像|FROM centos:6|
|ENV|设置环境变量|ENV key value|
|COPY|拷贝本地文件到镜像的指定目录|COPY ./jrell.tar.gz /tmp|
|RUN|执行linux的shell命令，常为安装过程命令。尽量使用&&链接多条命令以减小层级叠加|RUN tar -zxvf /tmp/jrell.tar.gz &&EXPORTS path=/tmp/jrell:$path|
|EXPOSE|指定这个容器运行时监听的端口|EXPOSE 8080|
|ENTRYPOINT|镜像中的启动命令，容器运行时调用|ENTRYPOINT java -jar xx.jar|
|WORKDIR|设置容器run时的工作路径,也可以创建目录,供copy使用|WORKDIR /code/app|

# docker desktop问题
vmmen内存占用过高,可能跟hype有关,但没有开启或使用hype也会出现问题
可以使用`Mem Reduct`清理内存
清理后docker命令行还能使用

