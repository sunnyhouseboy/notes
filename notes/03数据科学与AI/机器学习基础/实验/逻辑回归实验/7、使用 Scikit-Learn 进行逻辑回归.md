# 使用 Scikit-Learn 进行逻辑回归

## 目标
在本实验室中，您将：
- 使用 scikit-learn 训练一个逻辑回归模型。

## 数据集
让我们从和以前一样的数据集开始。

```python
import numpy as np

X = np.array([[0.5, 1.5], [1,1], [1.5, 0.5], [3, 0.5], [2, 2], [1, 2.5]])
y = np.array([0, 0, 0, 1, 1, 1])
````

## 拟合模型

下面的代码从 scikit-learn 导入了[逻辑回归模型](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html#sklearn.linear_model.LogisticRegression)。您可以调用 `fit` 函数在训练数据上拟合此模型。

```python
from sklearn.linear_model import LogisticRegression

lr_model = LogisticRegression()
lr_model.fit(X, y)
```
输出结结果：

|**参数名称 (Parameter)**|**当前值 (Value)**|**参数解释 (Explanation)**|
|---|---|---|
|**`penalty`**|`'l2'`|**正则化/惩罚项类型**。用于指定模型使用的惩罚项，常见的有 `'l1'`, `'l2'`, `'elasticnet'` 或 `None`。`'l2'` 是默认值，有助于防止模型过拟合。|
|**`dual`**|`False`|**对偶或原始方法**。仅当使用 `liblinear` 求解器且 `penalty='l2'` 时使用。通常当样本数量大于特征数量时，将其设置为 `False`。|
|**`tol`**|`0.0001`|**停止收敛的容忍度**。当优化的改进小于此值时，算法将停止训练。|
|**`C`**|`1.0`|**正则化强度的倒数**。必须是正浮点数。较小的值表示更强的正则化（限制模型复杂度），较大的值表示较弱的正则化。|
|**`fit_intercept`**|`True`|**是否计算截距（偏置项）**。如果为 `True`，模型将尝试拟合截距。如果数据已经中心化，可以设置为 `False`。|
|**`intercept_scaling`**|`1`|**截距缩放比例**。仅在使用 `solver='liblinear'` 且 `fit_intercept=True` 时生效。相当于向特征矩阵添加一个常数值特征。|
|**`class_weight`**|`None`|**类别权重**。用于处理不平衡的数据集。如果为 `None`，所有类别的权重都为 1。也可以设置为 `'balanced'` 自动根据样本频率调整权重。|
|**`random_state`**|`None`|**随机数生成器种子**。用于在数据打乱或选择某些求解器时控制随机性，保证结果可复现。|
|**`solver`**|`'lbfgs'`|**优化算法/求解器**。用于寻找参数最优解的算法。`'lbfgs'` 是默认值，适用于相对较小的数据集，其他选项包括 `'liblinear'`, `'newton-cg'`, `'sag'`, `'saga'` 等。|
|**`max_iter`**|`100`|**最大迭代次数**。求解器收敛前允许的最大迭代次数。如果模型未能收敛，可能需要增加此值。|
|**`multi_class`**|`'deprecated'`|**多分类策略**。图中显示为已弃用（deprecated），在较新版本中通常通过自动推断或不再作为独立参数使用。过去用于选择 `'ovr'`（一对多）或 `'multinomial'`（多项式分布）。|
|**`verbose`**|`0`|**日志冗长程度**。设置为任何正整数以输出训练过程中的详细信息。`0` 表示不输出日志。|
|**`warm_start`**|`False`|**是否热启动**。如果为 `True`，则重用上一次调用的解决方案作为本次拟合的初始化，这可以加快收敛速度。|
|**`n_jobs`**|`None`|**并行运行的 CPU 核心数**。`None` 通常意味着 1。设置为 `-1` 表示使用所有可用的处理器核心（仅对支持并行的求解器有效）。|
|**`l1_ratio`**|`None`|**Elastic-Net 混合参数**。取值范围在 0 到 1 之间。仅当 `penalty='elasticnet'` 时使用。它控制 `l1` 和 `l2` 正则化的比例。|
## 进行预测

您可以调用 `predict` 函数来查看该模型做出的预测。

```python
y_pred = lr_model.predict(X)

print("Prediction on training set:", y_pred)
```

**输出：**

```
Prediction on training set: [0 0 0 1 1 1]
```

## 计算准确率

您可以调用 `score` 函数来计算此模型的准确率。

```python
print("Accuracy on training set:", lr_model.score(X, y))
```

**输出：**

```
Accuracy on training set: 1.0
```
