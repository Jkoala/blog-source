## 参考

https://dev.mysql.com/doc/refman/8.0/en/user-variables.html



## 变量

```sql
# 用户变量
set @变量名=表达式；
# 系统变量
set @@系统变量名(=值)
# 局部变量声明
declare 变量名 数据类型；
```



## 赋值语句

```sql
set  变量 = 表达式
select  表达式 into 变量；//不产生结果集
select 变量 := 表达式；//产生结果集
set 变量1 = 表达式1，变量2 = 表达式2，…… 同时给多个变量赋值
```



## begin-end 语句块

```sql
# 创建存储过程
DELIMITER //
DROP PROCEDURE IF EXISTS test;
CREATE PROCEDURE test()
BEGIN
  DECLARE i INT;
  SET i = 0;
  REPEAT
    INSERT INTO test VALUES(i+11,'test','20');  　　　　　　　　　# 往test表添加数据
    SET i = i + 1;                              　　　　# 循环一次,i加一
  UNTIL i > 10 END REPEAT;                       　　　　# 结束循环的条件: 当i大于10时跳出repeat循环
  SELECT * FROM test;
END
//
CALL test();
DELIMITER ;
# 创建函数
DELIMITER //
create function test1(tid int) returns int
begin
    set @a = 0;
    select parent_id into @a from menu where id = tid;
    return @a;
end
//

set global log_bin_trust_function_creators=1;


```

```sql

SELECT T2.id, T2.name
FROM (
    SELECT
        @r AS _id,
        (SELECT @r := parent_id FROM auth_resource WHERE id = _id) AS parent_id, #@r是id,下一个递归的id=当前的parent_id,下一个递归的id作为新的parent_id
        @l := @l + 1 AS lvl
    FROM
#        修改@r  更改168 为你的子菜单
        (SELECT @r := 168, @l := 0) vars, #定义变量@r,@l
        auth_resource h
    WHERE @r <> 0) T1  #递归终止条件是 id==0
JOIN auth_resource T2
ON T1._id = T2.id;
```

