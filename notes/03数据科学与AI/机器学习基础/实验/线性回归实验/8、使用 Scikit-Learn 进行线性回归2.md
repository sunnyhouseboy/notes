# 使用 Scikit-Learn 进行线性回归

## 目标

在本实验中，你将：

- 利用 scikit-learn 实现基于正规方程的闭式解的线性回归。
    

## 工具

你将使用来自 scikit-learn 以及 matplotlib 和 NumPy 的函数。

```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.linear_model import LinearRegression
from lab_utils_multi import load_house_data
plt.style.use('./deeplearning.mplstyle')
np.set_printoptions(precision=2)
```

## 线性回归，闭式解

Scikit-learn 有一个[线性回归模型](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LinearRegression.html#sklearn.linear_model.LinearRegression)，它实现了闭式线性回归。

让我们使用早期实验的数据 —— 一栋 1000 平方英尺的房子以 300,000 美元售出，一栋 2000 平方英尺的房子以 500,000 美元售出。

|**面积 (1000 平方英尺)**|**价格 (1000 美元)**|
|---|---|
|1|300|
|2|500|

### 加载数据集

```python
X_train = np.array([1.0, 2.0])   # 特征
y_train = np.array([300, 500])   # 目标值
```

### 创建并拟合模型

下面的代码使用 scikit-learn 执行回归。

第一步创建一个回归对象。

第二步利用与该对象关联的方法之一 `fit`。这会执行回归，将参数拟合到输入数据。该工具包期望一个二维的 X 矩阵。

```python
linear_model = LinearRegression()
# X 必须是一个二维矩阵
linear_model.fit(X_train.reshape(-1, 1), y_train) 
```

_输出:_
![[Pasted image 20260512102401.png]]
### 查看参数

在 scikit-learn 中，$\mathbf{w}$ 和 $\mathbf{b}$ 参数分别被称为“系数”（coefficients）和“截距”（intercept）。

```python
b = linear_model.intercept_
w = linear_model.coef_
print(f"w = {w:}, b = {b:0.2f}")
print(f"'manual' prediction: f_wb = wx+b : {1200*w + b}")
```

_输出:_

```
w = [200.], b = 100.00
'manual' prediction: f_wb = wx+b : [240100.]
```

### 进行预测

调用 `predict` 函数生成预测。

```python
y_pred = linear_model.predict(X_train.reshape(-1, 1))

print("Prediction on training set:", y_pred)

X_test = np.array([[1200]])
print(f"Prediction for 1200 sqft house: ${linear_model.predict(X_test)[0]:0.2f}")
```

_输出:_

```
Prediction on training set: [300. 500.]
Prediction for 1200 sqft house: $240100.00
```

---

## 第二个例子

第二个例子来自之前一个具有多个特征的实验。最终的参数值和预测结果与该实验中未标准化的“长时间运行”结果非常接近。那个未标准化的运行花了几个小时才产生结果，而这个几乎是瞬间完成的。闭式解在像这样较小的数据集上表现良好，但在较大的数据集上可能需要大量的计算资源。

> 闭式解不需要进行标准化。

```python
# 加载数据集
X_train, y_train = load_house_data()
X_features = ['size(sqft)','bedrooms','floors','age']
```
X_train的数据形式：
![[Pasted image 20260512104757.png]]
```python
linear_model = LinearRegression()
linear_model.fit(X_train, y_train) 
```

```python
b = linear_model.intercept_
w = linear_model.coef_
print(f"w = {w:}, b = {b:0.2f}")
```

_输出:_

```
w = [  0.27 -32.62 -67.25  -1.47], b = 220.42
```

```python
print(f"Prediction on training set:\n {linear_model.predict(X_train)[:4]}" )
print(f"prediction using w,b:\n {(X_train @ w + b)[:4]}")#@是点乘的意思
print(f"Target values \n {y_train[:4]}")

x_house = np.array([1200, 3,1, 40]).reshape(-1,4)
x_house_predict = linear_model.predict(x_house)[0]
print(f" predicted price of a house with 1200 sqft, 3 bedrooms, 1 floor, 40 years old = ${x_house_predict*1000:0.2f}")
```

_输出:_

```
Prediction on training set:
 [295.18 485.98 389.52 492.15]
prediction using w,b:
 [295.18 485.98 389.52 492.15]
Target values 
 [300.  509.8 394.  540. ]
 predicted price of a house with 1200 sqft, 3 bedrooms, 1 floor, 40 years old = $318709.09
```