https://www.bookstack.cn/read/rocketmq-all-4.7.1/spilt.1.709d5b2b28de54b4.md

## 发生同步消息

## 发送异步消息

异步消息通常用在对响应时间敏感的业务场景，即发送端不能容忍长时间地等待Broker的响应

## 单向发送消息

这种方式主要用在不特别关心发送结果的场景，例如日志发送。

 



## MQ 的启动

https://blog.csdn.net/fyihdg/article/details/124603758

先启动nameserver

在运行下面命令行启动 broker

**start mqbroker.cmd -n 127.0.0.1:9876 autoCreateTopicEnable=true**

控制台启动