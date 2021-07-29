---
title: "部署模型"
chapter: false
weight: 25
---



## 部署和验证XGBOOST模型完成预测性维护



在此步骤中，您会将经过训练的模型部署到实时 HTTPS 端点。此过程可能需要大约 6-8 分钟。您还可以为此部署选择我们较新的实例类型，例如“ml.m5.xlarge”。

[![img](https://sagemaker-immersionday.workshop.aws/lab2/media/image17.png)](https://sagemaker-immersionday.workshop.aws/lab2/media/image17.png)



现在，我们还将在 AWS 控制台视图中检查 SageMaker 终端节点部署。在 SageMaker AWS 控制台中，转到左侧窗格中的“端点”。您将看到处于“正在创建”状态的端点。

[![img](https://sagemaker-immersionday.workshop.aws/lab2/media/image18.png)](https://sagemaker-immersionday.workshop.aws/lab2/media/image18.png)

然后它将转换为“InService”状态。

[![img](https://sagemaker-immersionday.workshop.aws/lab2/media/image19.png)](https://sagemaker-immersionday.workshop.aws/lab2/media/image19.png)



## 预测和评估模型性能

在此步骤中，您将重新格式化 CSV 数据，然后运行模型以创建预测。然后，您将使用混淆矩阵评估模型性能。在这种情况下，我们预测设备在未来的一段时间是否会发生故障（预测性维护场景）。



1. 首先，我们需要确定如何将数据传入和接收来自端点的数据。我们的数据目前以 NumPy 数组的形式存储在我们笔记本实例的内存中。为了在 HTTP POST 请求中发送它，我们将它序列化为一个 CSV 字符串，然后解码生成的 CSV。

*注意：对于 CSV 格式的推理，SageMaker XGBoost 要求数据不包括目标变量。*

[![img](https://sagemaker-immersionday.workshop.aws/lab2/media/image20.png)](https://sagemaker-immersionday.workshop.aws/lab2/media/image20.png)



2. 现在，您将创建一个简单的函数来：

- 循环我们的测试数据集。
- 将其拆分为小批量的行。
- 将这些小批量转换为 CSV 字符串有效负载（注意，我们首先从数据集中删除目标变量）。
- 通过调用 XGBoost 端点检索小批量预测。
- 收集预测并将我们的模型提供的 CSV 输出转换为 NumPy 数组。

[![img](https://sagemaker-immersionday.workshop.aws/lab2/media/image10.png)](https://sagemaker-immersionday.workshop.aws/lab2/media/image10.png)



3. 现在我们将检查我们的混淆矩阵，看看我们的预测与实际情况有多好。

[![img](https://sagemaker-immersionday.workshop.aws/lab2/media/image11.png)](https://sagemaker-immersionday.workshop.aws/lab2/media/image11.png)

因此，在大约 4000 个潜在客户中，模型预测 42 个会订阅，其中 94 个实际上订阅了。我们还有 389 名订阅者，他们实际上订阅了该模型并没有预测到会订阅。

| N=4000 |预测：否 |预测：是 |
| :--------- | :----------- | :------------ |
|实际：否 | 3594 | 42 |
|实际：是 |第389话94 |



特别声明：如果您在此过程中更改参数，此矩阵可能会有所不同。

