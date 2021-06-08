---
title: "准备环境"
chapter: false
weight: 32
---

1， 在 AWS 管理控制台的 服务搜索框中，输入：S3，点击 ’S3’

2， 进入S3控制台，点击 ’创建存储桶’

![](/images/LakeHouse/3_0_1_CreateS3Bucket.png)

做如下修改：

| 存储桶名称           | <$\color{#00FF00}{yourname}$>``-``e2e-workshop |
| -------------------- | ---------------------------------------------- |
| AWS 区域: （默认值） | 美国东部(弗吉尼亚北部) us-east-1               |

3， 点击<创建存储桶>

4， 1， 在存储桶中创建目录，点击 ’创建文件夹’，做如下修改：

| 文件夹名称 | data_source |
| ---------- | ----------- |

5， 点击’创建文件夹’

6， 重复步骤2-4，再创建3文件夹：data_brew_out, data_output, athena_output

7， 登陆到ec2上，使用s3 cp命令将模拟数据上传到S3上

aws s3 cp s3://jack-lab/e2e/10000871.csv s3://jack-lab/e2e/data_source/10000871.csv
