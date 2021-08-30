---
title: "准备SageMaker Studio环境"
chapter: false
weight: 14
---

## 启动 Amazon SageMaker Studio

Amazon SageMaker Studio 是用于机器学习的基于 Web 的集成开发环境 (IDE)，可让您构建、训练、调试、部署和监控机器学习模型。 Studio 提供了将模型从实验到生产所需的所有工具，同时提高您的生产力。



以下是使用 Quick Start 加入 Amazon SageMaker Studio 的一次性步骤：

1. 打开 AWS 控制台并切换到您要使用的 AWS 区域。

{{% notice warning %}}
**弗吉尼亚** 如下图所示，但您也可以选择其他地区 [SageMaker Studio 可用。](https://docs.aws.amazon.com/sagemaker/latest/dg/studio.html) 正确的区域选择听讲师的。
{{% /notice %}}

![image-20210731085428195](/images/PredictiveMaintenance/image-20210731085428195.png)


2. 在搜索栏中，输入 **SageMaker** 并单击 **Amazon SageMaker**。

[![img](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image23.png)](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image23.png)

3. 单击 **Amazon SageMaker Studio**（左窗格中的第一个选项）。

[![img](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image40.png)](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image40.png)

4. 点击**Quick Start - 快速启动**。
5. 将**用户名** 定义为 **sagemakeruser** 。
6. 在执行角色下选择**Create a new role - 创建新角色**。

[![img](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image24.png)](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image24.png)

7. 保持默认，点击**创建角色**。

[![img](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image25.png)](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image25.png)

8. 会看到角色创建成功。

[![img](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image26.png)](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image26.png)



{{% notice note %}} 

您可以看到选项 **Enable Amazon SageMaker project templates and JumpStart for this account and Studio users** 已启用。保留此默认设置。 

{{% /notice %}}



9. 选择新创建的角色并点击**Submit - 提交**。

[![img](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image27.png)](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image27.png)

10. SageMaker Studio 环境将在几分钟内处于 **Pending** 状态。

[![img](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image28.png)](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image28.png)

11. 几分钟后，状态将转换为**Ready**。

[![img](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image29.png)](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image29.png)

12. Amazon SageMaker Studio 准备就绪后，单击**Open Studio**。首次访问 SageMaker Studio 时，页面可能需要 1 或 2 分钟才能加载。

![image-20210731093200091](/images/PredictiveMaintenance/image-20210731093200091.png)

[![img](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image30.png)](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image30.png)

13. 您将被重定向到一个新的 Web 选项卡，如下所示：

[![img](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image31.png)](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image31.png)

14. 在 **Notebooks 和计算资源** 下，确保选中 **Data Science** SageMaker 图像并单击 **Notebook - Python 3**。

[![img](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image32.png)](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image32.png)

15. 您将进入 **Untitled.ipynb** 笔记本。

[![img](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image33.png)](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image33.png)

16. 您可以通过右键单击名称来重命名笔记本。改名称为`ImmersionDay.ipynb`

[![img](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image34.png)](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image34.png)

[![img](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image35.png)](https://sagemaker-immersionday.workshop.aws/prerequisites/media/image35.png)

**恭喜！！** 您已成功创建 SageMaker Studio 域并启动 SageMaker Studio Notebook。





