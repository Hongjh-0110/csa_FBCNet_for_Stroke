# csa_FBCNet_for_Stroke



#### 项目：兰州大学2024-2025校创

#### 名称：基于机器学习的运动想象脑机接口对脑卒中患者特化数据模型

#### 成员：洪佳慧、施博文、林泽宇、陈佳钰、胡可



#### 使用数据集来源及参考文献：

https://www.nature.com/articles/s41597-023-02787-8


https://www.nature.com/articles/s41597-022-01647-1



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

- 对源数据进行通道筛选、下采样、滤波等预处理步骤

- 使用上海大学数据集的前5个被试数据（以下统称SHU数据），以及脑卒中患者数据集的所有数据作为训练数据

- 对每个脑卒中患者，使用六折交叉验证方法对其它患者的数据及SHU数据训练（350个epoch）并验证，保存表现最好的模型
- 使用该患者对应的模型，通过十折交叉验证方法在患者数据上进行迁移学习（50个epoch）并验证
- 得出在每个患者身上预测的准确率，以及所有患者的平均准确率



#### 训练结果：
```
avg acc for subj1:  0.825
avg acc for subj2:  0.825
avg acc for subj3:  0.8
avg acc for subj4:  0.875
avg acc for subj5:  0.9
avg acc for subj6:  0.775
avg acc for subj7:  0.775
avg acc for subj8:  0.925
avg acc for subj9:  0.9
avg acc for subj10:  0.725
avg acc for subj11:  0.8
avg acc for subj12:  0.9
avg acc for subj13:  0.775
avg acc for subj14:  0.825
avg acc for subj15:  0.975
avg acc for subj16:  0.725
avg acc for subj17:  0.725
avg acc for subj18:  0.775
avg acc for subj19:  0.85
avg acc for subj20:  0.8
avg acc for subj21:  0.875
avg acc for subj22:  0.95
avg acc for subj23:  0.875
avg acc for subj24:  0.825
avg acc for subj25:  0.925
avg acc for subj26:  0.75
avg acc for subj27:  0.875
avg acc for subj28:  0.875
avg acc for subj29:  0.9
avg acc for subj30:  0.85
avg acc for subj31:  0.875
avg acc for subj32:  0.825
avg acc for subj33:  0.925
avg acc for subj34:  0.875
avg acc for subj35:  0.85
avg acc for subj36:  0.85
avg acc for subj37:  0.9
avg acc for subj38:  0.85
avg acc for subj39:  0.75
avg acc for subj40:  0.875
avg acc for subj41:  0.775
avg acc for subj42:  0.85
avg acc for subj43:  0.85
avg acc for subj44:  0.925
avg acc for subj45:  0.9
avg acc for subj46:  0.8
avg acc for subj47:  0.85
avg acc for subj48:  0.825
avg acc for subj49:  0.925
avg acc for subj50:  0.875
final acc for all subjs:  0.8464999999999999
```

