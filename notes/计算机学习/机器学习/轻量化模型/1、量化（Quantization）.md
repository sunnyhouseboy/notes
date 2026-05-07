# 一、概述
## 1、目的
旨在以较低精度表示模型的参数
## 2、神经网络中可量化的数据
1. 权重：神经网络的参数
2. 激活值：传播到神经网络层的值
## 3、优点
1. 更小的模型
2. 速度提升
	内存带宽
   - GEMM：通用矩阵乘法（矩阵与矩阵相乘）
   - GEMV：通用矩阵向量乘法（矩阵与向量相乘）
## 4、缺点
- 量化误差
- 重新训练（量化感知训练）
- 硬件支持有限
- 需要校准数据集
- 打包/解
# 二、线性量化
使用线性映射将高精度范围映射到低精度范围
公式：r=s(q-z)
有两个参数：缩放因子s，零点z
其中缩放因子以原始张量相同的数据类型存储，z以量化后张量相同的数据类型存储
r=s(q-z)
r/s=q-z
r/s+z=q
q=round(r/s+z)
q=int(round(r/s+z))
`import torch`
`def linear_q_with_scale_and_zero_point(tensor, scale, zero_point, dtype=torch.int8):`
`    scaled_and_shifted_tensor = tensor / scale + zero_point`
`    rounded_tensor = torch.round(scaled_and_shifted_tensor)`
`    q_min = torch.iinfo(dtype).min`
`    q_max = torch.iinfo(dtype).max`
`    q_tensor = rounded_tensor.clamp(q_min, q_max).to(dtype)`
`    return q_tensor`
