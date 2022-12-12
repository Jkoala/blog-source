## docker 运行mysql
> https://blog.csdn.net/u012643122/article/details/125899829
```bash
docker run -d -p 3307:3306 --privileged=true -v "F:\other\msyql\log":"/var/log/mysql" -v "F:\other\msyql\data":"/var/lib/mysql" -v "F:\other\msyql\conf":"/etc/mysql/conf.d" -e MYSQL_ROOT_PASSWORD="root" --name mysql8 mysql:8.0.23
```

## docker 运行redis
```java
docker run --restart=always --log-opt max-size=100m --log-opt max-file=2 -p 6379:6379 --name redis -v F:\other\redis\redis.conf:/etc/redis/redis.conf -v F:\other\redis\data:/data -d redis redis-server /etc/redis/redis.conf --appendonly yes --requirepass root

```
## docker 启动nacos
```c
docker run -p 8848:8848 --name koala-nacos -e MODE=standalone -d nacos/nacos-server:1.4.1
```
## dockerfile
```shell
#penjdk:8-jre 为基础镜像，来构建此镜像，可以理解为运行的需要基础环境
FROM openjdk:8-jre
#WORKDIR指令用于指定容器的一个目录， 容器启动时执行的命令会在该目录下执行。
WORKDIR /opt/docker/images/metabase/
#将当前metabase.jar 复制到容器根目录下
ADD helloworld-0.0.1-SNAPSHOT.jar helloworld-0.0.1-SNAPSHOT.jar
#将依赖包 复制到容器根目录/libs下,metabase.jar已不再需要添加其它jar包
#ADD libs /libs
#暴露容器端口为3000 Docker镜像告知Docker宿主机应用监听了3000端口
EXPOSE 3000
#容器启动时执行的命令
CMD java -jar helloworld-0.0.1-SNAPSHOT.jar
```
## 打包镜像
```shell
docker build -f DockerFile  -t  test/metabase:1.0.0  .
```
