

## 使用案例

### 得到最近若干时间

### 日期格式

```java
cn.hutool.core.date.DatePattern
```

### 计算时间间隔

```java
LocalDateTime start = LocalDateTimeUtil.parse("2019-02-02T00:00:00");
LocalDateTime end = LocalDateTimeUtil.parse("2020-02-02T00:00:00");

Duration between = LocalDateTimeUtil.between(start, end);

// 365
between.toDays();
```



### 开始时间可结束时间

```java
LocalDateTime localDateTime = LocalDateTimeUtil.parse("2020-01-23T12:23:56");

// "2020-01-23T00:00"
LocalDateTime beginOfDay = LocalDateTimeUtil.beginOfDay(localDateTime);

// "2020-01-23T23:59:59.999999999"
LocalDateTime endOfDay = LocalDateTimeUtil.endOfDay(localDateTime);
```

