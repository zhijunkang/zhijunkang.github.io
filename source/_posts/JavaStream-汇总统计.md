---
title: JavaStream-汇总统计
date: 2019-06-12 14:48:14
img: http://psxfdx6gr.bkt.clouddn.com/java.jpg
categories: Java8
tags: 
   - Java
   - Stream
---

## 汇总统计

##### 问题：用户希望获取数值流中元素的数量，总和、最小值、最大值已经平均值。

##### 方案：使用IntStream、DoubleStream、LongStream 接口定义的SummaryStatistics()方法

```java
DoubleSummaryStatistics doubleSummarystatistics = DoubleStream.generate(Math::random).limit(1_000_000).summaryStatistics();
System.out.println(doubleSummarystatistics);
System.out.println("count: "+doubleSummarystatistics.getCount());
System.out.println("min: "+doubleSummarystatistics.getMin());
System.out.println("max: "+doubleSummarystatistics.getMax());
System.out.println("sum: "+doubleSummarystatistics.getSum());
System.out.println("ave: "+doubleSummarystatistics.getAverage());
```

##### 输出结果：

```java
DoubleSummaryStatistics{count=1000000, sum=500292.313874, min=0.000000, average=0.500292, max=1.000000}
count: 1000000
min: 2.2396595011908715E-7
max: 0.9999995590575925
sum: 500292.3138742163
ave: 0.5002923138742162
```

### 一、采用collect方法的三参数形式

```java
doubleSummarystatistics =
        Arrays.asList(team,team1,team2,team3,team4,team5).stream().peek(System.out::println
).mapToDouble(Team::getSalary).collect(DoubleSummaryStatistics::new, DoubleSummaryStatistics::accept, DoubleSummaryStatistics::combine);

System.out.println(doubleSummarystatistics);
System.out.println("DoubleSummaryStatistics的实例 Team count: = ￥ "+doubleSummarystatistics.getCount());
System.out.println("DoubleSummaryStatistics的实例 Team min: = ￥"+doubleSummarystatistics.getMin());
System.out.println("DoubleSummaryStatistics的实例 Team max: = ￥"+doubleSummarystatistics.getMax());
System.out.println("DoubleSummaryStatistics的实例 Team sum: = ￥"+doubleSummarystatistics.getSum());
System.out.println("DoubleSummaryStatistics的实例 Team ave: = ￥"+doubleSummarystatistics.getAverage());
```

##### 输出结果：

```java
DoubleSummaryStatistics{count=6, sum=858452252.000000, min=62094433.000000, average=143075375.333333, max=245269535.000000}
collect方法的三参数形式 DoubleSummaryStatistics的实例 Team count: = ￥ 6
collect方法的三参数形式 DoubleSummaryStatistics的实例 Team min: = ￥6.2094433E7
collect方法的三参数形式 DoubleSummaryStatistics的实例 Team max: = ￥2.45269535E8
collect方法的三参数形式 DoubleSummaryStatistics的实例 Team sum: = ￥8.58452252E8
collect方法的三参数形式 DoubleSummaryStatistics的实例 Team ave: = ￥1.4307537533333334E8
```

##### 源码分析：

本例中，collect方法通过构造函数引用来提供DoubleSummaryStatistics的实例，通过accept
// 方法将另一个值添加到现有的DoubleSummaryStatistics对象，以及通过combine方法将两个单独的DoubleSummaryStatistics对象合二为一。

### 二、采用下游收集器

```java
doubleSummarystatistics =
        Arrays.asList(team,team1,team2,team3,team4,team5).stream().collect(Collectors.summarizingDouble(Team::getSalary));
System.out.println(doubleSummarystatistics);
System.out.println("游收集器 Collectors.summarizingDouble Team count: = ￥ "+doubleSummarystatistics.getCount());
System.out.println("游收集器 Collectors.summarizingDouble Team min: = ￥"+doubleSummarystatistics.getMin());
System.out.println("游收集器 Collectors.summarizingDouble Team max: = ￥"+doubleSummarystatistics.getMax());
System.out.println("游收集器 Collectors.summarizingDouble Team sum: = ￥"+doubleSummarystatistics.getSum());
System.out.println("游收集器 Collectors.summarizingDouble Team ave: = ￥"+doubleSummarystatistics.getAverage());
```

##### 输出结果：

```java
DoubleSummaryStatistics{count=6, sum=858452252.000000, min=62094433.000000, average=143075375.333333, max=245269535.000000}
游收集器 Collectors.summarizingDouble Team count: = ￥ 6
游收集器 Collectors.summarizingDouble Team min: = ￥6.2094433E7
游收集器 Collectors.summarizingDouble Team max: = ￥2.45269535E8
游收集器 Collectors.summarizingDouble Team sum: = ￥8.58452252E8
游收集器 Collectors.summarizingDouble Team ave: = ￥1.4307537533333334E8
```

