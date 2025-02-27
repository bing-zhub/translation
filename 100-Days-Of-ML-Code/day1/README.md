# 数据预处理
<p align="center">
  <img src="https://github.com/Avik-Jain/100-Days-Of-ML-Code/blob/master/Info-graphs/Day%201.jpg">
</p>
As shown in the infograph we will break down data preprocessing in 6 essential steps.
Get the dataset from [Here]() that is used in this example



## 步骤 1:  导入所需函数库
```Python
import numpy as np
import pandas as pd
```
每次我们将导入两个必须的函数库.
Numpy含许多数学函数 Pandas被用来导入和管理数据集.
## 步骤 2: 导入数据集
```python
dataset = pd.read_csv('Data.csv')
X = dataset.iloc[ : , :-1].values
Y = dataset.iloc[ : , 3].values
```
数据常常以.csv的格式存在. 一个CSV文件在纯文本文件存储了表格式化的数据. 文件的每一行都是一个数据项.我们用pandas库中的read_csv方法去读取本地CSV文件,并将读取内容当做一个数据帧. 之后我们创建不同的矩阵和向量表示数据帧中的自变量与因变量.
## 步骤 3: 处理缺失数据
```python
from sklearn.preprocessing import Imputer
imputer = Imputer(missing_values = "NaN", strategy = "mean", axis = 0)
imputer = imputer.fit(X[ : , 1:3])
X[ : , 1:3] = imputer.transform(X[ : , 1:3])
```
我们得到的数据很少是同类组成的. 由于不同的原因,会存在一定的数据缺失, 所以我们需要对缺失数据进行处理,以至于不影响机器学习模型的性能. 我们可以使用整列中的均值或中值来代替缺失数据. 我们用sklearn.preprocessing中的Imputer类来解决这个任务.
## 步骤 4: 将分类数据编码
```python
from sklearn.preprocessing import LabelEncoder, OneHotEncoder
labelencoder_X = LabelEncoder()
X[ : , 0] = labelencoder_X.fit_transform(X[ : , 0])
```
分类数据是一些包含了标签值而非数字值得变量. 可能值得个数往往局限于固定的集合. 数据例如"Yes" 和 "No" 不可用于模型中的数学方程, 所以我们需要把这些数据编码为数字. 为了实现编码,我们引入sklearn.preprocessing库中的LabelEncoder类.

### 创建模型变量
```python
onehotencoder = OneHotEncoder(categorical_features = [0])
X = onehotencoder.fit_transform(X).toarray()
labelencoder_Y = LabelEncoder()
Y =  labelencoder_Y.fit_transform(Y)
```
## 步骤 5: 把数据集切分为训练集和测试集 
```python
from sklearn.cross_validation import train_test_split
X_train, X_test, Y_train, Y_test = train_test_split( X , Y , test_size = 0.2, random_state = 0)
```
我们对数据集进行两个划分, 一个用来训练,被称作训练集. 另一个被用来测试训练过后模型的性能,被称作测试集. 数据集通常使用82分. 通过引入sklearn.crossvalidation库中的train_test_split()方法实现划分.
## 步骤 6: 特征缩放
```python
from sklearn.preprocessing import StandardScaler
sc_X = StandardScaler()
X_train = sc_X.fit_transform(X_train)
X_test = sc_X.fit_transform(X_test)
```
大多数机器学习算法在运算中使用两个数据点的Euclidean距离,与在幅度/单位和范围姿势问题上具有高度变化的特征.高幅度特征会比低幅度特征在距离计算中增加更大的权重. 这一切通过特征标准化和z-score标准化完成. 代码由sklearn.preprocessing中的StandardScalar完成.
### 结束 :smile:

