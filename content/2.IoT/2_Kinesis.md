---
title: "配置AWS IoT 数据转存储"
chapter: false
weight: 22
---
在此部分中,我们需要将设备上传的数据转存储到S3中,并在存储过程中对其进行修正和格式化.

我们使用AWS IoT core规则引擎和Kinesis Firehose作为IoT数据转存储的服务.

转到AWS IoT 服务界面,找到[规则](https://us-east-1.console.aws.amazon.com/iot/home?region=us-east-1#/rulehub)

点击**创建规则**

在创建规则的界面中按如下进行配置
![](/images/IoT/iotcreaterule.png)

| 项目 | 配置项 | 备注 |
| ----- | :-: | ---: |
| 名称    | e2eIoTRule  | 可自定义  |
| 描述    | IoT to kinesis and IoT analytic |  可选 |
| 规则查询语句    | SELECT * FROM 'sensor/out' |[参考文档](https://docs.aws.amazon.com/console/iot/iot-sql-reference)|

在下方**设置一个或多个操作**处,点击添加操作

在**设置一个或多个操作**中找到**添加操作**

选择将消息发送到 Amazon Kinesis firehose流
![](/images/IoT/rule1.png)

点击**配置操作**

在配置操作界面,选择创建新资源.

- 在Amazon Kinesis界面中点击创建传输流,在传输流名称中输入传输流名称例如**IoT2S3**其他保持默认
- 点击**下一步**
- 在使用 AWS Lambda 转换源记录--源记录转换,选择**已启用**,并选择以e2eWorkshop-IoTanalytics-IoT2S3LambdaXX开始的Lambda函数,其余保持默认
- 点击**下一步**
- 在目标中,我们选择Amazon S3作为目标
- 在S3存储桶中 我们选择前期Cloudformation创建的存储桶,以e2eworkshop-e2edatas3bucket-XX开头,其他保持默认
- 点击**下一步**
- 在配置设置页面中可以选择缓冲条件,间隔,压缩和加密方式等,我们这里将缓冲区大小修改为**50M**,在下方权限选项中,创建或更新IAM角色,其他保持默认
- 点击**下一步**
- 点击**创建传送流**

回到IoT规则页面的配置操作中,找到上一步创建的Amazon Kinesis Firehose 流
- 在流名称中选择之前创建的IoT2S3流
- 在分隔符中,我们选择 **无** 分隔符
- 在下方角色选项中点击创建角色,输入角色名称如IoT2S3_Role后点击**创建**
- 点击**添加操作**
- 点击**创建规则**

![](/images/IoT/rule2.png)

至此,IoT数据到S3的规则创建完成.稍后我们就可以在指定的S3存储桶中看到转换后的数据
![](/images/IoT/s3data.png)







 

