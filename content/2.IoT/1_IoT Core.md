---
title: "配置AWS IoT 设备环境(10 min)"
chapter: false
weight: 21
---

在此部分我们将完成IoT设备的数据模拟生成工作

首先进入AWS IoT 控制台

在左侧Greengrass中找到(经典版V1),在组中找到之前创建的Greengrass组
![](/images/IoT/greengrassgroup.png)

点击组名称进入配置界面

在Greengrass 组的配置界面中点击**Lambda**,点击 lambda 名称,如**e2e_gg_data_gen**

![](/images/IoT/GGLambda1.png)

在接下来的界面中左侧找到资源,并点击,在资源选项中找到**添加本地资源**

![](/images/IoT/GGlambda2.png)

在接下来的添加本地资源的界面中选择 **选择本地资源**

![](/images/IoT/GGlambda3.png)

在接下来的界面中点击**选择**,找到并选择LocalVolumeResourceData资源,选择只读访问权限
![](/images/IoT/GGlambda4.png)
点击**完成**并**保存**

返回到Greengrass组的选项中,找到部署选项点击**部署**

![](/images/IoT/e2egggroup1.png)

如果提示 -配置设备搜索您的核心的方式-,点击**自动检测**

稍等片刻提示成功部署已成功完成即可

![](/images/IoT/e2egggroup2.png)

接下来在IoT 控制台中找到**测试**-- **MQTT 测试客户端**
在**主题筛选条件** 中填入 # 即可以看到设备有消息发送

![](/images/IoT/e2egggroup3.png)

至此我们完成了IoT模拟设备和数据发送的的初始化工作.