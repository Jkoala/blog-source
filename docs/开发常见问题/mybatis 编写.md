查看官方文档即可 https://mybatis.org/mybatis-3/zh/dynamic-sql.html





## 细节
### mybatis 联表查询
结论
联表的主表用on 条件筛选始终会出来  where 才能正在的筛选
```sql
create table teacher  
(  
    id   int auto_increment  
        primary key,  
    name varchar(20) null  
);
create table student  
(  
    id         int auto_increment  
        primary key,  
    teacher_id int         not null,  
    name       varchar(20) not null  
);
```
select t.name,s.name from teacher t left  join student s on t.id = s.teacher_id;
![[Pasted image 20221230142954.png]]
select t.name,s.name from teacher t left  join student s on t.id = s.teacher_id and t.id = 2;
![[Pasted image 20221230143314.png]]

## group by

和 max min group_concat 使用  
一对多的情况没有group by就会出现重复数据