# csa_FBCNet_for_Stroke



#### 项目：兰州大学2024-2025校创

#### 名称：基于机器学习的运动想象脑机接口对脑卒中患者特化数据模型

#### 成员：洪佳慧、施博文、林泽宇、陈佳钰、胡可



#### 使用数据集来源及参考文献：

[脑卒中患者数据集](https://www.nature.com/articles/s41597-023-02787-8)

[上海大学数据集](https://www.nature.com/articles/s41597-022-01647-1)

[欧氏对齐](https://ieeexplore.ieee.org/document/8701679)



#### 下载依赖

```bash
pip install -r requirements.txt
```



#### 使用服务器将文件挂起运行

```bash
# 将ipynb转换为py文件
jupyter nbconvert --to script csa_FBCNet.ipynb
# 挂起运行
nohup python csa_FBCNet.py > output.log 2>&1 &
# 查看进程
ps -p [编号]
```



#### 方法：

- 对源数据进行通道筛选、下采样、滤波、去伪迹等预处理步骤

- 使用上海大学数据集的5个被试数据（以下统称SHU数据），以及脑卒中患者数据集（以下统称Stroke数据）的所有数据作为base model的训练数据

- 选中5名脑卒中患者分别测试

- 对选中的1名脑卒中患者，使用6折交叉验证，对剔除这名患者后的Stroke数据及SHU数据，先用欧氏对齐处理，再训练1500个epoch，在验证集上评估，且使用patience为200的早停法，以验证集的loss作为指标，保存表现最好的模型

- 使用该患者对应的模型，使用从头训练、解冻连接层和解冻所有层三种方法，通过10折交叉验证，在患者数据上，先用欧氏对齐处理，再分别训练800、200、200个epoch，并记录评估结果

- 对每个患者的评估结果，计算每个患者的预测准确率，以及所有患者的平均准确率



#### 训练结果：

##### 不使用base model(从头训练)

```
avg acc for subj1:  0.6875
avg acc for subj2:  0.71875
avg acc for subj3:  0.73125
avg acc for subj4:  0.74375
avg acc for subj5:  0.68125
final acc for all subjs:  0.7125
```

##### 解冻分类器层

```
avg acc for subj1:  0.8125
avg acc for subj2:  0.69375
avg acc for subj3:  0.70625
avg acc for subj4:  0.8
avg acc for subj5:  0.60625
final acc for all subjs:  0.7237500000000001
```

##### 解冻所有层

```
avg acc for subj1:  0.8625
avg acc for subj2:  0.68125
avg acc for subj3:  0.7125
avg acc for subj4:  0.75625
avg acc for subj5:  0.75625
final acc for all subjs:  0.75375
```
