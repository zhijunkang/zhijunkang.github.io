---
title: JavaStream-获取元素数量
date: 2019-06-12 14:15:05
img: http://psxfdx6gr.bkt.clouddn.com/java.jpg
categories: Java8
tags: 
   - Java
   - Stream
---

## 获取元素数量

### 一、使用java.util.stream.Stream 接口定义的 count()方法

```java
long count = Stream.of(3,1,4,1,5,9,2,6,5).count();
System.out.printf("There are %d elements in the stream %n",count);
```

##### 输出结果：

```
There are 9 elements in the stream 

```

### 二、使用 Lambda 表达式 mapToLong 求和 sum()方法

```java
long countMapToLong = Stream.of(3,1,4,1,5,9,2,6,5).mapToLong(e -> 1l).sum();
 System.out.printf("There are %d elements in the mapToLong %n",countMapToLong);
```

##### 输出结果：

```
There are 9 elements in the mapToLong
```

##### 源码分析：

流的每个元素都被映射1（long）然后，mapToLong方法生成LongStream,它定义了sum方法,换言之，先将所有元素映射为1，再将它们相加，简单明了

### 三、使用java.util.stream.Collectors 类定义的 counting()方法 

```java
long countCollect = Stream.of(3,1,4,1,5,9,2,6,5).collect(Collectors.counting());
System.out.printf("There are %d elements in the Collectors.counting %n",countCollect);
```

##### 输出结果：

```
There are 9 elements in the Collectors.counting 
```

##### 源码分析：

"下游收集器" （downstream collector）。

