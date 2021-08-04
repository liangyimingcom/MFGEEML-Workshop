---
title: "使用 Athena 对原始数据进行查询(5 min)"
chapter: false
weight: 50
---

36， 切换至 Athena 窗口。第一次使用 Athena，需要设置查询结果存放的 S3 位置。

在控制台右上角点击 '**设置**'，在弹出的窗口中，输入之前创建的 S3 桶的位置：

![](/images/LakeHouse/3_2_0_athena_set.png)

| 项目           | 配置项                                                 | 备注 |
| -------------- | ------------------------------------------------------ | ---- |
| 查询结果的位置 | s3://e2eworkshop-e2edatas3bucket-<*XX*>/athena_output/ |      |

将如下命令复制到查询编辑器的窗口中，替换窗口中所有已有的字符，之后点击 ’**运行查询**’。

~~~
SELECT COUNT(1) as TotalCount FROM "e2e-workshop"."labdata";
~~~

结果窗口中将显示表 ‘data_source’ 中的数据总条数。

37， 将如下命令复制到查询编辑器的窗口中，替换窗口中所有已有的字符，之后点击’**运行查询**’。

~~~
SELECT COUNT (1) as TotalCount FROM "e2e-workshop"."labdata" where code='500304';
~~~

结果窗口中将显示表 ‘data_source’ 中错误代码为500304的记录条数。请记录本次查询的运行时间和扫描数据量。您应该看到类似下面的结果：(运行时间: 1.11 秒, 扫描的数据: 526.89 MB)。
