---
title: "准备SageMaker Studio环境"
chapter: false
draft: true
weight: 13
---



# DRAFT - 准备 SageMaker Studio 环境 (simple version)



Amazon SageMaker Studio 是用于机器学习的基于 Web 的集成开发环境 (IDE)，可让您构建、训练、调试、部署和监控机器学习模型。 Studio 提供了将模型从实验到生产所需的所有工具，同时提高您的生产力。



 AWS 账户已由您的 AWS 讲师预置好了，请按照以下步骤访问 SageMaker Studio 环境：

1. 打开 AWS 控制台并切换到您的讲师沟通的 AWS 区域。

{{% notice warning %}}
**弗吉尼亚** 如下图所示，但您也可以选择其他地区 [SageMaker Studio 可用。](https://docs.aws.amazon.com/sagemaker/latest/dg/studio.html) 正确的区域选择听讲师的。
{{% /notice %}}



[![img](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image22.png)](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image22.png)

2. 在服务下搜索**Amazon SageMaker**。

[![img](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image23.png)](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image23.png)

3. 在 **Get Started** 下，单击橙色按钮 **SageMaker Studio**。

[![img](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image41.png)](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image41.png)

4. 应该已经配置了 SageMaker Studio 环境。单击 **Open Studio**（在预配置的 **sagemakeruser** 用户名右侧）。

[![img](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image42.png)](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image42.png)

5. 首次访问 SageMaker Studio 时，页面可能需要 1 或 2 分钟才能加载。

[![img](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image30.png)](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image30.png)

6. 您将被重定向到一个新的 Web 选项卡，如下所示：

[![img](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image31.png)](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image31.png)

7. 在 **Notebooks 和计算资源** 下，确保选中 **Data Science** SageMaker 图像并单击 **Notebook - Python 3**。

[![img](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image32.png)](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image32.png)

8. 您将进入 **Untitled.ipynb** 笔记本。

[![img](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image33.png)](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image33.png)

9.您可以通过右键单击名称来重命名笔记本。

[![img](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image34.png)](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image34.png)

[![img](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image35.png)](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image35.png)

**恭喜！！** 您已成功启动 SageMaker Studio Notebook。





## 下载实验所需的GitHub仓库的内容

1. 在 SageMaker 笔记本中，单击 **Launch Terminal in current SageMaker Image** 图标。内核必须完全启动（**分享**按钮右侧的圆圈必须为空）才能点击图标。

[![img](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image36.png)](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image36.png)

2. 在终端中，键入以下命令：

``
git 克隆 https://github.com/aws-samples/amazon-sagemaker-immersion-day.git
``

[![img](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image37.png)](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image37.png)

3. 完成第 2 步后，您将在工作室的 **left panel** 中创建 **amazon-sagemaker-immersion-day** 文件夹：

[![img](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image38.png)](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image38.png)

**恭喜！！** 您已成功下载 SageMaker Immersion Day 的内容。
