---
title: "SageMaker+XGBoost 训练与超参数调优"
chapter: false
weight: 45
---

## 五、SageMaker+XGBoost 训练与超参数调优

### 什么是XGBoost？

如果将机器学习问题分为传统机器学习和深度学习，那么XGBoost是在**传统机器学习**竞赛中获得最多奖项的算法。 XGBoost的全名是Extreme Gradient Boosting，它是梯度增强的开源实现。 梯度提升通过决策树将几个弱模型（集合）聚集在一起，以形成最终模型。 此过程是一个连续且迭代的优化过程。 通过计算损失函数的梯度可以优化每次迭代的方向 ，然后采用梯度下降法连续减小损失函数，得到最终模型。

**解决三个主要的ML问题:**

1. 分类（classification）
2. 回归（regression）
3. 排名

SageMaker中使用了开源的XGBoost machine learning (ML) library，实现了 高度的可扩展性和分布式，可在多台计算节点上使用海量数据用于训练。SageMaker XGBoost 容器的优势有：

![image-20210405220827609](https://raw.githubusercontent.com/liangyimingcom/storage/master/uPic/image-20210405220827609.png)



### 算法选择构建模型

综上所述，这里采用算法是：XGBoost  - Sagemaker的内置算法，主要原因：

1. 开箱即用、听话，出活。
2. 适合做项目，短、平、快！

作为 SageMaker XGBoost的用户，现在您可以在创建训练作业时指定新版本，从而轻松使用其提供的新功能与各项改进。详见以下代码：

```python
from sagemaker.amazon.amazon_estimator import get_image_uri
container = get_image_uri(region, 'xgboost', '1.0-1')

estimator = sagemaker.estimator.Estimator(container, 
                                          role, 
                                          hyperparameters=hyperparameters,
                                          train_instance_count=1, 
                                          train_instance_type='ml.m5.2xlarge', 
                                          )

estimator.fit(training_data)
```



### 模型训练

使用 SageMaker XGBoost 进行训练。具体请参见以下代码：

```python
from sagemaker.session import s3_input
from sagemaker.xgboost.estimator import XGBoost

xgb_script_mode_estimator = XGBoost(
    entry_point="abalone.py",
    hyperparameters=hyperparameters,
    image_name=container,
    role=role, 
    train_instance_count=1,
    train_instance_type="ml.m5.2xlarge",
    framework_version="1.0-1",
    output_path="s3://{}/{}/{}/output".format(bucket, prefix, "xgboost-script-mode"),
    train_use_spot_instances=train_use_spot_instances,
    train_max_run=train_max_run,
    train_max_wait=train_max_wait,
    checkpoint_s3_uri=checkpoint_s3_uri
)

xgb_script_mode_estimator.fit({"train": train_input})
```



### 超参数优化(反复调参试错)

我们已经准备好数据集，就可以训练模型了。在执行此操作之前，需要进行“超参数”的配置，这些配置参数可能会严重影响训练后的模型的准确度。例如，XGBoost算法具有几十个超参数，需要为这些超参数选择正确的值，才能获得理想的模型训练结果。由于超参数设置非常复杂（穷举矩阵很大）并导致了模型准确度的差别，因此通常无法直接获得最佳超参数的配置。而SageMaker的超参数优化（Hyperparameter_Tuning）非常好的解决了这个问题，SageMaker的超参数优化采用了自动的方法去搜索到了最佳超参数配置。

如何、将使用SageMaker Hyperparameter Tuning来有效地自动执行搜索最佳参数？具体来说，对于超参数，我们可以指定每个超参数指定一个范围或可能值的列表（给出穷举矩阵的范围）。 SageMaker超参数优化将自动启动具有不同超参数设置的多个训练作业，基于预定义的“结果指标evaluation metric”评估那些训练作业的结果，并根据先前的结果为以后的尝试选择超参数设置。对于每个超参数调整作业，我们将给它一个预算（最大训练作业数），并且在执行完许多训练作业后（在预算内）完成。

<img src="https://raw.githubusercontent.com/liangyimingcom/storage/master/uPic/image-20210405223346553.png" alt="image-20210405223346553" style="zoom:50%;" />

<img src="https://raw.githubusercontent.com/liangyimingcom/storage/master/uPic/image-20210405223357020.png" alt="image-20210405223357020" style="zoom:50%;" />

评估指标是mae，数值越小越优：

<img src="https://raw.githubusercontent.com/liangyimingcom/storage/master/uPic/image-20210405223405347.png" alt="image-20210405223405347" style="zoom:50%;" />

该过程的目的是得到一个最佳的超参配比，使得评估指标在validation set上的效果最优。这里的评估指标就是mae，数值越小越优。





### 评估Evaluation 与 模型推理

![image-20210406003641094](https://raw.githubusercontent.com/liangyimingcom/storage/master/uPic/image-20210406003641094.png)

**更多详情，请查看源代码：**

[Step02_SageMaker_XGBoost_Tuningjob.ipynb](https://github.com/liangyimingcom/Use-SageMaker_XGBoost-convert-Time-Series-into-Supervised-Learning-for-predictive-maintenance/blob/master/Step02_SageMaker_XGBoost_Tuningjob.ipynb)

