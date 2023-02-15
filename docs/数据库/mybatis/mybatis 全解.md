

# 使用案例

## 参考文档

[MyBatis注解（3种类型） (biancheng.net)](http://c.biancheng.net/mybatis/annotation.html)


# 对象模板

## 实体类

```java
@Data
@NoArgsConstructor
@TableName(value = "mybaties.goods")
public class Goods implements Serializable {
    @TableId(value = "id", type = IdType.INPUT)
    private Integer id;

    @TableField(value = "`name`")
    private String name;

    @TableField(value = "brand")
    private String brand;
	// 
    @JsonFormat(pattern = "yyyy-MM-dd'T'HH:mm:ss.SSS", timezone = "GMT+8")
    // 前台向后台传日期的接收模型
    @DateTimeFormat(pattern = "yyyy-MM-dd'T'HH:mm:ss.SSS")
    @TableField(value = "gmt_time")
    private LocalDateTime gmtTime;
		    @TableLogic
    private Integer isDeleted;
    private static final long serialVersionUID = 1L;
}
```



# mybatis 细节

## sql 不允许先过滤再联表 
过滤on  后面 and过滤只能过滤副表

## group by
和  max min  group_concat 使用  
一对多的情况没有group by就会出现重复数据

## #{} ${} 区别

1、#{}
解析为一个JDBC预编译语句（prepared statement）的参数标记符，把参数部分用占位符？代替。动态解析为：
select * from t_user where username = ？ ;而传入的参数将会经过PreparedStatement方法的强制类型检查和安全检查等处理，最后作为一个合法的字符串传入。
2、${}
这种方式只会做简单的字符串替换，在动态SQL解析阶段将会进行变量替换，假如传递的参数为Alice，最终处理结果如下：select * from t_user where username = 'Alice' ;
这样在预编译之前的sql语句已经不包含变量了，因此可以看出\${} 变量的替换阶段是在动态SQL解析阶段。

> 表名  行名用 ${}

## Mybatis属性useGeneratedKeys,keyProperty,keyColumn的使用

https://blog.csdn.net/csxypr/article/details/97522028

>在使用keyProperty的时候，发现竟然还有个类似的属性：keyColumn，那么他是干什么用的呢?
>keyColumn用于指定数据库table中的主键
>也就是说这是三个属性同时使用时，则可以使用数据库中自增长的主键，并且可以将主键的值返回给keyProperty中写好的字段

## mybaties 时间字段设置LocalDateTime处理

[类型处理器（typeHandlers）](https://mybatis.org/mybatis-3/zh/configuration.html#typeHandlers)

```java
<result column="gmt_time" jdbcType="TIMESTAMP" property="gmtTime" typeHandler="org.apache.ibatis.type.LocalDateTimeTypeHandler" javaType="java.time.LocalDateTime"/>
```

> java中的实体类用到了LocalDateTime 类型。
> 在转换时候报错
> Error attempting to get column ‘XXX’ from result set. Cause: java.sql.
>
> 解决方法最为简单。
> 是因为com.alibaba 的版本问题。
>
> 切换版本号到1.1.22 即可消除问题
>
> com.alibaba druid-spring-boot-starter 1.1.22
>
> 在Entity实体类内java8特性的LocalDateTime要求mysql-connector-java版本不能低于5.1.37

## 返回值解析

https://www.cnblogs.com/szrs/p/15257883.html

```java
@Override
    public PageInfo getSyncstatusPages(Syncstatus vo, int pageNo, int pageSize) {
        PageHelper.startPage(pageNo, pageSize);


       /* //查看增删改查的返回值
        //1新增：返回值自己定义，可以是void，int
        //1-1新增一条数据:插入成功,返回值为1
        int insert_success1 = yylfHttpServletMapper.insert("8", "2", "1");
        //1-2新增多条数据:插入成功，返回值为插入的数据条数，当有一条数据错误时，所有数据都会插入失败
        int insert_success2 = yylfHttpServletMapper.insert_duotiao("7");
        String insert_success3 = yylfHttpServletMapper.insert_duotiao_String("7");//不支持返回值为String类型
        //1-3新增一条数据:插入失败：主键冲突，会直接报异常
        int insert_failed = yylfHttpServletMapper.insert("1", "2", "1");
        //1-4插入null：属性为null，如果表中所有字段允许为null，插入一条所有值均为null的数据
        Syncstatus syncstatus1 = null;
        yylfHttpServletMapper.insertSyncstatus(syncstatus1);
        //1-5插入一个没有赋值的对象：属性为null，如果表中所有字段允许为null，插入一条所有值均为null的数据
        Syncstatus syncstatus2 = new Syncstatus();
        yylfHttpServletMapper.insertSyncstatus(syncstatus2);*/


        /*//2删除:返回值自己定义，可以是void，int
        //2-1删除成功：没有数据:返回值为0
        int delete_success1 = yylfHttpServletMapper.delete("0");
        //2-2删除成功：有多条数据：返回值为删除的数据条数
        int delete_success2 = yylfHttpServletMapper.delete_systemcode("2");
        //2-3删除失败：例如有外键:报异常
        int delete_fail = yylfHttpServletMapper.delete("1");*/

        //3更新:返回值自己定义，可以是void，int
        //3-1更新成功：没有数据，返回值为0
        int update_no = yylfHttpServletMapper.update_no("0");
        //3-2更新成功：有多条数据，返回更新的数据条数
        int update_duotiao = yylfHttpServletMapper.update_duotiao_systemcode("2");
        //3-3更新失败：例如有外键，报异常
        //int update_fail = yylfHttpServletMapper.update_fail("1");

        //4查询
        //4-1 没数:String 类型返回null
        Object object = yylfHttpServletMapper.select("0");
        //4-1 没数:集合 类型返回[]空集合
        Syncstatus syncstatus3 = new Syncstatus();
        syncstatus3.setStatus("7");
        List<Syncstatus> page0 = yylfHttpServletMapper.getSyncstatusList(syncstatus3);
        //4-1 没数:int 类型返回null,如果定义为int会报错。因为没数时返回null，可以将返回类型改为String
        String i = yylfHttpServletMapper.select_int(0);
        //4-1：当返回值为对象时，若返回值为空，则返回null
        //4-2 有数
        List<Syncstatus> pages = yylfHttpServletMapper.getSyncstatusList(vo);
        return new PageInfo<Syncstatus>(pages);
    }
```



# 遇到的异常

## 关于Mybatis的Mapper中多参数方法不使用@param注解报错的问题

https://blog.csdn.net/u011821334/article/details/101763001

