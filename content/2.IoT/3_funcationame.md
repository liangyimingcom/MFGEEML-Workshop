---
title: "配置AWS IoT Analytics 和监控环境"
chapter: false
weight: 23
---
接下来我们将使用AWS IoT Analytics对数据进行预处理和转存储,并结合Cloudwatch对特定的指标进行监控.
在AWS 控制台中找到AWS IoT Analytics或者点击
[AWS IoT Analytics]([https://link](https://console.amazonaws.cn/iotanalytics/home?region=cn-north-1#/first-run))

进入第一次运行界面,

在资源名称中可以为资源起一个名字例如PDMWorkshop

在MQTT主题里输入sensor/out

点击**快速创建**,等待创建完成
![](/images/IoT/AIA1strun.png)

接下来我们在AWS IoT 规则引擎中,增加IoT 消息到 AWS IoT Analytics的规则.

回到AWS IoT 服务界面,找到[规则](https://console.amazonaws.cn/iot/home?region=cn-north-1#/rulehub)

我们使用前期创建的IoT2Analytics规则

在添加操作中找到向IoT Analytics发送消息
![](/images/IoT/2iotanalytics.png)

点击**配置操作**,在配置页面中,选择手动选择手动选择 IoT Analytics 通道和角色
- 在通道名称中选择,前期创建的通道名称 pdmworkshop_channel
- 在角色中选择 pdmworkshop_role,并点击更新角色.
  
点击**添加操作**

点击**创建规则**

至此,AWS IoT Analytics的初始化工作完成,接下来我们利用Cloudwatch监控设备上的指标


点击 [IoTDashboard](https://console.amazonaws.cn/cloudformation/home?region=cn-north-1#/stacks/quickcreate?templateURL=https://pdm-iotworkshop.s3.cn-north-1.amazonaws.com.cn/cfn/IoTDashboard.yaml&stackName=IoTDashboard)
创建需要的Lambda函数.


点击确认创建
![](/images/IoT/iotdashboardcreate.png)

等待创建完成.

转到 [AWS IoT Analytics](https://console.amazonaws.cn/iotanalytics/home?region=cn-north-1)

找到前期创建的管道pdmworkshop_pipeline,在活动中,点击**编辑**
![](/images/IoT/pipline1.png)
在接下来界面你可以对其中的字段做删除或者丰富操作,这里我们点击**下一步**

在管道活动中点击**添加活动**,在添加活动中找到 **使用Lambda函数转换消息**

![](/images/IoT/dpipline2.png)

在下方,**使用 Lambda函数转换消息** 

选项中找到IoTDashboard-IoT2CWLambda-开头的Lambda函数
点击更新预览,如果没有报错,说明Lambda成功触发,点击最下方的保存更改.
![](/images/IoT/dpipline3.png)

如果出现重新处理通过管道的数据,点击**开始重新处理**

接下来转到Cloudwatch服务,[Cloudwatch](https://console.amazonaws.cn/cloudwatch/home?region=cn-north-1#metricsV2:graph=~())

在左侧指标中找到指标,在自定义命名空间中可以看到PDMIoT/Monitor这个命名空间.

接下来,我们转到左侧[Cloudwatch的控制面板](https://console.amazonaws.cn/cloudwatch/home?region=cn-north-1#dashboards:)中,
- 点击创建控制面板
- 在新建控制面板名称中输入你需要创建的控制面板名称,例如*PDM-Dashboard*,点击创建控制面板
- 由于我们监控的指标中大部分是随时间变化的指标,在小部件中可以选择线性图,如果指标为其他数值也可以选择其他部件,点击**下一步**
- 在您希望从哪个数据源来创建小部件？页面中,我们选择指标作为数据源,点击 **配置**
- 在配置页面,找到我们前期创建的PDMIoT/Monitor命名空间,在其中选择一些指标作为展示
![](/images/IoT/dashboard.png)
点击创建小部件,即可完成Dashboard的创建,后期也可以根据监控的数据不同调整小部件的大小和内容
![](/images/IoT/Dashboard2.png)








 

