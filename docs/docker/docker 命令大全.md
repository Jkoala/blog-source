# s
## 参考文档

[视频](https://www.bilibili.com/video/BV1og4y1q7M4?p=16)
[docker  菜鸟教程](https://www.coonote.com/docker/docker-tutorial.html)
[docker从入门到实践](https://yeasy.gitbook.io/docker_practice/image/other)
[dockerhub](https://hub.docker.com/)
[官方英文文档](https://docs.docker.com/search/?q=dockerfile)
[docker视频](https://www.bilibili.com/video/BV1gr4y1U7CY/?spm_id_from=333.337.search-card.all.click&vd_source=6df4aa7b31f2694a11d8f97c71a807d8)


## 命令大全
### **命令分类**
```c
Docker环境信息   info、version
镜像仓库命令      login、logout、pull、push、search
镜像管理          build、images、import、load、rmi、save、tag、commit
容器生命周期管理  create、exec、kill、pause、restart、rm、run、start、stop、unpause
容器运维操作      attach、export、inspect、port、ps、rename、stats、top、wait、cp、diff、update
容器资源管理      volume、network
系统信息日志      events、history、logs
1.events打印容器的实时系统事件
2.history 打印出指定镜像的历史版本信息
3.logs打印容器中进程的运行日志
```
### **其他命令**
```c
# 启动docker 服务
systemctl enable docker.service
```