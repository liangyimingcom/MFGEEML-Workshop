---
title: "构建IoT设备和数据环境 (10 Min)"
chapter: false
weight: 20
---
AWS IoT 提供云服务将 IoT 设备连接到其他设备和 AWS 云服务。AWS IoT 提供设备软件以帮助您将 IoT 设备集成到基于 AWS IoT 的解决方案。在这个部分中,我们将构建一个模拟环境用来模拟设备并发出模拟的传感器数据,传感器数据进入AWS IoT Core后我们使用Kinesis和AWS IoT Analytics进行数据的处理.

完成本实验后，您搭建的IoT设备和数据环境将如下架构图所示：
![](/images/IoT/Arc.png)

1. 使用AWS IoT Greengrass 模拟设备并发送数据至AWS IoT Core
2. AWS IoT Core 接收消息并通过规则引擎分发至Amazon Kinesis Firehose和AWS IoT Analytics
3. Amazon Kinesis Firehose将消息以流式数据处理并转换为CSV格式存储至S3中
4. AWS IoT Analytics对数据内容进行处理并结合Cloudwatch做实时展现


这一阶段我们使用AWS Cloudformation 构建基础环境，通过本Cloudformation模版可以一键部署如下资源
1. 创建VPC 并配置基本的网络设置
2. 启动一个EC2 实例安装Greengrass,并启动服务
3. 一个Lambda用来部署到Greengrass并模拟设备端产生数据
4. 用于存储数据的存储桶(以e2eworkshop-e2edatas3bucketXXX 开头)
5. 其他依赖的Lambda函数


#### 1.1 登录控制台
首先使用eventengine的AWS Console 跳转或登录 [AWS美东1区域](https://us-east-1.console.aws.amazon.com/console/home?region=us-east-1)在登录界面输入，账户，用户名，密码登录

接下来进入Cloudformation服务,导入Cloudformation模板或
[直接点击此链接直接创建](https://us-east-1.console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/quickcreate?templateURL=https://pdm-workshop-ue1.s3.amazonaws.com/cfn/e2eworkshop_final.yml&stackName=e2eWorkshop)


在参数部分,可以保留默认,也可以自定义Core设备名称,keypair处选择ee-default-keypair
![](/images/IoT/createstack1.png)

在最下方选中**我确认，AWS CloudFormation 可能创建 IAM 资源**,然后点击创建堆栈即可
![](/images/IoT/creatstack.png)
稍等片刻等待创建完毕,
![](/images/IoT/createstack2.png)

这时在AWS IoT 控制台--Greengrass--组 中可以找到已创建的e2e_gg组

![](/images/IoT/greengrassgroup.png)

至此,IoT 设备的基础环境已构建完成.

