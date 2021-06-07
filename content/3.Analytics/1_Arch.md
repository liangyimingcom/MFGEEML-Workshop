---
title: "应用程序架构"
chapter: false
weight: 31
---

# 应用程序架构

完成本实验后，您搭建的数据湖将如下： 

![img](file:////Users/jacktian/Library/Group Containers/UBF8T346G9.Office/TemporaryItems/msohtmlclip/clip_image001.png?lastModify=1623047408)

架构图所示：采集到的传感器数据存放在S3中央存储中；实时数据也不断通过Kinesis套件注入到S3；我们将会：

\1.   使用AWS Glue DataBrew对原始数据进行预览和完整性检查

\2.   使用AWS Glue对数据进行元数据管理和数据ETL

\3.   使用Athena对数据进行ad hoc查询，验证数据准确性

