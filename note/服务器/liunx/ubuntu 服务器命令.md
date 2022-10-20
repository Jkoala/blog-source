## 设置root 密码

sudo passws root



## 查询密码

SELECT `user`,`host`,`authentication_string`,`plugin` FROM mysql.user; 



## 开放端口

https://blog.csdn.net/qiaoliong/article/details/122176812

iptables -I INPUT -p tcp --dport 8080 -j ACCEPT

iptables-save

sudo apt-get install iptables-persistent



## 导出java 命令

 export JAVA_HOME=/home/lingjiatong/software/jdk1.8.0_333

export PATH=$PATH:$JAVA_HOME/bin

## 解压

tar -zxvf

## 关闭防火墙

```
systemctl stop firewalld.service # 停止
systemctl disable firewalld.service # 禁用防火墙，下次启动也不会开启
```

