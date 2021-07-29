---
title: "Data Brew - 创建项目"
chapter: false
weight: 10
---

8， 在 AWS 管理控制台的 服务搜索框中，输入：databrew，点击 ‘**AWS Glue DataBrew**’

9， 进入DataBrew 控制台，点击’**创建项目**’

![](/images/LakeHouse/3_1_0_brew_create_project.png)

做如下修改：

| 项目名称 | e2e-workshop-databrew |
| -------- | --------------------- |
| 配方名称 | 保持默认              |

10， 选择一个数据集，点击 ‘**新数据集**’

![](/images/LakeHouse/3_1_1_brew_dataset.png)

做如下修改：

| 数据集名称 | e2e-workshop-dataset |
| ---------- | -------------------- |

11， 连接到新的数据集,

![](/images/LakeHouse/3_1_2_brew_dataset_source.png)

做如下修改：

| 输入来自S3的源 | s3://e2eworkshop-e2edatas3bucket-<*XX*>/<*Year*>/<*Month*>/<*Day*>/ |
| -------------- | ------------------------------------------------------------ |

12， 在下方列出的文件中，选择之前复制的数据源：e2e_workshop.csv

13， 其它配置：

![](/images/LakeHouse/3_1_3_brew_dataset_csv.png)

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

点击‘**创建项目**’
