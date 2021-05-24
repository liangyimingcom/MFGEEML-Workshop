---
title: "数据预处理与特征工程"
chapter: false
weight: 44
---

## 四、数据预处理与特征工程

### 滑动窗口的代码实现

上一章节我们讲了强大的滑动窗口方法，这是将时间序列问题转化为监督学习问题的基础。在数据预处理章节，我们来具体看一下滑动窗口的代码实现。

**核心实现代码**：

~~~python
# 时间序列数据集转换为监督学习问题，将《多列时间序列数据》转换为《监督学习问题》Transform the timeseries data into supervised learning
# 参数: data=原始数据集；n_in=滑窗值（合并多少条时序记录合并在一起）；dropnan=是否保留华创后部分为空的记录；
def series_to_supervised(data, n_in=1, n_out=1, dropnan=True):
       n_vars = 1 if type(data) is list else data.shape[1]
       df = DataFrame(data)
       cols = list()
        
       # input sequence (t-n, ... t-1)
       for i in range(n_in, 0, -1):
              cols.append(df.shift(i))
                
       # forecast sequence (t, t+1, ... t+n)
       for i in range(0, n_out):
              cols.append(df.shift(-i))
                
       # put it all together
       agg = concat(cols, axis=1)
        
       # drop rows with NaN values
       if dropnan:
              agg.dropna(inplace=True)
       return agg.values

~~~

**优化后的代码避免JupyterLab Instance内存溢出**

时间序列数据集转换为监督学习的过程是在内存中完成的。实际操作中对有超过50列的50万行数据集，JupyterLab Instance内存占用非常轻松就超过100GB。

虽然SageMaker Studio支持随时申请更大的Instance（如ml.m5.24xlarge(96c/384g)）的Instance服务器来完成滑窗这个操作，但这显然成本过高，并不划算。

通过代码的优化，完成数据集进行**分段滑窗**，就可以很好的**解决内存溢出**的问题。实际测试过程中，此段代码可以在64G内存配置Instance（如ml.m5.4xlarge(16c/64g)）的实现120W行60列的测试数据集全部滑窗操作。

```python
# 对数据集进行分段滑窗，从而避免内存溢出；
# 参数：data=原始数据集；n_in=滑窗值（合并多少条时序记录合并在一起）；splite_md=行分段的数量，分的越小内存占用越小
def splite_series_to_supervised(data, n_in=1, splite_md=500000):
    splited_series_to_supervised = pd.DataFrame()  
    # start, stop, step 三个参数可以为负数
    for i in range(0,len(data),splite_md):
        splited_series_to_supervised = splited_series_to_supervised.append(DataFrame(
            series_to_supervised(model_data.iloc[ i : i+splite_md ], n_in=n_in, dropnan=False)))    
    return splited_series_to_supervised
```



### 数据预处理

滑窗后需要清理无用的数据，核心代码如下：

~~~python
#滑窗后处理：滑窗后的数据清理，将不是最后错误之前发生的滑窗全部删除
# 用 n_slidingwindow（滑窗数量） 做一个循环：不考虑（查询）最后一位的hascode，前面所有hascode=1 (每间隔58个列的第一个是hascode=true/false)的行全部删除；
# 即：只保留全部hascode=0的行(没有错误发生的行) 与 最后一位hascode=1的行(第一个错误发生的行)
def clear_supervised(data, n_slidingwindow, n_totalcolumns):
    count = 0
    while count < n_slidingwindow :
        n_colnum = count * n_totalcolumns
        data.drop(index=data[data[n_colnum].isin([True])].index, inplace=True)
        #print('column num= '+ str(n_colnum)) # for testing
        count = count + 1
    
~~~



### 样本不均衡处理

由于预测性维护的业务特性，导致了**故障样本**占整体数据样本的**比例极低**。实验数据中，故障样本比例大约是全部数据集合的万分之五。这是符合业务真实情况的，也是可以理解的。因为实际业务场景中，如果一个设备总是处于故障中，用户早就退货处理了，没有机会能让你收集到高比例的故障数据。不管如何，这么悬殊的样本会大幅度降低预测模型的准确度。对于XGBoost算法，可以使用imblearn库与scale_pos_weight来解决了样本不均衡问题，从而提升了预测性维护模型的准确度。 

本次实验数据，因为在前期调研中深入的理解了用户业务情况，所以通过了更简单的思路解决了样本不均衡问题。即数据集以时间序列顺向排序，**以故障发生记录点为原点 - 向过去的时间序列投影进行取值**，从而覆盖故障发生前的各种阈值的变化情况。

**截图说明：以故障发生记录点为原点 - 向过去的时间序列投影进行取值，从而覆盖故障发生前的各种阈值的变化情况。**

![image-20210406102410526](https://raw.githubusercontent.com/liangyimingcom/storage/master/uPic/image-20210406102410526.png)



实现的核心代码如下：

~~~python
# 滑窗后处理：正确滑窗，应该是 “有错和无错，各自一条”； 同时适用于pd.sample随机
# 即：挑出报错时的最后一条数据 + 删除上面N条未报错数据（上一条正常数据为行数为 except - n）
# 样本不均衡处理：以状态位=1的row为准，向上画出一个状态位=0的矩阵，从而仅保留部分状态位=0的滑窗集合（非故障数据集的筛选）
def pickup_supervised_4train_imbalance(data, n_slidingwindow, n_totalcolumns, splite_md=500000):
    splited_series_to_supervised = pd.DataFrame()  #定义一个临时的dataframe，用于解决内存溢出的问题    
    for i in range(0,len(data),splite_md):
        splited_data= data.iloc[ i : i+splite_md ]
        splited_data.reset_index(drop=True,inplace=True)

        n_checkpoint = n_totalcolumns * n_slidingwindow # 检查点位数 
        index_hascode_truerows = splited_data[splited_data[n_checkpoint].isin([True])].index #检查点列 为真的Index号，用于下一步挑出来
        target_data = pd.DataFrame(data=splited_data,index=index_hascode_truerows) # 把检查点列 为真 挑出来
        
          #--- 以状态位=1的row为准，向上画出一个状态位=0的矩阵 ---# 
        for i in range(1,n_slidingwindow+1): 
            target_data = target_data.append(pd.DataFrame(data=splited_data,index=index_hascode_truerows-i)) # 把检查点列 为真的上n滑窗行，挑出来 (N等于滑窗个数)，不适用于sample随机
            
        target_data[n_checkpoint].fillna(0, inplace=True) #上一行的 检查点列 有可能是空的，空值清洗为0
        splited_series_to_supervised = splited_series_to_supervised.append(target_data)

    splited_series_to_supervised.drop_duplicates(inplace=True) #清除重复的行（造成1增加）    
    return splited_series_to_supervised

~~~



### 数据标注与特征工程

**超过70％的工作量**是数据预处理与特征工程相关工作，这里的难点有：1）探索相关性；2）缩小特征值范围；3）将海量数据分为几批进行预处理，以避免服务器内存溢出；4）数据清理，滑动窗口清除无效数据；5）过滤数据，解决正负样本不平衡的问题；

**更多详情，请查看源代码：**

[Step01_SageMaker_XGBoost-convert-Time-Series-into-Supervised-Learning.ipynb](https://github.com/liangyimingcom/Use-SageMaker_XGBoost-convert-Time-Series-into-Supervised-Learning-for-predictive-maintenance/blob/master/Step01_SageMaker_XGBoost-convert-Time-Series-into-Supervised-Learning.ipynb)

