---
title: "使用Data Brew进行数据预览和完整性检查(10min)"
chapter: false
weight: 33
---

8， 在 AWS 管理控制台的 服务搜索框中，输入：databrew，点击‘AWS Glue DataBrew’

9， 进入DataBrew 控制台，点击’创建项目’

![](/images/LakeHouse/3_1_0_brew_create_project.png)

做如下修改：

| 项目名称 | e2e-workshop-databrew |
| -------- | --------------------- |
| 配方名称 | 保持默认              |

10， 选择一个数据集，点击 ‘新数据集’

![](/images/LakeHouse/3_1_1_brew_dataset.png)

做如下修改：

| 数据集名称 | e2e-workshop-dataset |
| ---------- | -------------------- |

11， 连接到新的数据集,

![](/images/LakeHouse/3_1_2_brew_dataset_source.png)

做如下修改：

| 输入来自S3的源 | s3://<*yourname*>-e2e-workshop/data_source/ |
| -------------- | ------------------------------------------- |

12， 在下方列出的文件中，选择之前复制的数据源：e2e_workshop.csv

13， 其它配置：

![](/images/LakeHouse/3_1_2_brew_dataset_csv.png)

做如下修改：

| 所选文件的格式 | csv  |
| -------------- | ---- |

14， 采样（可选）：决定如何抽取数据进行统计分析

15， 权限：因为AWS将要访问您的数据，所以在这里，您需要通过一个IAM角色授权AWS允许访问您的数据

![](/images/LakeHouse/3_1_4_brew_iam.png)

做如下修改：

| 角色名称      | 创建新的IAM角色 |
| ------------- | --------------- |
| 新IAM角色后缀 | e2e-workshop    |

点击‘创建项目’

16， 等1-2分钟，控制台上会展示出如下主界面：我们可以获得数据集的概览，包括：所有的字段名/采样值/每个字段的数值分布情况/唯一性情况等。表格上方有250+开箱即用的数据处理方法，

![](/images/LakeHouse/3_1_5_brew_preview.png)

17，    点击 ’SCHEMA’，可以看到数据集的所有：列定义/数据质量/数值分布 等。在这里，可以针对每一列确定是否显示。

18，    点击 ’刨析’，’运行数据刨析’

![](/images/LakeHouse/3_1_6_brew_analytics.png)

做如下修改：

| 作业运行样本/数据样本/自定义样本 | 修改为2000（加速实验过程）                    |
| -------------------------------- | --------------------------------------------- |
| 作业输出设置/S3位置              | s3://<*yourname*>-e2e-workshop/data_brew_out/ |
| 权限/角色名称：(选择之前创建的)  | AWSGlueDataBrewServiceRole-e2e-workshop       |

19，    点击 ‘创建并运行作业’ (该过程需要持续几分钟)

20，    点击 ‘作业’，’刨析作业’，可以看到该作业正在运行

21，    点击 ‘数据集’，’e2e-workshop-dataset’，即可查看刚才创建的数据集的基本情况，列统计信息等。
