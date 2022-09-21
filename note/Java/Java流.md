## 案例

### Peek

```java
/**
* peek 
*/
@Test
public void test12() {
  ArrayList<Person> peoples = Lists.newArrayList(new Person(), new Person(), new Person(), new Person("tom", 1), new Person("koala", 1));
  final List<Person> a = peoples.stream().peek(v -> {
    v.setName("A");
  }).collect(Collectors.toList());
  System.out.println(JSON.toJSONString(a));
}
```

### 流变换Key 的类型

```java
ArrayList<Person> peoples = Lists.newArrayList(new Person("tom", 12), new Person("koala", 1));
final Map<String, Person> collect = peoples.stream().collect(Collectors.toMap(v -> v.getAge().toString(), v -> v, (a, b) -> a));
```

### flatMap

[不会Lambda表达式、函数式编程？你确定能看懂公司代码？-java8函数式编程(Lambda表达式，Optional，Stream流)从入门到精通-最通俗易懂_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1Gh41187uR?p=24&spm_id_from=pageDriver&vd_source=71a1a85793fb701c6a91e78a21d30e6c)
