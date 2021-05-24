---
title: "模型部署与使用"
chapter: false
weight: 46
---

## 六、模型部署与使用

### 部署模型线上推理

为了更好的理解，超参数调优后的模型部署流程，这里采用了UI方式来部署模型。当然这部分可以通过代码实现。

![image-20210405230902960](https://raw.githubusercontent.com/liangyimingcom/storage/master/uPic/image-20210405230902960.png)

![image-20210405231402322](https://raw.githubusercontent.com/liangyimingcom/storage/master/uPic/image-20210405231402322.png)

![image-20210405231448328](https://raw.githubusercontent.com/liangyimingcom/storage/master/uPic/image-20210405231448328.png)



### 模型评估 与 模型推理（预测效果展示）

现在我们要使用上图中的部署好的endpoint来做推理，代码如下：

~~~python
#预测 1：准备sagemaker endpoint
xgb_predictor = sagemaker.predictor.RealTimePredictor(endpoint=endpoint_name)

#from sagemaker.predictor import csv_serializer
from sagemaker.predictor import csv_serializer, json_deserializer
xgb_predictor.content_type = 'text/csv'
xgb_predictor.serializer = csv_serializer
xgb_predictor.deserializer = None

# inference预测处理：传入modeldata数据和 sagemaker inference handle，获得预测结果
def sagemaker_predict(data, xgb_predictor, rows=100):
    split_array = np.array_split(data, int(data.shape[0] / float(rows) + 1))    
    predictions = ''
    for array in split_array:
        split_result = xgb_predictor.predict(data=array).decode('utf-8')
        #print(split_result)
        split_result = str.strip(split_result, '[]') # 去掉多余的前后[]符号
        #split_result=split_result.replace(' ', '')
        #print('res='+split_result)
             
        predictions = ','.join([predictions, split_result])
            
    #print(predictions)
    #return np.fromstring(predictions[1:], sep=',', dtype=np.float64) 
    return np.fromstring(predictions[1:], sep=',') 
  
#预测 2：预测并获得预测结果
model_data_to_numpy = model_data.to_numpy()[:, 1:] #转换所有的行，从第一列开始（忽略0列）

#调用函数
predictions = sagemaker_predict(model_data_to_numpy,xgb_predictor, rows=100)
~~~

**更多详情，请查看源代码：**

[Step02_SageMaker_XGBoost_Tuningjob.ipynb](https://github.com/liangyimingcom/Use-SageMaker_XGBoost-convert-Time-Series-into-Supervised-Learning-for-predictive-maintenance/blob/master/Step02_SageMaker_XGBoost_Tuningjob.ipynb)



## 七、结论

**预测性维护需求场景验证成功**

1. 《预测性维护》需求场景验证成功，用户现有的数据集可以实现故障提前周期的预测；
2. 数据预处理中《滑窗》次数越多，预测准确度越高。超过100个《滑窗》提高了预测模型的准确性。（100个滑窗的数据集，分别为5、10、20、30、40、50分钟的6个预测模型）
3. 提前周期从5分钟到50分钟，预测《有故障》的准确率较高，召回率有待提高。 
4. 在反复数据预处理和XGBoost调参训练后，使用Sagemaker将预测准确度AUC从0.79提高到0.93；
5. AUC指标表现良好，意味着模型质量较高；ROI曲线图也证明了AUC的结果；

**SageMaker 独有特性与功能**

使用SageMaker的内置的XGBoost算法，展示了SageMaker在ML的整个生命周期中的各项功能。Amazon SageMaker提供了一连贯的功能，帮助数据科学家高效的、低成本实现端到端，从模型构建到生成环境部署的各种工作。这些功能包括全托管Jupyter notebook 用来构建模型，后续的自动调参、模型构建、部署、负载均衡、弹性伸缩直达生产环境。在自动训练和自动调参的过程中可以使用spot training大大节省训练成本。

这些功能，大幅度降低了企业使用ML所需要的资金门槛和人才门槛，是当今企业通过ML来提升竞争力的强有力的平台。

![](https://raw.githubusercontent.com/liangyimingcom/storage/master/uPic/image-20210405223223554.png)



## 八、引用reference

1. 机器学习中梯度提升算法的简要介绍 https://machinelearningmastery.com/gentle-introduction-gradient-boosting-algorithm-machine-learning/
2. 时间序列预测转化为监督学习问题 https://machinelearningmastery.com/time-series-forecasting-supervised-learning/
3. 如何用Python将时间序列问题转化为有监督学习问题 https://machinelearningmastery.com/convert-time-series-supervised-learning-problem-python/
4. How To Backtest Machine Learning Models for Time Series Forecasting如何回测时间序列预测的机器学习模型 https://machinelearningmastery.com/backtest-machine-learning-models-time-series-forecasting/
5. How to Use XGBoost for Time Series Forecasting https://machinelearningmastery.com/xgboost-for-time-series-forecasting/
