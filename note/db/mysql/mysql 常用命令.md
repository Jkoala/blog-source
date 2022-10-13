## 防止自增过大

alter table tablename AUTO_INCREMENT=0



## 更改唯一索引

alter table use_info add unique index agd(user_account_id,game_id,daily_date);

alter table user_info add unique key agdkey(user_account_id,game_id,daily_date);





## 改数据库编码

1.修改数据库的编码
  将数据库（test）的编码方式修改为utf8，如：
  ALTER DATABASE `test` DEFAULT CHARACTER SET utf8 COLLATE utf8_bin;

2.修改表的编码
  将表（test）的编码方式修改为utf8，如：
  ALTER TABLE `test` DEFAULT CHARACTER SET utf8 COLLATE utf8_bin;

3.修改字段的编码
  将表（test）中字段（name）的编码方式修改为utf8，如：

ALTER TABLE `test` CHANGE `name` `name` VARCHAR( 10 ) CHARACTER SET utf8 COLLATE  utf8_bin NOT NULL;

mysql数据库修改数据库编码，字段编码与表编码
https://blog.51cto.com/woshisap/5652126