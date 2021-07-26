---
title: "系统架构"
chapter: false
weight: 10
---

完成本实验后，您搭建的数据湖将如以下架构图所示：



![](/images/LakeHouse/3_0_0_arch.png)

采集到的传感器数据存放在 S3 中央存储中；实时数据也不断通过 Kinesis 套件注入到 S3；我们将会：

1. 使用 AWS Glue DataBrew 对原始数据进行预览和完整性检查

2. 使用 AWS Glue 对数据进行元数据管理和数据 ETL

3. 使用 Athena 对数据进行 ad hoc 查询，验证数据准确性

