---
title: "构建智能湖仓进行数据清洗"
chapter: false
weight: 30
---

## 智能湖仓（Lake House）

AWS为客户提供了基于S3的智能湖仓解决方案，包括：数据收集，存储，预览，数据处理和数据展现的各个环节。在本次实验中，我们利用xxx数据集，搭建一个设备故障数据分析平台，为后续第三部分的预测性维护做数据准备。这个分析平台提供针对采集到的设备数据进行存储，预览，清洗，ETL和分析等功能。在整个过程中，您将使用并了解AWS的DataBrew，Glue， Athena，等无服务器服务。

# 应用程序架构 

完成本实验后，您搭建的数据湖将如下： 

![img](file:////Users/jacktian/Library/Group%20Containers/UBF8T346G9.Office/TemporaryItems/msohtmlclip/clip_image001.png)

架构图所示：采集到的传感器数据存放在S3中央存储中；实时数据也不断通过Kinesis套件注入到S3；我们将会：

\1.   使用AWS Glue DataBrew对原始数据进行预览和完整性检查

\2.   使用AWS Glue对数据进行元数据管理和数据ETL

\3.   使用Athena对数据进行ad hoc查询，验证数据准确性

