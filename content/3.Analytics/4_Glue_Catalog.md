---
title: "使用 Glue 对元数据进行管理(10 min)"
chapter: false
weight: 40
---

在这个任务中，我们将使用 AWS Glue 的爬虫功能爬取 S3 中的数据的元数据，并在 Glue 的元数据仓库中建立表定义。

22， 在 AWS 管理控制台的 服务搜索框中，输入：glue，点击 ‘**AWS Glue**’

23， 在左侧菜单中选择 ‘爬网程序’，点击蓝色 ‘**添加爬网程序**’ 按钮。

24， 输入爬网程序的名字：e2e-workshop-crawler，点击 ‘**下一步**’。

25， Specify crawler source type，保持默认，点击 ‘**下一步**’

26， 添加数据存储，做如下修改，点击 ‘**下一步**’

| 项目         | 配置项                                           | 备注 |
| ------------ | ------------------------------------------------ | ---- |
| 爬行数据位于 | 我的账户中的指定路径                             |      |
| 包含路径     | s3://e2eworkshop-e2edatas3bucket-<*XX*>/labdata/ |      |

27， 添加另一个数据存储，保持默认（否），点击 ‘**下一步**’

28， 使用 ‘创建IAM角色’ 选项，输入：’e2e-workshop-crawler’，点击 ‘**下一步**’。

29， 为此爬网程序创建计划，保持默认（按需运行），点击 ‘**下一步**’

30， 配置爬网程序的输出，点击 ‘**添加数据库**’，做如下设置，点击 ’创建’，点击 ‘**下一步**’

| 项目       | 配置项       | 备注 |
| ---------- | ------------ | ---- |
| 数据库名称 | e2e-workshop |      |

31，    预览如果没有问题，点击 ‘**完成**’

32，    选择刚刚建立的爬网程序e2e-workshop-parquet-crawler，点击 ‘**运行爬网程序**’ 按钮。（该过程需要几分钟时间）  

33，    选择 ‘添加数据库’，数据库名称：’e2e-workshop’，点击 ‘创建’，点击 ‘**下一步**’

34，    选择刚刚建立的爬网程序e2e-workshop-crawler，点击 ‘**运行爬网程序**’ 按钮。（该过程需要几分钟时间）

35，    运行完毕后，点击页面上方提示信息中的数据库名称：e2e-workshop，可以看到新创建了1张表：labdata。现在，可以检查这张表的相关信息。

