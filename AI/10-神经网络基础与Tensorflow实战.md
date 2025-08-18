### 激活函数
非线性函数，能够让神经网络解决非线性的问题
梯度容易保持稳定（求导为1）
1. sigmoid（浅层的神经网络可用）
2. tanh（比sigmoid更容易训练）
3. relu
### 损失函数
1. MAE 绝对误差 ｜y-y‘｜
2. MSE （y’-y）^2
### 反向传播
从最终结果开始，一层一层从后往前计算每个节点、每个参数对最终结果的“影响力”（梯度）
即求导的过程，Loss对每个参数的偏导数
### 梯度下降
### 优化方法
告诉参数，往那个方向改，改多少
1. SGD，收敛速度快，但不稳定
2. Momentum，模拟运动惯性，保持一定方向的一致性
3. Adagrad，自适应梯度算法，越往后学习，误差越来越小，会自动调整学习率
4. RMSprop
5. Adam，结合Adagrad和RMSprop
#### 归一化处理
提升学习效率
1. MinMaxScaler 数据压缩到`[0,1]`之间
2. StandardScaler 数据压缩到(0,1)均值为0，标准差为1的正态分布

## 整个过程
1. 前向传播计算当前参数的预测值和Loss
2. 反向传播计算梯度（Loss对每个参数的偏导数）
3. 优化算法根据梯度信息，结合自身规则更新参数

# Tensorflow的使用
### 参数调整
1. 早停参数
2. 学习率参数
### 分布式训练
1. tf.distribute.MirroredStrategy（单机多卡）
2. MultiWorkerMirroredStrategy（多机多卡）
### 部署
TensorFlow Serving
1. 模型导出 `tf.saved_model.save(model, "/model/1")`
2. 启动服务：通过Docker或直接运行 
```
docker run -p 8501:8501 --name=tfserving \

-v "/model:/models" -e MODEL_NAME=my_model \

tensorflow/serving
```
3. 客户端调用
```
import requests

data = {"instances": [input_data]}

requests.post("http://localhost:8501/v1/models/my_model:predict",

json=data)
```
### 应用
1. 推荐系统
2. 广告CTR预测
3. 通过TensorFlow Lite配合部署到移动设备实现边缘计算

### 时间序列的神经网络

informer