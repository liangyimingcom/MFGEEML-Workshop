---
title: "使用 Glue 对数据进行变形以便优化查询(30 min)"
chapter: false
weight: 60
---

在这个任务中，我们将使用 AWS Glue 的任务功能，将 S3 中的 csv 格式数据转换为 Parquet 格式，从而优化 sql 查询效率。

38， 在 AWS 管理控制台的 服务搜索框中，输入：glue，点击 ‘**AWS Glue**’

选择界面左侧的作业，点击 ‘**添加作业**‘。

39， 做如下修改，点击 ‘**下一步**’

| 项目    | 配置项                                  | 备注 |
| ------- | --------------------------------------- | ---- |
| 名称    | e2e-parquet-job                         |      |
| IAM角色 | AWSGlueServiceRole-e2e-workshop-crawler |      |

40， 选择一个数据源，labata 位于 e2e-workshop中，点击 ‘**下一步**’

41， 选择转换类型，保持默认，点击 ‘**下一步**’

42， 选择一个数据目标，选择 ‘在数据目标中创建表’，做如下修改，点击 ‘**下一步**’

| 项目     | 配置项                                              | 备注 |
| -------- | --------------------------------------------------- | ---- |
| 数据存储 | Amazon S3                                           |      |
| 格式     | Parquet                                             |      |
| 目标路径 | s3://e2eworkshop-e2edatas3bucket-<*XX*>/data_output |      |

43， Output Schema Definition，点击 ‘**保存作业并编辑脚本**’

44， 【选做】检查Glue自动生成的代码，在倒数第二行的connection_options中增加参数"partitionKeys": ["code"]，并与前一参数”Path”用逗号与空格隔开。**(注意：如下代码中，需要将<*XX*>修改为账号中S3路径对应的字符串)**

~~~Plaintext
datasink4 = glueContext.write_dynamic_frame.from_options(frame = dropnullfields3, connection_type = "s3", connection_options = {"path": "s3://e2eworkshop-e2edatas3bucket-<XX>/data_output", "partitionKeys": ["code"]}, format = "parquet", transformation_ctx = "datasink4")
~~~
45， 点击 ‘**保存**’，’**运行作业**’。（该过程需要几分钟时间）观察是否失败了？

失败了：思考是什么原因？（之前创建的IAM角色：AWSGlueServiceRole-e2e-workshop-crawler缺少对S3目录s3://e2eworkshop-e2edatas3bucket-<*XX*>/data_output的访问权限，导致失败。所以现在为其增加相应权限）

46， 在 AWS 管理控制台的 服务搜索框中，输入：iam，点击 ‘**IAM**’

47，    左侧点击角色，右侧搜索框中，输入：AWSGlueServiceRole-e2e-workshop-crawler，在搜索结果列表中点击该角色

48，    点击策略名称 ‘AWSGlueServiceRole-e2e-workshop-crawler’

![](/images/LakeHouse/3_6_0_glue_etl_iam.png)

49，    点击 ‘**编辑策略**’，’JSON’，使用如下json串覆盖原有的内容

~~~json
{
  "Version": "2012-10-17",
  "Statement": [
		{
				"Sid": "VisualEditor0",
				"Effect": "Allow",
				"Action": [
					"s3:PutObject",
					"s3:GetObject",
					"s3:DeleteObject"
				],
				"Resource": "*"
		}
	]
}
~~~

点击 ‘**查看策略**’，’保存修改’

回到 Glue 服务界面，ETL/作业/e2e-parquet-job/操作/运行作业，再次运行：e2e-parquet-job

50，    当 e2e-parquet-job 运行完毕后，在左侧菜单中选择 ‘爬网程序’，点击蓝色 ‘**添加爬网程序**’ 按钮。

51，    输入爬网程序的名字：e2e-workshop-parquet-crawler，点击 ‘**下一步**’

52，    Specify crawler source type，保持默认，点击 ‘**下一步**’

53，    添加数据存储，做如下修改，点击 ‘**下一步**’

| 项目         | 配置项                                              | 备注 |
| ------------ | --------------------------------------------------- | ---- |
| 爬行数据位于 | 我的账户中的指定路径                                |      |
| 包含路径     | s3://e2eworkshop-e2edatas3bucket-<*XX*>/data_output |      |

54，    添加另一个数据存储，保持默认（否），点击 ‘**下一步**’

55，    选择一个 IAM 角色，AWSGlueServiceRole-e2e-workshop-crawler，点击 ‘**下一步**’

56，    为此爬网程序创建计划，保持默认，点击 ‘**下一步**’

57，    配置爬网程序的输出，做如下修改，点击 ‘**下一步**’

| 项目   | 配置项       | 备注 |
| ------ | ------------ | ---- |
| 数据库 | e2e-workshop |      |

58，    预览如果没有问题，点击 ‘**完成**’

59，    选择刚刚建立的爬网程序e2e-workshop-parquet-crawler，点击 ‘**运行爬网程序**’ 按钮。（该过程需要几分钟时间）

60，    运行完毕后，点击页面上方提示信息中的数据库名称：e2e-workshop，可以看到新创建的1张表：data_output。现在，可以检查这张表的相关信息。
