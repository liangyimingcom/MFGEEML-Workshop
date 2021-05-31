---
title: "构建AWS和边缘端设备环境"
chapter: false
weight: 20
---

设备数据上云（IoT）：程序模拟设备数据 → IoT GG → IoT Core → Rule Engine → IoT Analytics→S3。通过Cloudwatch做大屏展示

这一阶段我们使用AWS Cloudformation 构建基础环境，通过本Cloudformation模版可以一键部署如下资源
1. 创建VPC 并配置基本的网络设置
2. 启动一个EC2 实例安装Greengrass,并启动服务
3. 一个Lambda用来模拟设备端产生数据
#### 1.1 登录控制台
首先登录区 [AWS中国](https://console.amazonaws.cn/console/home?region=cn-north-1#)账号，在登录界面输入，账户，用户名，密码登录
![](/images/IoT/1login.png)

进入Cloudformation服务,[或直接点击此链接创建](https://console.amazonaws.cn/cloudformation/home?region=cn-north-1#/stacks/quickcreate?templateURL=https://pdm-iotworkshop.s3.cn-north-1.amazonaws.com.cn/cfn/greengrass_cfn_cn_v7&stackName=PDMIoTWorkshop)


在参数部分,可以保留默认,keypair处选择前期创建的EC2Key Pair即可.
![](/images/IoT/2key.png)

在最下方选中**我确认，AWS CloudFormation 可能创建 IAM 资源**,然后点击创建堆栈即可
![](/images/IoT/creatstack.png)

稍等片刻等待创建完毕

![](/images/IoT/stacksuccess.png)


这是在AWS IoT 控制台--Greengrass--组 中可以找到已创建的gg_cfn组

![](/images/IoT/gggroup.png)


