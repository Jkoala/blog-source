## 参考文档

[CSDN博客](https://blog.csdn.net/huangjhai/article/details/118854733)

[视频](https://www.bilibili.com/video/BV1og4y1q7M4?p=16)

[docker  菜鸟教程](https://www.coonote.com/docker/docker-tutorial.html)



## 命令大全

1. 执行某个容器

   >  docker run -d --name rabbitmq3.7.7 -p 5672:5672   2888deb59dfc

2. 镜像操作

   > docker rm e00b8e3e3e2e  移除镜像

3. 容器

   > docker stop 容器id
   >
   > docker start 容器id
   >
   > docker restart 容器id

4. 启动docker 服务

   > systemctl enable docker.service









## dcker

```
kubectl logs -n kubesphere-system $(kubectl get pod -n kubesphere-system -l app=ks-install -o jsonpath='{.items[0].metadata.name}') -f
```