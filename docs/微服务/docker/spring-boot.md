[将jar包打包为docker镜像_Jarbein的博客（Java军师公众号）-CSDN博客_jar包打成docker镜像](https://blog.csdn.net/Jarbein/article/details/103627413) 

容器有三种状态   暂停  运行  停止

要完成的事项

1. 从github 拉取项目
2. 本地构建镜像
3. 打包部署运行



打包命令  

```java
mvn clean package
java -jar helloworld
```

```

```

编写镜像文件

```dockerfile
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

打包镜像

```shell
docker build -f DockerFile  -t  test/metabase:1.0.0  

```



## 问题

我启动镜像 hello world 8080 主机访问8080 没反应

