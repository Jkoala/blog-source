## Mysql中索引primary key 、unique key ？

primary key 只能有一个  unique key 可以有多个，两者都会建立一个索引





## 如何保证幂等

### 1. 策略

1. 状态机
2. 唯一索引
3. 分布式锁

### 2. 问题

	1. 唯一索引和is_deleted 冲突怎么办



## varchar(n) 存英文和中文的情况

> https://blog.csdn.net/sqlquan/article/details/113041833
>
> varchar(n) 的单位是字符 无论汉字和英文，mysql都能存入 n 个字符，仅实际字节长度有所区别。

## 不区分大小写
*_bin: 表示的是binary case sensitive collation，也就是说是区分大小写的  
_cs: case sensitive collation，区分大小写  
_ci: case insensitive collation，不区分大小写