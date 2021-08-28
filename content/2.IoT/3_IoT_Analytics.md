---
title: "配置AWS IoT Analytics 进行数据展示(20min)"
chapter: false
weight: 23
---
接下来我们将使用AWS IoT Analytics对数据进行预处理和转存储,并结合Cloudwatch对特定的指标进行监控.

在AWS 控制台中找到AWS IoT Analytics或者直接点击
[AWS IoT Analytics](https://console.aws.amazon.com/iotanalytics/home?region=us-east-1#)

进入第一次运行界面,进行以下配置

| 名称 | 配置 | 备注 |
| ----- | :-: | ---: |
| 资源前缀    | e2eWorkshop |  可自定义 |
| MQTT 主题    | sensor/out |   |

点击**快速创建**,或**创建资源**,等待创建完成


接下来我们在AWS IoT 规则引擎中,增加IoT 消息到 AWS IoT Analytics的规则.

回到AWS IoT 服务界面,找到[规则](https://console.aws.amazon.com/iot/home?region=us-east-1#/rulehub)

我们使用前期创建的e2eIoTRule规则

点击**添加操作**

在添加操作中找到**向IoT Analytics发送消息**,点击配置操作
![](/images/IoT/iotrule3.png)

在配置页面中,选择手动选择手动选择 IoT Analytics 通道和角色
- 在通道名称中选择,前期创建的通道名称 e2eworkshop_channel
- 在角色中选择 e2eworkshop_role,并点击**更新角色**.
  
点击**添加操作**

点击**创建规则**

![](/images/IoT/iotrule4.png)

至此,AWS IoT Analytics的初始化工作完成,接下来我们利用Cloudwatch监控设备上的指标


找到前期创建的管道e2eworkshop_pipeline,找到**活动**

![](/images/IoT/pipline1.png)



在下方找到**活动**,点击**添加活动**

在编辑活动中按如下步骤配置:
1. **消息属性**中可以预览在Payload中的属性.这一步保持默认,点击**下一步**
2. 在**管道活动**中,选择一个活动中选择**使用Lambda转换消息**,并点击下方**添加**
   ![图 3](/images/IoT/1629878614937.png)  

3. 在下方**使用 Lambda 函数转换消息**中Lambda 函数 中选择以e2eWorkshop-IoT2CWLambdaXX开头的Lambda函数,其他选项保持默认,点击**下一步**.
   ![图 4](/images/IoT/1629878657810.png)  

4. 点击**更新**


稍等5分钟左右等待数据打入到Cloudwatch中.

接下来转到Cloudwatch服务,或点击[Cloudwatch](https://console.aws.amazon.com/cloudwatch/home?region=us-east-1#metricsV2:graph=~())

在左侧指标中找到指标,在自定义命名空间中可以看到E2EIoT/Monitor这个命名空间.

接下来,我们转到左侧[Cloudwatch的控制面板](https://console.aws.amazon.com/cloudwatch/home?region=us-east-1#dashboards:)中,
- 点击创建控制面板
- 在新建控制面板名称中输入你需要创建的控制面板名称,例如*E2E-Dashboard*,点击创建控制面板
- 由于我们监控的指标中大部分是随时间变化的指标,在小部件中可以选择线性图,如果指标为其他数值也可以选择其他部件,点击**下一步**
- 在您希望从哪个数据源来创建小部件？页面中,我们选择指标作为数据源,点击 **配置**
- 在配置页面,找到我们前期创建的E2EIoT/Monitor命名空间,在其中选择一些指标作为展示
![图 5](/images/IoT/1629879421528.png)  
如果需要快速看到结果,可以将指标的刷新频段从默认5分钟调整为10秒
![图 7](/images/IoT/1629879619192.png)  

- 点击创建小部件,即可完成Dashboard的创建,后期也可以根据监控的数据不同调整小部件的大小和内容

*说明:如果需要调整观察的参数指标,可以在e2eWorkshop-IoT2CWLambda 这个lambda这个函数的环境变量中调整.*

至此本章节结束,完成IoT设备的模拟,数据发送,数据转换以及数据展示.



 

