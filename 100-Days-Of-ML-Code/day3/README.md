# 多重线性回归


<p align="center">
  <img src="https://github.com/Avik-Jain/100-Days-Of-ML-Code/blob/master/Info-graphs/Day%203.jpg">
</p>


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


