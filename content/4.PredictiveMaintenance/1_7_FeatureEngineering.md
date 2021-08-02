---
title: "特征工程"
chapter: false
weight: 15
---



## 利用NUMPY 和 Pandas对实验数据进行特征工程



## 一、数据准备

在此步骤中，您将使用 Amazon SageMaker Studio 笔记本来预处理训练机器学习模型所需的数据。

1. 单击“amazon-sagemaker-immersion-day”文件夹，然后双击最后一个文件：“xgboost_direct_marketing_sagemaker.ipynb”笔记本。
2. 系统将提示您选择一个内核。选择“Python 3 (Data Science)”内核并单击“选择”。

[![img](https://sagemaker-immersionday.workshop.aws/lab1/option2/media/image39.png)](https://sagemaker-immersionday.workshop.aws/lab1/option2/media/image39.png)

[![img](https://sagemaker-immersionday.workshop.aws/lab1/option2/media/image40.png)](https://sagemaker-immersionday.workshop.aws/lab1/option2/media/image40.png)

3. 然后打开笔记本，您可以在笔记本的右上角点击更改《CPU 和内存状态》，更改笔记本实例的配置为**ml.m5.2xlarge**，从而缩小实验数据完成特征工程的所需时间。

![image-20210802144426244](/images/PredictiveMaintenance/image-20210802144426244.png)

![image-20210802144345203](/images/PredictiveMaintenance/image-20210802144345203.png)



4. 等待几分钟后，验证内核、 CPU 内存的状态是否准确（如下图）。

![image-20210802144605110](/images/PredictiveMaintenance/image-20210802144605110.png)

5. 通过在每个单元格中按 **Shift+Enter** 执行前两个单元格。
{{% notice tip %}}
* 代码运行时，* 出现在方括号之间，如右侧第一个屏幕截图所示。
* 几秒钟后，代码执行将完成，* 将替换为数字 1。
* 可以通过不断的 **Shift+Enter** 来执行到笔记本的结尾，完成全部实验代码！
    {{% /notice %}}

此代码将导入一些库并在您的 Jupyter 笔记本环境中定义一些环境变量。

[![img](https://sagemaker-immersionday.workshop.aws/lab1/option2/media/image9.png)](https://sagemaker-immersionday.workshop.aws/lab1/option2/media/image9.png)

5. 现在，让我们通过运行第三个单元来下载数据集。

![image-20210802145828779](/images/PredictiveMaintenance/image-20210802145828779.png)


7. 在下一个单元格中，您将数据集加载到 Pandas 数据框中

![image-20210802150304401](/images/PredictiveMaintenance/image-20210802150304401.png)


8. 现在让我们探索数据并了解每个特征的数据分布：

[![img](https://sagemaker-immersionday.workshop.aws/lab1/option2/media/image12.png)](https://sagemaker-immersionday.workshop.aws/lab1/option2/media/image12.png)

![image-20210802150603465](/images/PredictiveMaintenance/image-20210802150603465.png)

9. 现在让我们看看我们的特征与我们试图预测的目标之间的关系。

![image-20210802150751725](/images/PredictiveMaintenance/image-20210802150751725.png)

10. 现在让我们看看我们的特征是如何相互关联的

![image-20210802150924387](/images/PredictiveMaintenance/image-20210802150924387.png)

11. 现在我们使用滑动窗口方法，对数据完成预处理和数据转换变形。
    所谓“滑动窗口方法”，是使用先前的时间步长预测下一个时间步长，在统计资料中它也称为滞后法。使用滑动窗口方法，可以将《多元时间序列数据集》转换为《监督学习问题》。

![image-20210802151317557](/images/PredictiveMaintenance/image-20210802151317557.png)

12. Amazon SageMaker XGBoost 算法要求数据采用 libSVM 或 CSV 格式（无标题），并且第一列必须是目标变量。所以在这一步中，我们相应地转换数据

![image-20210802151729818](/images/PredictiveMaintenance/image-20210802151729818.png)

13. 我们将我们的数据集分成 3 个通道：训练、验证、测试集：

![image-20210802151838458](/images/PredictiveMaintenance/image-20210802151838458.png)

14. 现在我们将最终数据上传到 Amazon S3 存储桶中。

[![img](https://sagemaker-immersionday.workshop.aws/lab1/option2/media/image19.png)](https://sagemaker-immersionday.workshop.aws/lab1/option2/media/image19.png)

16. 现在通过控制台检查 S3 存储桶，确保您已上传 train.csv 和 validation.csv。在 AWS 控制台主页中，键入“S3”。

[![img](https://sagemaker-immersionday.workshop.aws/lab1/option2/media/image44.png)](https://sagemaker-immersionday.workshop.aws/lab1/option2/media/image44.png)

17. 单击您的存储桶名称。如果存在两个存储桶，请使用包含您的区域名称的存储桶（下图中的**“us-east-1”**示例）。

[![img](https://sagemaker-immersionday.workshop.aws/lab1/option2/media/image45.png)](https://sagemaker-immersionday.workshop.aws/lab1/option2/media/image45.png)

18. 点击“sagemaker/”，然后点击“DEMO-xgboost-predictive_maintenance/”。您将看到“train/”和“validation/”文件夹。

[![img](https://sagemaker-immersionday.workshop.aws/lab1/option2/media/image46.png)](https://sagemaker-immersionday.workshop.aws/lab1/option2/media/image46.png)

19. 您可以查看每个文件夹的内部，以确保“train.csv”文件和“validation.csv”文件都在那里。

[![img](https://sagemaker-immersionday.workshop.aws/lab1/option2/media/image47.png)](https://sagemaker-immersionday.workshop.aws/lab1/option2/media/image47.png)[![img](https://sagemaker-immersionday.workshop.aws/lab1/option2/media/image48.png)](https://sagemaker-immersionday.workshop.aws/lab1/option2/media/ image48.png)

**恭喜！！** 您已成功准备数据以训练 XGBoost 模型。



## 二、结论

在本实验中，您已经完成了所需的环境设置和数据工程过程，以清理和准备用于模型构建和训练的数据。在下一个实验中，您将学习如何使用 SageMaker 的内置 XGBoost 算法训练、调整和部署 XGBoost 模型。

