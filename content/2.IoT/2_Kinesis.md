---
title: "配置AWS IoT 数据转存储 (20 min)"
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

在创建传输流界面中
- 源 选择**Direct PUT**
- 目标 选择 **Amazon S3**
- 传输流名称输入自定义的传输流名称 如 **IoT2S3**
- 在变换和转换记录下面的数据转换选项选择**已启用**
    - 在AWS Lambda函数 点击浏览到前期以e2eWorkshop-IoT2S3LambdaXX开始的Lambda函数
![图 1](/images/IoT/1629875920578.png)  
- 在下方目标设置中
    - S3 存储桶选择我们选择前期Cloudformation创建的,以e2eworkshop-e2edatas3bucket-XX开头的存储桶
![图 2](/images/IoT/1629876106461.png) 
- 其余保持默认,点击**创建传输流**




回到IoT规则页面的配置操作中,找到上一步创建的Amazon Kinesis Firehose 流
- 在流名称中选择之前创建的IoT2S3流
- 在分隔符中,我们选择 **无** 分隔符
- 在下方角色选项中点击创建角色,输入角色名称如IoT2S3_Role后点击**创建**
- 点击**添加操作**
- 点击**创建规则**

![](/images/IoT/rule2.png)

至此,IoT数据到S3的规则创建完成.稍后我们就可以在指定的S3存储桶中看到转换后的数据
![](/images/IoT/s3data.png)







 

