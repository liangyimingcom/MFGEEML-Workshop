---
title: "使用 Athena 对处理后数据进行查询验证(5 min)"
chapter: false
weight: 70
---

61， 切换至 Athena 窗口
将如下命令复制到查询编辑器的窗口中，替换窗口中所有已有的字符，之后点击 ’**运行查询**’。

~~~
SELECT COUNT(1) as TotalCount FROM "e2e-workshop"."data_output";
~~~
结果窗口中将显示表 ‘data_output’ 中的数据总条数。

62， 将如下命令复制到查询编辑器的窗口中，替换窗口中所有已有的字符，之后点击 ’**运行查询**’。

~~~
SELECT COUNT (1) as TotalCount FROM "e2e-workshop"."data_output" where SYSTEM_CONDSIDETEMPIN>24;
~~~
结果窗口中将显示表 ‘data_output’ 中，SYSTEM_CONDSIDETEMPIN值大于24的记录条数。请记录本次查询的运行时间和扫描数据量。您应该看到类似下面的结果：(运行时间: 0.65 秒, 扫描的数据: 253 KB)。

【注意】对比这里的扫描时间和扫描的数据量与之前的差异。(运行时间和扫描的数据量明显减少了)
