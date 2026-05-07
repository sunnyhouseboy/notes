**异常流量检测 + Concept Drift 3个月学习计划（研0版）**

# **总目标**

· 掌握 Python、Numpy、Pandas、Scikit-learn、PyTorch 基础。

· 理解网络流量基础（TCP/IP、packet、flow、常见攻击）。

· 完成异常流量检测 baseline + 深度学习模型实验。

· 理解 Concept Drift 与在线学习。

· 能够阅读并复现1篇相关论文。

# **每日学习安排**

· 09:00-11:30 理论学习（课程/书籍/文档）

· 14:00-17:00 编码实践（Notebook/实验）

· 20:00-21:00 论文阅读与总结

# **Week1-4 基础阶段**

· Week1: Numpy + sklearn 基础，完成分类小项目

· Week2: 异常检测算法（Isolation Forest/LOF/KMeans）

· Week3: 网络基础（TCP/IP、Wireshark、常见攻击）

· Week4: CICIDS2017 数据集处理与 baseline
## **第一周**
这份执行到每一天的“作战简报”，将第一周的宏大目标拆解成了每天只需要专注几个小时的微小动作。

你的学习主阵地是 **Jupyter Notebook**，请务必保证每天的代码都在同一个工程文件夹下，这样周末整合时才会得心应手。

以下是你这 5 天的详细行动清单：

---

### 🗓️ Day 1: 降维打击 —— Numpy 矩阵与数组思维

今天是打底子的一天。机器学习不吃 Excel 表格，它只吃 Numpy 矩阵。

- **📚 具体学习资源**：
    
    - **视频**：B站搜索“Numpy 快速入门课”（找时长在 1-2 小时左右的精简版即可，不要看几十个小时的长篇大论）。
        
    - **文档**：Numpy 官方文档的 _NumPy quickstart_。
        
- **💡 怎么学（操作步骤）**：
    
    1. 打开 Jupyter，导入库：`import numpy as np`。
        
    2. 尝试把你 NSL-KDD 数据集里的一列提取出来，用 `np.array()` 变成数组。
        
    3. 故意制造一个报错：拿一个一维数组去强制转换形状。
        
- **✅ 掌握什么（通关标准）**：
    
    - **理解 Shape（形状）**：明白 `(100,)` 是一维向量，而 `(100, 1)` 是二维矩阵。
        
    - **掌握 Reshape**：能熟练敲出 `.reshape(-1, 1)` 这个在后续喂数据时必用的升维指令。
        
    - **基础切片**：能像切蛋糕一样，用 `X[:, 0:3]` 提取矩阵的前三列特征。
        

---

### 🗓️ Day 2: 消除数据代沟 —— 独热编码与特征缩放

这是第一周**最核心、最容易踩坑**的一天。你要把包含字母和异常极大值的数据，变成平滑的数字。

- **📚 具体学习资源**：
    
    - **视频**：B站搜索“菜菜的sklearn”，看第 3 期 **“数据预处理和特征工程”**（前 40 分钟就够了）。
        
    - **书籍**：《机器学习实战》（蜥蜴书）第 2 章的“处理文本和分类属性”与“特征缩放”两节。
        
- **💡 怎么学（操作步骤）**：
    
    1. 调用 `OneHotEncoder` 或 Pandas 的 `get_dummies`，把 `protocol_type` 这一列的 `tcp/udp/icmp` 变成由 0 和 1 组成的三列。
        
    2. 调用 `StandardScaler` 对 `src_bytes`（发送字节数）进行缩放。
        
    3. **关键对比**：缩放前打印一次这列的最大值，缩放后再打印一次，观察数值如何被压缩到 -3 到 3 之间。
        
- **✅ 掌握什么（通关标准）**：
    
    - **理解转换逻辑**：彻底搞懂 `.fit()`（计算均值和方差）和 `.transform()`（执行缩放操作）的区别。
        
    - **避坑必知**：永远只拿训练集去 `fit`，然后用算出来的均值去 `transform` 测试集。绝对不能把整个数据集混在一起缩放（这叫数据穿越，是极其严重的学术错误）。
        

---

### 🗓️ Day 3: 划分战场 —— 数据集拆分与模型初始化

不能拿全部数据训练模型，必须留一部分作为“期末考试卷”。

- **📚 具体学习资源**：
    
    - **官方文档**：Scikit-learn 官网搜索 `train_test_split`，直接看它底部的 Examples 代码块。
        
- **💡 怎么学（操作步骤）**：
    
    1. 设定 `X`（特征矩阵，不包含 label 列）和 `y`（标签列，即 normal 还是攻击）。
        
    2. 敲下这行魔法代码：`X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)`。
        
    3. 从 `sklearn.ensemble` 库中导入 `RandomForestClassifier` 并将其实例化：`clf = RandomForestClassifier(n_estimators=100)`。
        
- **✅ 掌握什么（通关标准）**：
    
    - **数据配比**：明白 8:2 或 7:3 是最科学的切分比例。
        
    - **随机种子的意义**：深刻理解为什么必须写 `random_state=42`（为了让你明天的实验和今天的实验结果完全一致，保证科研可复现性）。
        

---

### 🗓️ Day 4: 让子弹飞 —— 模型训练与预测

今天是见证黑盒运转的时刻，代码极其简单，但意义非凡。

- **📚 具体学习资源**：
    
    - **书籍**：《机器学习实战》（蜥蜴书）第 2 章“选择并训练模型”。
        
    - **博客**：搜索“通俗理解随机森林算法”，看看那些树是怎么长出来的。
        
- **💡 怎么学（操作步骤）**：
    
    1. 训练模型：执行 `clf.fit(X_train, y_train)`。由于 NSL-KDD 数据量有十几万，这个过程可能需要电脑跑个几十秒到一两分钟，喝口水耐心等待。
        
    2. 下达判决：执行 `y_pred = clf.predict(X_test)`，让模型对没见过的两万条测试数据下结论。
        
    3. 提取秘籍：执行 `clf.feature_importances_`，看看模型是根据什么抓住黑客的。
        
- **✅ 掌握什么（通关标准）**：
    
    - **理解 Fit 的本质**：知道这一行代码背后，计算机在疯狂计算特征分裂点（比如尝试 `count > 15` 能不能把 DoS 攻击分出来）。
        
    - **特征解读**：能够把 `feature_importances_` 里的数值，和你第一周画的热力图（比如 `serror_rate`）对应起来。
        

---

### 🗓️ Day 5: 审判席 —— 科学的评估体系

这是安全领域研究员的基本功，绝对不要拿着 Accuracy（准确率）去向导师汇报。

- **📚 具体学习资源**：
    
    - **视频**：B站搜索“机器学习 混淆矩阵与 F1-score”，找几分钟的动画原理解释。
        
    - **代码库**：查阅 `sklearn.metrics` 中的 `classification_report` 和 `confusion_matrix`。
        
- **💡 怎么学（操作步骤）**：
    
    1. 调用 `print(classification_report(y_test, y_pred))`，将输出的文本报告完整截图保存。
        
    2. 找一张纸，手动画一个 2x2 的格子，标出 TP（真阳性）、FP（假阳性）、TN（真阴性）、FN（假阴性）。然后对照你跑出的 `confusion_matrix` 结果，填入这四个格子。
        
- **✅ 掌握什么（通关标准）**：
    
    - **灵魂三问**：
        
        1. Precision（精确率）低说明什么？（误杀正常用户太多，频繁弹窗报警让管理员烦躁）。
            
        2. Recall（召回率）低说明什么？（漏掉了真实黑客，系统已经被黑了还不自知）。
            
        3. F1-Score 是什么？（为了平衡以上两者的综合成绩单）。
            

---

### ☕ 周末：复盘与连线

把这 5 天零散的代码片段，在一个干净的 Jupyter Notebook 里从上到下顺畅地跑通。添加好 Markdown 注释，给你的第一个完整的 AI 安全项目起个名字。

准备好迎接 Day 1 的 Numpy 挑战了吗？如果有任何代码报错，直接把报错信息扔给我。

# **Week5-8 深度学习阶段**

· Week5: PyTorch（tensor、autograd、Dataset、DataLoader）

· Week6: CNN/LSTM

· Week7: AutoEncoder 异常检测

· Week8: 整理代码并上传 GitHub

# **Week9-12 科研阶段**

· Week9: Concept Drift 理论（sudden/gradual/incremental/recurring）

· Week10: Drift Detection（DDM、EDDM、ADWIN、River）

· Week11: 阅读 survey 论文并做笔记

· Week12: 复现1篇 anomaly detection / drift 论文

# **额外补充**

· 每周2小时数学基础（线代、概率统计、梯度）

· 每周1小时 Linux + Git 基础

· 每周至少2篇论文笔记

