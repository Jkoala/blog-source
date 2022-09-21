DISTINCT

EXISTS

```
用于在WHERE后的判断操作，其返回结果是一个布尔值，使用方式是将现有行代入内查询检验，如果内查询中返回一行或是多行数据，则输出本行数据，反之内查询没有数据则不输出本行数据，如：SELECT * FROM user u WHERE EXISTS(SELECT * FROM untitled n WHERE n.friend_id=u.id)返回的是在untitled表中friend字段可以与user表中的id相关联的数据,也可以在EXISTS关键字前加NOT 返回的就是不关联的数据了
```

