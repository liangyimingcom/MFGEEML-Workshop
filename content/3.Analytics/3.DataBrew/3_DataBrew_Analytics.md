---
title: "Data Brew - Analytics"
chapter: false
weight: 30
---

18，    点击 ’**刨析**’，’**运行数据刨析**’

![](/images/LakeHouse/3_1_6_brew_analytics-s3.png)

![](/images/LakeHouse/3_1_6_brew_analytics-iam.png)

做如下修改：

| 作业运行样本/数据样本/自定义样本 | 修改为2000（加速实验过程）                    |
| -------------------------------- | --------------------------------------------- |
| 作业输出设置/S3位置              | s3://<*yourname*>-e2e-workshop/data_brew_out/ |
| 权限/角色名称：(选择之前创建的)  | AWSGlueDataBrewServiceRole-e2e-workshop       |

19，    点击 ‘**创建并运行作业**’ (该过程需要持续几分钟)

20，    点击 ‘**作业**’，’**刨析作业**’，可以看到该作业正在运行

21，    点击 ‘**数据集**’，’e2e-workshop-dataset’，即可查看刚才创建的数据集的基本情况，列统计信息等。
