# 简易线性回归


<p align="center">
  <img src="https://github.com/Avik-Jain/100-Days-Of-ML-Code/blob/master/Info-graphs/Day%202.jpg">
</p>
使用单一特征预测对应值.
这回一个基于自变量(X)预测因变量(Y)的方法. 假设两个变量是线性相关的. 因此,我们尝试找到一个线性函数根据自变量(x)尽可能准确的预测对应因变量(y)

如何找到最切合的直线?
在回归模型中,我们尝试通过寻找最切合直线来最小化预测误差.回归直线的误差将会最小. 我们尝试最小化观测值(Yi)和模型预测值(Yp)之间的距离.
在回归任务中,我们会预测学生基于数个小时的学习会取得怎样的成绩.

# 步骤 1: 数据预处理
我们仍最受前序介绍中数据预处理的步骤
导入所需库
引入数据集
检查缺失数据
切分数据集
特征规格化将会被Simple Linear Regression Model这个库完成
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

dataset = pd.read_csv('studentscores.csv')
X = dataset.iloc[ : ,   : 1 ].values
Y = dataset.iloc[ : , 1 ].values

from sklearn.cross_validation import train_test_split
X_train, X_test, Y_train, Y_test = train_test_split( X, Y, test_size = 1/4, random_state = 0) 
```

# 步骤 2: 将简单线性回归模型贴合训练集
为了贴合模型数据集,我们使用sklearn.linear_model库中的LinearRegression类.然后我们实例化LinearRegression,创建regressor. 现在我们使用LinearRegression类中的fit()方法贴合回归对象.
 ```python
 from sklearn.linear_model import LinearRegression
 regressor = LinearRegression()
 regressor = regressor.fit(X_train, Y_train)
 ```
 # 步骤 3: 预测结果
 ```python
 Y_pred = regressor.predict(X_test)
 ```
 现在我们通过测试集预测观测值. 把输出内容保存在向量Y_pred中.为了预测结果我们使用LinearRegression类实例化并经过前序步骤训练过的regressor中的predict方法.
 # 步骤 4: 可视化 
 最后一步是对结果可视化 我们使用matplotlib.pyplot库对我们训练集和测试集结果作点,来观测我们模型预测值和真实值有多接近.
 ## 可视化训练结果
 ```python
 plt.scatter(X_train , Y_train, color = 'red')
 plt.plot(X_train , regressor.predict(X_train), color ='blue')
 ```
 ## 可视化测试结果
 ```python
 plt.scatter(X_test , Y_test, color = 'red')
 plt.plot(X_test , regressor.predict(X_test), color ='blue')
 ``` 


