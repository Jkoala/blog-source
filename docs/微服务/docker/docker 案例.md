## docker 安装mysql
> https://blog.csdn.net/u012643122/article/details/125899829
```bash
docker run -d -p 3307:3306 --privileged=true -v "F:\other\msyql\log":"/var/log/mysql" -v "F:\other\msyql\data":"/var/lib/mysql" -v "F:\other\msyql\conf":"/etc/mysql/conf.d" -e MYSQL_ROOT_PASSWORD="root" --name mysql8 mysql:8.0.23
```

## docker 安装redis
```java
docker run --restart=always --log-opt max-size=100m --log-opt max-file=2 -p 6379:6379 --name redis -v F:\other\redis\redis.conf:/etc/redis/redis.conf -v F:\other\redis\data:/data -d redis redis-server /etc/redis/redis.conf --appendonly yes --requirepass root

```