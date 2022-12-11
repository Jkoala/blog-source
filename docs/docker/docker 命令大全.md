## 参考文档

[视频](https://www.bilibili.com/video/BV1og4y1q7M4?p=16)
[docker  菜鸟教程](https://www.coonote.com/docker/docker-tutorial.html)
[docker从入门到实践](https://yeasy.gitbook.io/docker_practice/image/other)
[dockerhub](https://hub.docker.com/)
[官方英文文档](https://docs.docker.com/search/?q=dockerfile)
[docker视频](https://www.bilibili.com/video/BV1gr4y1U7CY/?spm_id_from=333.337.search-card.all.click&vd_source=6df4aa7b31f2694a11d8f97c71a807d8)

## 命令大全

**1. 执行某个容器**
   >  docker run -d --name rabbitmq3.7.7 -p 5672:5672   2888deb59dfc
**2. 镜像操作**
   > docker rm e00b8e3e3e2e  移除镜像
3. 容器
   > docker stop 容器id
   > docker start 容器id
   > docker restart 容器id
4. 启动docker 服务
   > systemctl enable docker.service
5. 查看容器的IP https://www.cnblogs.com/xyztank/articles/16595836.html
> docker inspect container_id
6. 查看正在运行的容器
> docker ps

## docker 命令
```c

```