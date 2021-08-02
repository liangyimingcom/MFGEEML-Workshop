---
title: "训练和调整模型"
chapter: false
weight: 23

---



## 训练、调整XGBOOST模型

在此步骤中，您将使用您在上一个实验室 **（特征工程实验）** 中上传到 Amazon S3 存储桶中的训练数据集来训练您的机器学习模型。

要运行此实验，您需要先完成特征工程实验 。



1. 首先，我们将指定 XGBoost ECR 容器位置。

[![img](https://sagemaker-immersionday.workshop.aws/lab2/media/image15.png)](https://sagemaker-immersionday.workshop.aws/lab2/media/image15.png)



2. 指定训练和验证数据集位置：

[![img](https://sagemaker-immersionday.workshop.aws/lab2/media/image4.png)](https://sagemaker-immersionday.workshop.aws/lab2/media/image4.png)



3. 现在，在 SageMaker Estimator 中定义训练参数。您还将在 set_hyperparameters 中定义调整超参数，然后调用“fit”方法来训练模型。

[![img](https://sagemaker-immersionday.workshop.aws/lab2/media/image5.png)](https://sagemaker-immersionday.workshop.aws/lab2/media/image5.png)



4. 您也可以从 AWS 控制台检查以验证训练作业是否已启动，并等待状态变为“已完成”。从 AWS 控制台主页转到 SageMaker。

[![img](https://sagemaker-immersionday.workshop.aws/lab2/media/image16.png)](https://sagemaker-immersionday.workshop.aws/lab2/media/image16.png)



5. 单击左侧窗格并选择“培训作业”。您将首先看到处于“InProgress”状态的作业。等待 3-5 分钟，直到训练作业完成且状态变为“已完成”。

[![img](https://sagemaker-immersionday.workshop.aws/lab2/media/image6.png)](https://sagemaker-immersionday.workshop.aws/lab2/media/image6.png)



**您成功训练了 XGBoost 模型！！** 



