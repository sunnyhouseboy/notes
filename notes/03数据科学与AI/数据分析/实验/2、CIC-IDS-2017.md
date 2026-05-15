# CIC-IDS-2017数据集
## Label各标签的含义

|标签名（Label）|中文含义|攻击类型解释|特点|
|---|---|---|---|
|**BENIGN**|正常流量|合法用户产生的正常网络通信数据|作为正常类别，通常数量最多|
|**FTP-Patator**|FTP暴力破解攻击|攻击者不断尝试用户名和密码登录FTP服务|大量重复登录请求，连接频繁失败|
|**SSH-Patator**|SSH暴力破解攻击|暴力尝试SSH远程登录账号密码|与FTP类似，但目标是SSH服务|
|**DoS Hulk**|Hulk拒绝服务攻击|发送大量HTTP请求耗尽服务器资源|流量大、请求密集、持续时间短|
|**DoS GoldenEye**|GoldenEye拒绝服务攻击|模拟大量HTTP连接拖垮Web服务器|建立大量连接，占用服务资源|
|**DoS Slowloris**|Slowloris慢速攻击|缓慢发送HTTP请求头，保持连接不释放|连接多但速率低，很隐蔽|
|**DoS Slowhttptest**|Slow HTTP Test攻击|缓慢发送HTTP请求体或响应数据|与Slowloris类似，拖慢服务器|
|**Heartbleed**|Heartbleed漏洞攻击|利用OpenSSL漏洞读取服务器内存数据|少见但危险，属于漏洞利用攻击|
|**Web Attack – Brute Force**|Web暴力破解|针对Web登录页面进行密码猜解|多次登录尝试，请求重复性强|
|**Web Attack – XSS**|跨站脚本攻击|注入恶意JavaScript代码到网页|常见Web漏洞攻击|
|**Web Attack – Sql Injection**|SQL注入攻击|在输入中插入SQL语句攻击数据库|可导致数据泄露或数据库破坏|
|**Infiltration**|内网渗透攻击|攻击者进入内网后横向移动或植入恶意程序|行为复杂，较难检测|
|**Bot**|僵尸网络流量|被控制主机与C2服务器通信|周期性通信、异常连接模式|
|**PortScan**|端口扫描|扫描目标开放端口和服务信息|短时间访问大量端口|
|**DDoS**|分布式拒绝服务攻击|多台主机同时发送大量请求瘫痪目标|流量爆发性极强|

---

### 1. 正常类

- `BENIGN`
    

---

### 2. 暴力破解类

- `FTP-Patator`
    
- `SSH-Patator`
    
- `Web Attack – Brute Force`
    

特点：

- 高频重复尝试
    
- 登录失败多
    

---

### 3. DoS / DDoS 类

- `DoS Hulk`
    
- `DoS GoldenEye`
    
- `DoS Slowloris`
    
- `DoS Slowhttptest`
    
- `DDoS`
    

特点：

- 流量异常高 or 连接异常多
    

---

### 4. Web攻击类

- `Web Attack – XSS`
    
- `Web Attack – Sql Injection`
    

特点：

- 针对Web应用漏洞
    

---

### 5. 侦察/扫描类

- `PortScan`
    

特点：

- 探测端口和服务
    

---

### 6. 高级攻击类

- `Bot`
    
- `Infiltration`
    
- `Heartbleed`
    

特点：

- 更复杂、更隐蔽
    

---
## 字段含义分析
这里我根据你提供的实际字段列表（79个特征列），结合你之前文档中的含义解释，为你重新梳理并生成了一份完整的 **字段含义分析**。

由于你提供的字段列表中包含了部分原文档未提及的衍生特征（例如 `Packet Length Variance`，`Bulk` 相关特征等），我已补充了这些新字段的中文含义和解释，以保证字典的完整性。

---

### 1. 基本信息 (Basic Flow Info)


|**列名**|**中文含义**|**解释**|
|---|---|---|
|**Destination Port**|目标端口|接收方端口号|

---

### 2. 流量统计特征 (Traffic Statistics)

_统计整条流或单向流的基础包数量与容量信息。_

|**列名**|**中文含义**|**解释**|
|---|---|---|
|**Flow Duration**|流持续时间|从第一包到最后一个包的时间间隔（微秒）|
|**Total Fwd Packets**|前向总包数|源IP向目标IP发送的总数据包数|
|**Total Backward Packets**|后向总包数|目标IP向源IP发送的总数据包数|
|**Total Length of Fwd Packets**|前向总字节数|前向数据包的总长度|
|**Total Length of Bwd Packets**|后向总字节数|后向数据包的总长度|
|**Down/Up Ratio**|下载/上传比例|后向与前向的数据量/包比例|
|**act_data_pkt_fwd**|前向实际数据包数|前向传输中实际携带有效载荷（Payload）的包数|

---

### 3. 速率特征 (Rate Features)

_常用于检测高频攻击，如 DDoS 或 PortScan。_

| **列名**             | **中文含义** | **解释**     |
| ------------------ | -------- | ---------- |
| **Flow Bytes/s**   | 每秒字节数    | 整条流的数据传输速率 |
| **Flow Packets/s** | 每秒包数     | 整条流的包传输速率  |
| **Fwd Packets/s**  | 前向每秒包数   | 源向目标的包传输速率 |
| **Bwd Packets/s**  | 后向每秒包数   | 目标向源的包传输速率 |

---

### 4. 包长度统计 (Packet Length Features)

_描述数据包大小的分布特征，常用于识别特定协议或异常的Payload注入。_

**前/后向包长特征：**

|**列名**|**中文含义**|**解释**|
|---|---|---|
|**Fwd Packet Length Max**|前向最大包长|前向数据包中的最大长度|
|**Fwd Packet Length Min**|前向最小包长|前向数据包中的最小长度|
|**Fwd Packet Length Mean**|前向平均包长|前向数据包长度的平均值|
|**Fwd Packet Length Std**|前向包长标准差|前向数据包长度的波动程度|
|**Bwd Packet Length Max**|后向最大包长|后向数据包中的最大长度|
|**Bwd Packet Length Min**|后向最小包长|后向数据包中的最小长度|
|**Bwd Packet Length Mean**|后向平均包长|后向数据包长度的平均值|
|**Bwd Packet Length Std**|后向包长标准差|后向数据包长度的波动程度|

**整体流包长特征：**

|**列名**|**中文含义**|**解释**|
|---|---|---|
|**Min Packet Length**|整体最小包长|整条流中的最小包长度|
|**Max Packet Length**|整体最大包长|整条流中的最大包长度|
|**Packet Length Mean**|整体平均包长|整条流所有包的平均长度|
|**Packet Length Std**|包长标准差|整条流包长的波动程度|
|**Packet Length Variance**|包长方差|整条流包长的方差|
|**Average Packet Size**|平均包大小|平均每个数据包的大小|
|**Avg Fwd Segment Size**|前向平均段大小|平均每个前向TCP段的大小（与Fwd Pkt Len Mean类似）|
|**Avg Bwd Segment Size**|后向平均段大小|平均每个后向TCP段的大小（与Bwd Pkt Len Mean类似）|

---

### 5. 时间间隔特征 (Inter Arrival Time, IAT)

_描述包与包之间到达的时间间隔（微秒），是识别慢速攻击（如Slowloris）和僵尸网络（Bot）心跳的重要特征。_

**整条流与前向：**

|**列名**|**中文含义**|**解释**|
|---|---|---|
|**Flow IAT Mean**|流平均到达间隔|流中两个连续包之间的平均时间|
|**Flow IAT Std**|流间隔标准差|流中包到达间隔的波动|
|**Flow IAT Max**|流最大间隔|两个包之间的最大时间差|
|**Flow IAT Min**|流最小间隔|两个包之间的最小时间差|
|**Fwd IAT Total**|前向总间隔时间|前向包到达间隔的总和|
|**Fwd IAT Mean**|前向平均间隔|前向包之间的平均到达时间|
|**Fwd IAT Std**|前向间隔标准差|前向包间隔时间的波动|
|**Fwd IAT Max**|前向最大间隔|前向包之间的最大时间差|
|**Fwd IAT Min**|前向最小间隔|前向包之间的最小时间差|

**后向：**

|**列名**|**中文含义**|**解释**|
|---|---|---|
|**Bwd IAT Total**|后向总间隔时间|后向包到达间隔的总和|
|**Bwd IAT Mean**|后向平均间隔|后向包之间的平均到达时间|
|**Bwd IAT Std**|后向间隔标准差|后向包间隔时间的波动|
|**Bwd IAT Max**|后向最大间隔|后向包之间的最大时间差|
|**Bwd IAT Min**|后向最小间隔|后向包之间的最小时间差|

---

### 6. TCP 标志位特征 (Flags)

_TCP连接状态的监控，对端口扫描（PortScan）和各类网络层 DoS 攻击极为敏感。_

|**列名**|**中文含义**|**解释**|
|---|---|---|
|**Fwd PSH Flags**|前向PSH标志包数|前向包含PSH（推送数据）标志的包数|
|**Bwd PSH Flags**|后向PSH标志包数|后向包含PSH标志的包数|
|**Fwd URG Flags**|前向URG标志包数|前向包含URG（紧急指针）标志的包数|
|**Bwd URG Flags**|后向URG标志包数|后向包含URG标志的包数|
|**FIN Flag Count**|FIN标志计数|包含连接结束（FIN）标志的总包数|
|**SYN Flag Count**|SYN标志计数|包含请求建立连接（SYN）标志的总包数|
|**RST Flag Count**|RST标志计数|包含重置连接（RST）标志的总包数|
|**PSH Flag Count**|PSH标志计数|包含推送数据（PSH）标志的总包数|
|**ACK Flag Count**|ACK标志计数|包含确认（ACK）标志的总包数|
|**URG Flag Count**|URG标志计数|包含紧急数据（URG）标志的总包数|
|**CWE Flag Count**|CWE标志计数|拥塞窗口减小（CWR）标志计数|
|**ECE Flag Count**|ECE标志计数|ECN-Echo标志计数（与拥塞控制有关）|

---

### 7. Header 及底层特征 (Header & Base Features)

|**列名**|**中文含义**|**解释**|
|---|---|---|
|**Fwd Header Length**|前向头部长度|前向数据包的 TCP/IP 头部总长度|
|**Bwd Header Length**|后向头部长度|后向数据包的 TCP/IP 头部总长度|
|**Fwd Header Length.1**|前向头部长度（副本）|_数据集中经常出现的冗余字段，与上述字段一致_|
|**min_seg_size_forward**|前向最小段大小|前向传输中观察到的最小 TCP 段大小|

---

### 8. 批量传输特征 (Bulk Features)

_描述大块数据（Bulk）在流中的传输情况。正常大文件传输通常会有较高的 Bulk 率。_

|**列名**|**中文含义**|**解释**|
|---|---|---|
|**Fwd Avg Bytes/Bulk**|前向平均批量字节数|前向单次批量传输的平均字节数|
|**Fwd Avg Packets/Bulk**|前向平均批量包数|前向单次批量传输的平均数据包数|
|**Fwd Avg Bulk Rate**|前向平均批量传输率|前向批量传输的数据吞吐率|
|**Bwd Avg Bytes/Bulk**|后向平均批量字节数|后向单次批量传输的平均字节数|
|**Bwd Avg Packets/Bulk**|后向平均批量包数|后向单次批量传输的平均数据包数|
|**Bwd Avg Bulk Rate**|后向平均批量传输率|后向批量传输的数据吞吐率|

---

### 9. 子流特征 (Subflow)

_子流是将整体连接按照特定窗口切割后的统计量。_

|**列名**|**中文含义**|**解释**|
|---|---|---|
|**Subflow Fwd Packets**|子流前向包数|子流中源向目标发送的包数|
|**Subflow Fwd Bytes**|子流前向字节数|子流中源向目标发送的总字节数|
|**Subflow Bwd Packets**|子流后向包数|子流中目标向源发送的包数|
|**Subflow Bwd Bytes**|子流后向字节数|子流中目标向源发送的总字节数|

---

### 10. 窗口大小特征 (Window Features)

_TCP 滑动窗口大小，用于流量控制。常用于识别特定操作系统或扫描工具特征。_

|**列名**|**中文含义**|**解释**|
|---|---|---|
|**Init_Win_bytes_forward**|初始前向窗口大小|前向连接建立时设定的初始TCP窗口字节数|
|**Init_Win_bytes_backward**|初始后向窗口大小|后向连接建立时设定的初始TCP窗口字节数|

---

### 11. 活跃/空闲时间特征 (Activity & Idle)

_将网络流按时间片段划分，统计其处于传输数据（Active）或无数据传输（Idle）状态的时间。_

|**列名**|**中文含义**|**解释**|
|---|---|---|
|**Active Mean**|活跃平均时间|流处于活跃状态的平均持续时间|
|**Active Std**|活跃时间标准差|活跃时间的波动程度|
|**Active Max**|最大活跃时间|连续活跃状态的最长时间|
|**Active Min**|最小活跃时间|连续活跃状态的最短时间|
|**Idle Mean**|空闲平均时间|流处于空闲（无包传输）状态的平均时间|
|**Idle Std**|空闲时间标准差|空闲时间的波动程度|
|**Idle Max**|最大空闲时间|最长一次空闲状态的时间|
|**Idle Min**|最小空闲时间|最短一次空闲状态的时间|

---

### 12. 标签分类列 (Label)

_机器学习模型进行分类的目标变量（Target Variable）。_

| **列名**    | **中文含义** | **解释**                      |
| --------- | -------- | --------------------------- |
| **Label** | 标签       | 标记当前流是正常流量（BENIGN）还是对应的攻击类型 |
1、Destination Port','Bwd Packet Length Std','Flow Duration',
2、'Destination Port','Bwd Packet Length Std','Flow Duration','Init_Win_bytes_forward','Flow Bytes/s'
3、'Destination Port','Bwd Packet Length Std','Flow Duration','Flow IAT Max','Init_Win_bytes_forward','Flow Bytes/s','PSH Flag Count'