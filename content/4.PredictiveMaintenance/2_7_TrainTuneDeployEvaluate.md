---
title: "模型自动调优(可选)"
chapter: false
weight: 27
---



## 模型自动调优Automatic Tunning(可选)



Amazon SageMaker 自动模型调整，也称为超参数调整，通过使用您指定的算法和超参数范围在您的数据集上运行许多训练作业来找到模型的最佳版本。然后，它会选择超参数值，以生成性能最佳的模型，这由您选择的指标衡量。

例如，假设您想在此解决 [*二进制分类*](https://docs.aws.amazon.com/general/latest/gr/glos-chap.html#binary-classification-model) 问题数据集。您的目标是通过训练最大化算法的 [*曲线下面积 (auc)*](https://docs.aws.amazon.com/general/latest/gr/glos-chap.html#AUC) 指标XGBoost 算法模型。您不知道要使用 eta、alpha、min_child_weight 和 max_depth 超参数的哪些值来训练最佳模型。要找到这些超参数的最佳值，您可以指定 Amazon SageMaker 超参数优化搜索的值范围，以查找导致训练作业执行最佳的值组合，如您选择的目标指标所衡量的那样。超参数调整启动使用您指定范围内的超参数值的训练作业，并返回具有最高 auc 的训练作业。

1. 我们将在这个例子中调整四个超参数：

- *eta*：更新中使用的步长收缩以防止过度拟合。在每一步提升之后，你可以直接得到新特征的权重。 eta 参数实际上缩小了特征权重，使提升过程更加保守。
- *min_child_weight*：子节点所需的最小实例权重（hessian）总和。如果树分区步骤导致实例权重总和小于 min_child_weight 的叶节点，则构建过程放弃进一步分区。在线性回归模型中，这仅对应于每个节点所需的最小实例数。算法越大，越保守。
- *alpha*：权重的 L1 正则化项。增加此值会使模型更加保守。
- *max_depth*：树的最大深度。增加此值会使模型更加复杂，并且可能会过度拟合。

[![img](https://sagemaker-immersionday.workshop.aws/lab2/media/image21.png)](https://sagemaker-immersionday.workshop.aws/lab2/media/image21.png)

2. 接下来，我们将指定要调整的目标指标及其定义，其中包括从训练作业的 CloudWatch 日志中提取该指标所需的正则表达式 (Regex)。由于我们在这里使用内置的 XGBoost 算法，它发出两个预定义的指标：validation:auc 和 train:auc，我们选择监控validation:auc，如下所示。在这种情况下，我们只需要指定指标名称，不需要提供正则表达式。

[![img](https://sagemaker-immersionday.workshop.aws/lab2/media/image22.png)](https://sagemaker-immersionday.workshop.aws/lab2/media/image22.png)

3. 现在，我们将创建一个 HyperparameterTuner 对象，我们将传递给它：

- 上面创建的 XGBoost estimator
- 超参数范围
- 指标名称和定义
- 资源配置，例如要运行的训练作业总数以及可以并行运行的训练作业数量。

[![img](https://sagemaker-immersionday.workshop.aws/lab2/media/image23.png)](https://sagemaker-immersionday.workshop.aws/lab2/media/image23.png)

4. 现在我们可以通过调用 fit() 函数启动超参数调整作业。创建超参数调整作业后，我们可以进入 SageMaker 控制台跟踪超参数调整作业的进度，直到完成。

[![img](https://sagemaker-immersionday.workshop.aws/lab2/media/image24.png)](https://sagemaker-immersionday.workshop.aws/lab2/media/image24.png)

5. 让我们使用以下命令快速检查超参数调整作业状态。输出应该是“InProgress”。这意味着工作已成功启动。

[![img](https://sagemaker-immersionday.workshop.aws/lab2/media/image25.png)](https://sagemaker-immersionday.workshop.aws/lab2/media/image25.png)

6. 我们可以到 SageMaker 控制台跟踪超参数调整作业的进度，直到它完成。大约需要 **30 分钟** 才能完成。

[![img](https://sagemaker-immersionday.workshop.aws/lab2/media/image12.png)](https://sagemaker-immersionday.workshop.aws/lab2/media/image12.png)

7. 选择 Tuning 作业以查看详细视图：

[![img](https://sagemaker-immersionday.workshop.aws/lab2/media/image13.png)](https://sagemaker-immersionday.workshop.aws/lab2/media/image13.png)

8. （可选）调整作业完成后，您可以选择性能最佳的训练作业，像以前一样部署、预测和评估作业开发的模型。

[![img](https://sagemaker-immersionday.workshop.aws/lab2/media/image26.png)](https://sagemaker-immersionday.workshop.aws/lab2/media/image26.png)

