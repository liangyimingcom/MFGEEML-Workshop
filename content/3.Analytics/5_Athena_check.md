---
title: "使用Athena对原始数据进行查询(5 min)"
chapter: false
weight: 50
---

36， 切换至 Athena 窗口

将如下命令复制到查询编辑器的窗口中，替换窗口中所有已有的字符，之后点击 ’运行查询’。

~~~
SELECT COUNT(1) as TotalCount FROM "e2e-workshop"."data_source";
~~~

结果窗口中将显示表 ‘data_source’ 中的数据总条数。

37， 将如下命令复制到查询编辑器的窗口中，替换窗口中所有已有的字符，之后点击’运行查询’。

~~~
SELECT COUNT (1) as TotalCount FROM "e2e-workshop"."data_source" where code='500304';
~~~

结果窗口中将显示表 ‘data_source’ 中错误代码为500304的记录条数。请记录本次查询的运行时间和扫描数据量。您应该看到类似下面的结果：(运行时间: 1.48 秒, 扫描的数据: 1.09 GB)。
