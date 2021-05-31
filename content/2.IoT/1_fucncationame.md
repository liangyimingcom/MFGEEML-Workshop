---
title: "配置AWS IoT 环境"
chapter: false
weight: 21
---


进入AWS IoT 控制台

在左侧Greengrass中找到(经典版V1),在组中找到前面创建的Greengrass组
![](/images/IoT/GGroup.png)
点击组名称进入配置界面

在部署选项中,找到右上方点击**部署**选项,点击部署
![](/images/IoT/deployGG.png)
在配置设备搜索您的核心的方式点击**自动检测**

等待完成,左上方会由正在进行转变为已成功完成.
成功完成表示Greenngrass组部署成功


接下来点击**资源**选项
![](/images/IoT/Resources.png)
点击添加本地资源--**选择本地资源**
在附加本地资源中选择**LocalVolumeResourceData**
![](/images/IoT/lambda10.png)
点击完成后保存,再次点击部署,等待部署完成.

![](/images/IoT/deploygg2.png)

在控制台左侧菜单中点击**测试**选项.
![](/images/IoT/test1.png)
在订阅主题中的主题筛选条件中输入,*sensor/out*

![](/images/IoT/test2.png)

稍等片刻,订阅窗口就会有消息产生
![](/images/IoT/test3.png)

