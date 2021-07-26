---
title: "准备环境"
chapter: false
weight: 20
---

在本环节中，需要在 S3 上创建：

1个存储桶：aws-athena-query-results-<*yourname*>-us-east-1

3个临时文件夹：在实验1部分创建的存储桶 e2eworkshop-e2edatas3bucket-<*XX*>下创建：data_brew_out, data_output, athena_output



1， 在 AWS 管理控制台的 服务搜索框中，输入：S3，点击 ’**S3**’

2， 进入S3控制台，点击 ’**创建存储桶**’

![](/images/LakeHouse/3_0_1_CreateS3Bucket.png)

做如下修改：

| 项目         | 配置项                        | 备注 |
| -------------------- | -------------------------------- | -------------------- |
| 存储桶名称           | aws-athena-query-results-<*yourname*>-us-east-1 |  |
| AWS 区域: （默认值） | 美国东部(弗吉尼亚北部) us-east-1 |  |

3， 点击<创建存储桶>

4， 在S3控制台中，搜索并点击：e2eworkshop-e2edatas3bucket-<*XX*>开头的存储桶，点击 ’**创建文件夹**’，做如下修改：

| 项目       | 配置项        | 备注 |
| ---------- | ------------- | ---- |
| 文件夹名称 | data_brew_out |      |

5， 点击 ’**创建文件夹**’

6， 重复步骤4，再创建如下文件夹：data_output, athena_output

7， 登陆到ec2上，使用s3 cp命令将模拟数据上传到S3上

~~~ bash
aws s3 cp s3://jack-lab/e2e/10000871.csv s3://jack-lab/e2e/data_source/10000871.csv
~~~

