# 多重线性回归


<p align="center">
  <img src="https://github.com/Avik-Jain/100-Days-Of-ML-Code/blob/master/Info-graphs/Day%203.jpg">
</p>
多元线性回归试图通过将线性方程拟合到观测数据来模拟两个或更多个特征与响应之间的关系. 执行多元线性回归的步骤几乎和简单的线性回归相同. 评估是唯一的不同点. 可以通过评估找到对预测输出有最大的影响的因素与不同变量之间的参照关系.

$$ y(因变量) = b_0 + b_1*x_1 + b_2 * x_2 +  ...  + b_n*x_n(多元自变量)$$

假设
  对于一个成功的回归分析,验证以下假设是非常必须的.
  1. 线性 自变量和因变量之间的关系应该是线性的.
  2. 方差齐性(恒定方差) 误差的方差应维持恒定
  3. 多元正态 多元回归假设剩余数据是正态分布
  4. 非多重性 在数据中,假设没有或有极少重复. 当特征(自变量)不相互独立,就会出现多重性.
## 步骤 1: 数据预处理

### 导入库
```python
import pandas as pd
import numpy as np
```
### 导入数据集
```python
dataset = pd.read_csv('50_Startups.csv')
X = dataset.iloc[ : , :-1].values
Y = dataset.iloc[ : ,  4 ].values
```

### 编码分类数据
```python
from sklearn.preprocessing import LabelEncoder, OneHotEncoder
labelencoder = LabelEncoder()
X[: , 3] = labelencoder.fit_transform(X[ : , 3])
onehotencoder = OneHotEncoder(categorical_features = [3])
X = onehotencoder.fit_transform(X).toarray()
```

### 避免进入坏数据陷阱
```python
X = X[: , 1:]
```

### 将数据集分为训练集和测试集
```python
from sklearn.cross_validation import train_test_split
X_train, X_test, Y_train, Y_test = train_test_split(X, Y, test_size = 0.2, random_state = 0)
```
## 步骤 2: 使多重线性回归贴合训练集
```python
from sklearn.linear_model import LinearRegression
regressor = LinearRegression()
regressor.fit(X_train, Y_train)
```

## 步骤 3: 预测测试集结果
```python
y_pred = regressor.predict(X_test)
```


