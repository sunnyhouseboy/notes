# 使用 Scikit-Learn 进行线性回归

有一个名为 [scikit-learn](https://scikit-learn.org/stable/index.html) 的开源且可商用的机器学习工具包。这个工具包包含了你将在本课程中学习到的许多算法的实现。

## 目标

在本实验中，你将：

- 使用 scikit-learn 来实现基于梯度下降的线性回归
    

## 工具

你将使用来自 scikit-learn、matplotlib 和 NumPy 的函数。

```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.linear_model import SGDRegressor
from sklearn.preprocessing import StandardScaler
from lab_utils_multi import  load_house_data
from lab_utils_common import dlc
np.set_printoptions(precision=2)
plt.style.use('./deeplearning.mplstyle')
```

## 梯度下降

Scikit-learn 提供了一个梯度下降回归模型 [sklearn.linear_model.SGDRegressor](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.SGDRegressor.html#examples-using-sklearn-linear-model-sgdregressor)。与你之前自己实现的梯度下降类似，该模型在输入数据经过归一化处理后表现最佳。[sklearn.preprocessing.StandardScaler](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.StandardScaler.html#sklearn.preprocessing.StandardScaler) 将执行与之前实验中一样的 z-score 归一化。在这里，它被称为“标准分数”（standard score）。

## 加载数据集

```python
X_train, y_train = load_house_data()
X_features = ['size(sqft)','bedrooms','floors','age']
```

## 缩放/归一化训练数据

```python
scaler = StandardScaler()
X_norm = scaler.fit_transform(X_train)
print(f"Peak to Peak range by column in Raw        X:{np.ptp(X_train,axis=0)}")   
print(f"Peak to Peak range by column in Normalized X:{np.ptp(X_norm,axis=0)}")
```
**输出：**
```
Peak to Peak range by column in Raw        X:[2.41e+03 4.00e+00 1.00e+00 9.50e+01]
Peak to Peak range by column in Normalized X:[5.85 6.14 2.06 3.69]
```

## 创建并拟合回归模型

```python
sgdr = SGDRegressor(max_iter=1000)
sgdr.fit(X_norm, y_train)
print(sgdr)
print(f"number of iterations completed: {sgdr.n_iter_}, number of weight updates: {sgdr.t_}")
```

**输出：**

```
SGDRegressor()
number of iterations completed: 111, number of weight updates: 10990.0
```

## 查看参数

注意，这些参数是与**归一化**后的输入数据相关联的。拟合出的参数与上一实验中使用相同数据得出的参数非常接近。

```python
b_norm = sgdr.intercept_
w_norm = sgdr.coef_
print(f"model parameters:                   w: {w_norm}, b:{b_norm}")
print( "model parameters from previous lab: w: [110.56 -21.27 -32.71 -37.97], b: 363.16")
```

**输出：**

```
model parameters:                   w: [109.95 -20.97 -32.35 -38.07], b:[363.15]
model parameters from previous lab: w: [110.56 -21.27 -32.71 -37.97], b: 363.16
```

## 进行预测

预测训练数据的目标值。请同时使用 `predict` 方法以及使用 _w_ 和 _b_ 来进行计算。

```python
# make a prediction using sgdr.predict()
y_pred_sgd = sgdr.predict(X_norm)
# make a prediction using w,b. 
y_pred = np.dot(X_norm, w_norm) + b_norm  
print(f"prediction using np.dot() and sgdr.predict match: {(y_pred == y_pred_sgd).all()}")

print(f"Prediction on training set:\n{y_pred[:4]}" )
print(f"Target values \n{y_train[:4]}")
```

**输出：**

```
prediction using np.dot() and sgdr.predict match: True
Prediction on training set:
[295.17 485.84 389.62 492.  ]
Target values 
[300.  509.8 394.  540. ]
```

## 绘制结果

让我们将预测值与目标值进行绘图对比。

```python
# plot predictions and targets vs original features    
fig,ax=plt.subplots(1,4,figsize=(12,3),sharey=True)
for i in range(len(ax)):
    ax[i].scatter(X_train[:,i],y_train, label = 'target')
    ax[i].set_xlabel(X_features[i])
    ax[i].scatter(X_train[:,i],y_pred,color=dlc["dlorange"], label = 'predict')
ax[0].set_ylabel("Price"); ax[0].legend();
fig.suptitle("target versus prediction using z-score normalized model")
plt.show()
```
![[Pasted image 20260512101153.png]]