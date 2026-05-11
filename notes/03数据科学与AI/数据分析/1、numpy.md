# NumPy 全维度深度学习笔记：从基础属性到向量化进阶

## 一、 NumPy 核心哲学：ndarray

`ndarray` (NumPy) 是最底层的、纯粹的**数学矩阵**。它是高效科学计算的基础。

### 1.1 三大核心特性

- **多维性**：支持 0 维（标量）、1 维（向量）、2 维（矩阵）及更高维数组。
    
- **同质性**：所有元素类型必须一致，不能同时包含字符和数字。
    
- **高效性**：基于连续内存块存储，支持向量化运算，利用硬件并行性（SIMD）提升速度。
    

### 1.2 ndarray 核心属性

|**属性名称**|**解释**|**示例/备注**|
|---|---|---|
|**shape**|数组的形状|行数和列数，如 `(4,)` 或 `(2, 3)`|
|**ndim**|维度数量|数组是几维的|
|**size**|总元素个数|数组中所有元素的总数|
|**dtype**|元素类型|数组中元素的类型（如 `float64`）|
|**T**|转置|矩阵的行变列|
|**itemsize**|内存字节数|单个元素占用的内存字节数|
|**nbytes**|总内存占用|数组内存占用总量|
|**flags**|内存存储方式|存储细节信息|

---

## 二、 数组的创建例程

### 2.1 基础与形状预定义

- **基础创建**：`arr = np.array([1, 2, 3])`
    
- **副本创建**：`arr1 = np.array(arr)` 或 `np.copy(arr)`
    
- **全 0 矩阵**：`np.zeros((2, 3))` -> `[[0. 0. 0.], [0. 0. 0.]]`
    
- **全 1 矩阵**：`np.ones((2,))` -> `[1. 1.]`
    
- **未初始化**：`np.empty((4, 2))` (结果为内存随机值)
    
- **固定值填充**：`np.full((2, 3), 20)` -> `[[20 20 20], [20 20 20]]`
    

### 2.2 数列生成器

- **等差数列**：`np.arange(2, 12, 2)` (start, end(不含), step) -> `[2 4 6 8 10]`
    
- **等间隔数列**：`np.linspace(0, 10, 2)` (start, end(含), 份数) -> `[0. 10.]`
    
- **指数间隔**：`np.logspace(0, 4, 3, base=2)` -> `[1. 4. 16.]` (注：原文结果 0 应为 1)
    
- **单位矩阵**：`np.eye(3, 4, dtype=int)`
    
- **对角矩阵**：`np.diag([1, 2, 3])`
    

### 2.3 随机数组生成

- **0-1 随机浮点**：`np.random.rand(3, 4)` 或 `np.random.random_sample(4)`
    
- **指定范围浮点**：`np.random.uniform(3, 6, (2, 3))`
    
- **指定范围整数**：`np.random.randint(3, 30, (2, 3))`
    
- **正态分布**：`np.random.randn(2, 3)`
    
- **随机种子**：`np.random.seed(20)` (种子相同时生成的随机数一致)
    

---

## 三、 数据类型 (dtype)

|**数据类型**|**说明**|
|---|---|
|**bool**|布尔类型|
|**int8/16/32/64**|有符号整型（1, 2, 4, 8 字节）|
|**uint8/16/32/64**|无符号整型|
|**float16/32/64**|半精度、单精度、双精度浮点型|
|**complex64/128**|分别用两个 32/64 位浮点数表示的复数|

---

## 四、 索引、切片与变形

### 4.1 索引与基本切片

- **一维访问**：`arr[2]` 获取第 3 个元素；`arr[-1]` 获取最后一个元素。
    
- **二维访问**：`arr[row, col]`。如 `arr[1, 3]` 获取索引为 (1, 3) 的元素。
    
- **切片语法**：`[start:stop:step]`。
    
    - `arr[2:5]`：获取索引 2 到 4 的元素。
        
    - `arr[1, 2:5]`：获取第 2 行索引为 2 到 4 的元素。
        
- **提取整行/整列**：
    
    - `arr[1, :]` 或 `arr[1]`：访问第 2 行所有元素（返回 1-D 数组）。
        
    - `arr[:, 3]`：访问第 4 列所有元素。
        

### 4.2 条件索引（布尔索引）

- **单一条件**：`arr[arr > 10]`
    
- **复合条件**：`arr[(arr > 10) & (arr < 70)]` (注意：必须使用 `&` 不能用 `and`)。
    
- **行列组合**：`arr[2][arr[2] > 50]` (第 3 行大于 50 的数)。
    

### 4.3 形状重塑：reshape

- **基本重塑**：`arr.reshape(3, 2)`
    
- **自动计算重塑**：`arr.reshape(-1, 2)` (让 NumPy 自动计算行数)。
    
- **==重要：np.reshape(-1, 1)==**：
    
    - **作用**：升维，将平铺的“线”变成直立的“柱子”。
        
    - **1**：明确要求变为 1 列。
        
    - **-1**：占位符，自动计算行数以保证数据完整性。
        

---

## 五、 运算与广播机制

### 5.1 基础算术运算

- **数组间运算（逐元素）**：要求形状相同。
    
    - `a + b`, `a - b`, `a * b`, `a / b`, `a 2`
        
- **标量运算（缩放）**：
    
    - `a + 2` 或 `5 * a` (标量作用于每个元素)。
        
- **矩阵/点积运算**：
    
    - `a @ b` 或 `np.dot(a, b)`：矩阵乘法/点积。
        

### 5.2 矩阵广播机制 

**判断条件**：

1. **维度对齐**：维度不同的，在较短数组的前面（左边）补 1 直到维度数量相同。
    
2. **维度兼容**：从后向前逐个比较，对应维度大小**相等**，或**其中一个大小为 1**。
    
    _不满足以上条件的数组不可进行广播运算。_
    

---

## 六、 向量化进阶
### 6.1 numpy 数组 

NumPy 的基础数据结构是一个可索引的、n 维的、包含相同类型元素 (`dtype`) 的“数组 (array)”。这里我们对“维度 (dimension)”这个术语进行了重载：在上面它指向量中元素的数量，而在这里它指数组索引的数量。一维 (1-D) 数组有一个索引。在课程 1 中，我们将使用 NumPy 1-D 数组来表示向量。

- 1-D 数组，形状 (n,)：n 个元素，索引从 [0] 到 [n-1]。
    

### 6.2 向量创建
==更多方法参考[[1、numpy#二、 数组的创建例程]]==
NumPy 中的数据创建例程通常第一个参数就是对象的形状 (shape)。对于 1-D 结果，这可以是一个单一数值；对于多维结果，则是一个元组 (n, m, ...)。以下是使用这些例程创建向量的示例。

```python
# NumPy 分配内存并填充数值的例程
a = np.zeros(4);                print(f"np.zeros(4) :   a = {a}, a shape = {a.shape}, a data type = {a.dtype}")
a = np.zeros((4,));             print(f"np.zeros(4,) :  a = {a}, a shape = {a.shape}, a data type = {a.dtype}")
a = np.random.random_sample(4); print(f"np.random.random_sample(4): a = {a}, a shape = {a.shape}, a data type = {a.dtype}")
```

**输出结果：**

> np.zeros(4) : a = [0. 0. 0. 0.], a shape = (4,), a data type = float64
> 
> np.zeros(4,) : a = [0. 0. 0. 0.], a shape = (4,), a data type = float64
> 
> np.random.random_sample(4): a = [0.16054681 0.65264985 0.98302218 0.29864795], a shape = (4,), a data type = float64

某些数据创建例程不接受形状元组作为参数：

```python
# 分配内存并填充数组，但不接受形状元组作为输入参数的 NumPy 例程
a = np.arange(4.);              print(f"np.arange(4.):     a = {a}, a shape = {a.shape}, a data type = {a.dtype}")
a = np.random.rand(4);          print(f"np.random.rand(4): a = {a}, a shape = {a.shape}, a data type = {a.dtype}")
```

**输出结果：**

> np.arange(4.): a = [0. 1. 2. 3.], a shape = (4,), a data type = float64
> 
> np.random.rand(4): a = [0.04467047 0.14854614 0.24949402 0.02417095], a shape = (4,), a data type = float64

也可以手动指定数值：

```python
# 分配内存并使用用户指定值填充的 NumPy 例程
a = np.array([5,4,3,2]);  print(f"np.array([5,4,3,2]):  a = {a},     a shape = {a.shape}, a data type = {a.dtype}")
a = np.array([5.,4,3,2]); print(f"np.array([5.,4,3,2]): a = {a}, a shape = {a.shape}, a data type = {a.dtype}")
```

### 6.3 向量操作 

#### 6.3.1 索引

可以通过索引和切片访问向量元素。**索引**是指通过元素在数组中的位置来引用该元素。**切片**是指根据索引获取数组的子集。NumPy 索引从零开始，因此向量 $\mathbf{a}$ 的第 3 个元素是 `a[2]`。

```python
# 1-D 向量的索引操作
a = np.arange(10)
print(a)

# 访问一个元素
print(f"a[2].shape: {a[2].shape} a[2]  = {a[2]}, 访问一个元素返回一个标量")

# 访问最后一个元素，负索引从末尾开始计数
print(f"a[-1] = {a[-1]}")

# 索引必须在向量范围内，否则会报错
try:
    c = a[10]
except Exception as e:
    print("你会看到的错误信息是：")
    print(e)
```

#### 6.3.2 切片 
==可参考[[1、numpy#4.1 索引与基本切片]]==
切片使用一组三个值 (`start:stop:step`) 创建索引数组。
```python
# 向量切片操作
a = np.arange(10)
print(f"a         = {a}")

# 访问 5 个连续元素 (start:stop:step)
c = a[2:7:1];     print("a[2:7:1] = ", c)

# 访问 3 个元素，间隔为 2
c = a[2:7:2];     print("a[2:7:2] = ", c)

# 访问索引 3 及以上的所有元素
c = a[3:];        print("a[3:]    = ", c)

# 访问索引 3 以下的所有元素
c = a[:3];        print("a[:3]    = ", c)

# 访问所有元素
c = a[:];         print("a[:]     = ", c)
```

#### 6.3.3 单向量运算 
```python
a = np.array([1,2,3,4])
print(f"a             : {a}")
# 元素取反
b = -a 
print(f"b = -a        : {b}")

# 对所有元素求和，返回一个标量
b = np.sum(a) 
print(f"b = np.sum(a) : {b}")

# 求均值
b = np.mean(a)
print(f"b = np.mean(a): {b}")

# 元素平方
b = a**2
print(f"b = a**2      : {b}")
```

#### 6.3.4 向量-向量 逐元素运算

大多数 NumPy 算术、逻辑和比较运算符也适用于向量。这些运算符在逐元素的基础上工作。

$$\mathbf{a} + \mathbf{b} = \sum_{i=0}^{n-1} a_i + b_i$$
```python
a = np.array([ 1, 2, 3, 4])
b = np.array([-1,-2, 3, 4])
print(f"二元运算符逐元素工作: {a + b}")
```

#### 6.3.5 标量-向量 运算

向量可以通过标量值进行“缩放”。标量值就是一个普通的数字。该标量会乘以向量的所有元素。
```python
a = np.array([1, 2, 3, 4])

# 将向量 a 乘以标量
b = 5 * a 
print(f"b = 5 * a : {b}")
```

#### 6.3.6 向量-向量 点积

点积是线性代数和 NumPy 的支柱。点积将两个向量的对应值逐元素相乘，然后对结果求和。向量点积要求两个向量的维度必须相同。

**使用 for 循环**实现一个返回两个向量点积的函数：

$$x = \sum_{i=0}^{n-1} a_i b_i$$
```python
def my_dot(a, b): 
    """
   计算两个向量的点积
    """
    x=0
    for i in range(a.shape[0]):
        x = x + a[i] * b[i]
    return x

# 测试 1-D
a = np.array([1, 2, 3, 4])
b = np.array([-1, 4, 3, 2])
print(f"my_dot(a, b) = {my_dot(a, b)}")
```
让我们使用 `np.dot` 尝试相同的操作。
```python
# 测试 1-D
a = np.array([1, 2, 3, 4])
b = np.array([-1, 4, 3, 2])
c = np.dot(a, b)
print(f"NumPy 1-D np.dot(a, b) = {c}, np.dot(a, b).shape = {c.shape} ") 
c = np.dot(b, a)
print(f"NumPy 1-D np.dot(b, a) = {c}, np.dot(a, b).shape = {c.shape} ")
```

---

## 七、 NumPy 常用函数汇总表

|**分类**|**函数**|**解释/备注**|
|---|---|---|
|**基本数学**|`sqrt`, `exp`, `log`, `sin`, `abs`, `power`, `round`, `ceil`, `floor`|`exp`即$e^x$, `log`即$\ln x$|
|**统计函数**|`sum`, `mean`, `median`, `max`, `min`, `var`, `std`|均值、中位数、方差、标准差|
|**统计进阶**|`percentile(x, q)`, `argmax`, `argmin`|分位数、最大/小值索引|
|**比较/逻辑**|`greater`, `less`, `equal`, `logical_and/or/not`|比较与逻辑运算|
|**数组处理**|`concatenate`, `split`, `reshape`, `copy`, `unique`|拼接、分割、重塑、去重|
|**逻辑检索**|`where(condition, x, y)`, `any`, `all`, `in1d(a, b)`|条件选择、一真即真、全真即真|
|**排序**|`np.sort(x)`, `x.sort()`, `argsort`, `lexsort`|副本排序、就地排序、索引排序|
|**检测/其他**|`np.isnan(x)`, `np.select(conds, choices, default)`|缺失值检测、多条件选择|

---

## 八、 总结

通过本笔记，你掌握了 NumPy 的核心 `ndarray` 操作。在机器学习课程 1 中，最常见的操作是：

1. 提取样本向量 `X[i]`。
    
2. 计算权重与样本的点积 `np.dot(X[i], w)`。
    
3. 使用 `reshape(-1, 1)` 处理特征数据形状。