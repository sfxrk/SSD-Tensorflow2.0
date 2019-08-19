
# 训练步骤
定义网络结构-设计损失函数-梯度下降优化器

## 自己训练一个商品分类模型，在未使用预训练模型的情况下
```
>> 2019-08-19 15:34: Training Epoch: 10 || learning rate: 0.0001 || Loss: 0.43 || Accuracy: 85.25%|██████████████████████████████| 143 / 142 [use time : 0.273280]
>> 2019-08-19 15:34: Testing  Epoch: 10 || Loss: 4.04 || Accuracy: 6.57%|████████████████████████████████| 16 / 15 [use time : 0.121930]
>> 2019-08-19 15:47: Training Epoch: 20 || learning rate: 0.0001 || Loss: 0.27 || Accuracy: 90.87%|██████████████████████████████| 143 / 142 [use time : 0.277797]
>> 2019-08-19 15:47: Testing  Epoch: 20 || Loss: 3.10 || Accuracy: 23.63%|████████████████████████████████| 16 / 15 [use time : 0.120158]
>> 2019-08-19 16:00: Training Epoch: 30 || learning rate: 0.0001 || Loss: 0.21 || Accuracy: 93.06%|██████████████████████████████| 143 / 142 [use time : 0.274961]
>> 2019-08-19 16:00: Testing  Epoch: 30 || Loss: 2.79 || Accuracy: 33.18%|████████████████████████████████| 16 / 15 [use time : 0.120523]
>> 2019-08-19 16:13: Training Epoch: 40 || learning rate: 0.0001 || Loss: 0.17 || Accuracy: 94.30%|██████████████████████████████| 143 / 142 [use time : 0.272260]
>> 2019-08-19 16:13: Testing  Epoch: 40 || Loss: 2.44 || Accuracy: 41.17%|████████████████████████████████| 16 / 15 [use time : 0.122118]
>> 2019-08-19 16:26: Training Epoch: 50 || learning rate: 0.0001 || Loss: 0.15 || Accuracy: 95.07%|██████████████████████████████| 143 / 142 [use time : 0.275074]
>> 2019-08-19 16:26: Testing  Epoch: 50 || Loss: 2.25 || Accuracy: 46.26%|████████████████████████████████| 16 / 15 [use time : 0.123509]

```
50个epoch后，训练集95%准确率，测试集上只有46%准确率

## 接着上一次的模型，降低学习率，在训练50个epoch

```
>> 2019-08-19 16:52: Training Epoch: 10 || learning rate: 0.00001 || Loss: 0.02 || Accuracy: 99.30%|██████████████████████████████| 143 / 142 [use time : 0.164653]
>> 2019-08-19 16:52: Testing  Epoch: 10 || Loss: 1.26 || Accuracy: 76.31%|████████████████████████████████| 16 / 15 [use time : 0.102806]
>> 2019-08-19 17:03: Training Epoch: 20 || learning rate: 0.00001 || Loss: 0.02 || Accuracy: 99.43%|██████████████████████████████| 143 / 142 [use time : 0.177552]
>> 2019-08-19 17:03: Testing  Epoch: 20 || Loss: 1.24 || Accuracy: 79.10%|████████████████████████████████| 16 / 15 [use time : 0.099919]
>> 2019-08-19 17:14: Training Epoch: 30 || learning rate: 0.00001 || Loss: 0.02 || Accuracy: 99.50%|██████████████████████████████| 143 / 142 [use time : 0.178489]
>> 2019-08-19 17:14: Testing  Epoch: 30 || Loss: 1.17 || Accuracy: 80.53%|████████████████████████████████| 16 / 15 [use time : 0.103548]
>> 2019-08-19 17:25: Training Epoch: 40 || learning rate: 0.00001 || Loss: 0.01 || Accuracy: 99.54%|██████████████████████████████| 143 / 142 [use time : 0.176810]
>> 2019-08-19 17:25: Testing  Epoch: 40 || Loss: 1.13 || Accuracy: 81.38%|████████████████████████████████| 16 / 15 [use time : 0.102053]
>> 2019-08-19 17:36: Training Epoch: 50 || learning rate: 0.00001 || Loss: 0.01 || Accuracy: 99.58%|██████████████████████████████| 143 / 142 [use time : 0.174650]
>> 2019-08-19 17:36: Testing  Epoch: 50 || Loss: 1.08 || Accuracy: 81.76%|████████████████████████████████| 16 / 15 [use time : 0.099363]

```
## 使用imagenet预训练模型训练
```
>> 2019-08-19 17:41: Training Epoch: 1 || learning rate: 0.00001 || Loss: 0.38 || Accuracy: 89.01%|██████████████████████████████| 143 / 142 [use time : 1.070145]
>> 2019-08-19 17:41: Testing  Epoch: 1 || Loss: 1.66 || Accuracy: 41.22%|████████████████████████████████| 16 / 15 [use time : 0.660282]
>> 2019-08-19 17:42: Training Epoch: 2 || learning rate: 0.00001 || Loss: 0.22 || Accuracy: 93.50%|██████████████████████████████| 143 / 142 [use time : 0.165178]
>> 2019-08-19 17:42: Testing  Epoch: 2 || Loss: 1.05 || Accuracy: 61.64%|████████████████████████████████| 16 / 15 [use time : 0.100874]
>> 2019-08-19 17:43: Training Epoch: 3 || learning rate: 0.00001 || Loss: 0.16 || Accuracy: 95.24%|██████████████████████████████| 143 / 142 [use time : 0.163894]
>> 2019-08-19 17:43: Testing  Epoch: 3 || Loss: 0.88 || Accuracy: 68.57%|████████████████████████████████| 16 / 15 [use time : 0.101310]
>> 2019-08-19 17:44: Training Epoch: 4 || learning rate: 0.00001 || Loss: 0.13 || Accuracy: 96.13%|██████████████████████████████| 143 / 142 [use time : 0.164405]
>> 2019-08-19 17:44: Testing  Epoch: 4 || Loss: 0.67 || Accuracy: 76.04%|████████████████████████████████| 16 / 15 [use time : 0.102454]
>> 2019-08-19 17:45: Training Epoch: 5 || learning rate: 0.00001 || Loss: 0.11 || Accuracy: 96.74%|██████████████████████████████| 143 / 142 [use time : 0.165080]
>> 2019-08-19 17:45: Testing  Epoch: 5 || Loss: 0.57 || Accuracy: 78.97%|████████████████████████████████| 16 / 15 [use time : 0.104766]
>> 2019-08-19 17:50: Training Epoch: 10 || learning rate: 0.00001 || Loss: 0.06 || Accuracy: 98.07%|██████████████████████████████| 143 / 142 [use time : 0.162428]
>> 2019-08-19 17:50: Testing  Epoch: 10 || Loss: 0.41 || Accuracy: 84.44%|████████████████████████████████| 16 / 15 [use time : 0.103347]
>> 2019-08-19 18:01: Training Epoch: 20 || learning rate: 0.00001 || Loss: 0.04 || Accuracy: 98.81%|██████████████████████████████| 143 / 142 [use time : 0.166186]
>> 2019-08-19 18:01: Testing  Epoch: 20 || Loss: 0.49 || Accuracy: 84.57%|████████████████████████████████| 16 / 15 [use time : 0.102875]

```
明显训练速度变快