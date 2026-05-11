# 一、介绍
|特性|Series|DataFrame|
|:--|:--|:--|
|维度|一维|二维|
|索引|单索引|行索引+列名|
|数据存储|同质化数据类型|各列可不同数据类型|
|类比|Excel单列|整张Excel工作表|
|创建方式|`pd.Series([1,2,3])`|`pd.DataFrame({'col':[1,2,3]})`|
# 二、Series
**`Series` (Pandas)** 是一维的**带标签数组**，相当于电子表格里的一列。
## 1、创建方法
### ①基础创建
1. `s=pd.Series([1,2,3,4,5])`
2. `s=pd.Series([1,2,3,4,5],index=['A','B','C','D','E'],name='月份')`
### ②字典创建
1. `s=pd.Series({'a':1,'b':2,'c':3})`
2. `s2=pd.Series([10,2,3,4,5],index=['a','b','c','d','e'],name='月份')  
   `s1=pd.Series(s2,index=['a','b'])`
## 2、属性
| 属性               | 说明          | 属性       | 说明            |
| :--------------- | :---------- | :------- | :------------ |
| `index`          | Series的索引对象 | `loc[]`  | 显式索引，按标签索引或切片 |
| `values`         | Series的值    | `iloc[]` | 隐式索引，按位置索引或切片 |
| `dtype`或`dtypes` | Series的元素类型 | `at[]`   | 使用标签访问单个元素    |
| `shape`          | Series的形状   | `iat[]`  | 使用位置访问单个元素    |
| `ndim`           | Series的维度   |          |               |
| `size`           | Series的元素个数 |          |               |
| `name`           | Series的名称   |          |               |
## 3、访问数据
1. `s['a']`
2. `s[s<3]`
3. `s.head(x)#打印数据前x行,默认为5`
4. `s.tail(x)#打印数据后x行，默认为5`
## 4、常用方法
| 方法                  | 说明                     | 方法              | 说明                                         |
| :------------------ | :--------------------- | :-------------- | :----------------------------------------- |
| `head()`            | 查看前 n 行数据，默认 5 行       | `max()`         | 最大值                                        |
| `tail()`            | 查看后 n 行数据，默认 5 行       | `var()`         | 方差                                         |
| `isin()`            | 判断元素是否包含在参数集合中         | `std()`         | 标准差                                        |
| `isna()`            | 判断是否为缺失值（如 NaN 或 None） | `median()`      | 中位数                                        |
| `sum()`             | 求和，自动忽略缺失值             | `mode()`        | 众数（可返回多个）                                  |
| `mean()`            | 平均值                    | `quantile(q)`   | 分位数，q 取 0~1 之间                             |
| `min()`             | 最小值                    | `describe()`    | 常见统计信息（count、mean、std、min、25%、50%、75%、max） |
| `value_counts()`    | 每个唯一值的出现次数             | `sort_values()` | 按值排序                                       |
| `count()`           | 非缺失值数量                 | `replace()`     | 替换值                                        |
| `nunique()`         | 唯一值个数（去重）              | `keys()`        | 返回 Series 的索引对象                            |
| `unique()`          | 获取去重后的值数组              |                 |                                            |
| `drop_duplicates()` | 去除重复项                  |                 |                                            |
| `sample()`          | 随机抽样                   |                 |                                            |
| `sort_index()`      | 按索引排序                  |                 |                                            |
# 三、DataFrame
**`DataFrame` (Pandas)** 是二维的**数据表**，由多个 `Series` 拼装而成。
## 1、创建方法
1. 通过Series创建：`s1=pd.Series([1,2,3]) ` 
								`s2=pd.Series([4,5,6])`  
								`df=pd.DataFrame({'第一列':s1,'第二列':s2})`
2. 通过字典创建：`df=pd.DataFrame({  
					   ` 'id':[1,2,3],  `
						    `'name':['a','b','c'],` 
						    `'age':[10,20,30], ` 
					   ` 'score':[100,200,300]`  
							`}),index[1,2,3],columns=['id','age','name','score']` 
3. 字典列表：`data = [
    `{"id": 1, "name": "张三", "age": 18},`
    `{"id": 2, "name": "李四", "score": 95},`  
    `{"id": 3, "age": 20}`                   
     `]`
   `df = pd.DataFrame(data)` 
## 2、属性
| 属性      | 说明             | 属性     | 说明              |
| :------ | :------------- | :----- | :-------------- |
| index   | DataFrame的行索引  | loc[]  | 显式索引，按行列标签索引或切片 |
| values  | DataFrame的值    | iloc[] | 隐式索引，按行列位置索引或切片 |
| dtypes  | DataFrame的元素类型 | at[]   | 使用行列标签访问单个元素    |
| shape   | DataFrame的形状   | iat[]  | 使用行列位置访问单个元素    |
| ndim    | DataFrame的维度   | T      | 行列转置            |
| size    | DataFrame的元素个数 |        |                 |
| columns | DataFrame的列标签  |        |                 |
## 3、访问数据
### ①获取单列数据
1. `df['name']#Series类型`
2. `df.name#Series类型`
3. `df.[['name']]#DataFrame类型`
### ②多列数据
`df.[['name','age']]#DataFrame类型`
### ③查看部分数据
1. `df.head()`
2. `df.tail()`
3. `df[df.score>60]`
### ④随机取样
`df.sample(3)`
### ⑤查看整体摘要信息
`df.info()`
## 4、常见方法
| 方法                  | 说明                     | 方法              | 说明                                         |
| :------------------ | :--------------------- | :-------------- | :----------------------------------------- |
| `head()`            | 查看前 n 行数据，默认 5 行       | `max()`         | 最大值                                        |
| `tail()`            | 查看后 n 行数据，默认 5 行       | `var()`         | 方差                                         |
| `isin()`            | 判断元素是否包含在参数集合中         | `std()`         | 标准差                                        |
| `isna()`            | 判断是否为缺失值（如 NaN 或 None） | `median()`      | 中位数                                        |
| `sum()`             | 求和，自动忽略缺失值             | `mode()`        | 众数（可返回多个）                                  |
| `mean()`            | 平均值                    | `quantile(q)`   | 分位数，q 取 0~1 之间                             |
| `min()`             | 最小值                    | `describe()`    | 常见统计信息（count、mean、std、min、25%、50%、75%、max） |
| `value_counts()`    | 每个唯一值的出现次数             | `sort_values()` | 按值排序                                       |
| `count()`           | 非缺失值数量                 | `nlargest()`    | 返回某列最大的 n 条数据                              |
| `duplicated()`      | 是否重复                   | `nsmallest()`   | 返回某列最小的 n 条数据                              |
| `drop_duplicates()` | 去除重复项                  |                 |                                            |
| `sample()`          | 随机抽样                   |                 |                                            |
| `replace()`         | 替换值                    |                 |                                            |
| `sort_index()`      | 按索引排序                  |                 |                                            |
# 四、数据分析
## 1、步骤
数据收集->数据清洗->数据分析->数据可视化
## 2、数据的导入导出
### ①csv文件
`df=pd.read_csv('文件地址')`
`pd.to_csv('文件地址')`
### ③json文件
**读入：**
普通json文件：`df=pd.read_json('文件地址')`
字典列表：`with open(r"E:\数据练习\product.json",encoding='UTF-8-sig') as f:  
				  `data=json.load(f)`  
				`df=pd.DataFrame(data)`
复杂嵌套：`from pandas import json_normalize  
				`with open(r"E:\数据练习\user.json",encoding='UTF-8-sig') as f:`  
			    `data=json.load(f)`  
				`df=json_normalize(data)`
**读出：**`pd.to_json('文件地址')`
## 3、缺失值处理
缺失值的种类：`np.nan`，`None`，`pd.NA`
### ①缺失值判断
`df.isna()`
`df.isnull()`
### ②缺失值剔除
`df.dropna()#剔除一整条记录`
`df.dropna(how='all')#如果所有的值都是缺失值，删除这一行`
`df.dropna(thresh=1)#如果至少有n个值不是缺失值，就保留`
`df.dropna(axis=1)#剔除一整列记录`
`df.dropna(subset=['第一列'])#如果某列有缺失值，则删除这一行`
### ③缺失值填充
`df.fillna({'temp_max':20,'wind':2.5})#使用字典填充固定值`
`df.fillna(df[['temp_max','wind']].mean)#使用统计值来填充`
`df.ffill()#使用前面的相邻值填充`
`df.bfill()#使用后面的相邻值填充`
## 4、重复值处理
`df.duplicated()#一整条记录都是一样的`
`df.drop_duplicates()#去除重复行`
`df.drop_duplicates(subset=['name'])#根据指定列去重`
`df.drop_duplicates(subset=['name'],keep='last')#保留最后一次出现的行`
## 5、数据类型转换
`df['age']=df['age'].astype('int16')`
`df['gender']=df['gender'].astype('category')`
字符串处理效率最低
## 6、数据变形
### ①行列转置
`df.T`
### ②宽表变长表
`df2=pd.melt(df,id_vars['ID','name'],var_name='科目',value_name='分数')`
![[Pasted image 20260419163727.png]]
![[Pasted image 20260419163738.png]]
### ③长表变宽表
`pd.pivot(df2,index=['ID','name'],columns='科目',values='分数')`
![[Pasted image 20260419164101.png]]
![[Pasted image 20260419164109.png]]
### ④分列
`df[['first','last']]=df['name'].str.split(" ",expand=True)`
![[Pasted image 20260419164442.png]]
## 7、数据分箱
`pd.cut(df1['salary'],bins=3)#bins=n,分成n段区间，起始值、结束值是所有数据的最小值、最大值`
`pd.cut(df1[salary],bins=[0,10000,20000,30000])#bins=list,分成n段区间`
`df1['收入范围']=pd.cut(df1[salary],bins=[0,10000,20000,30000],labels=['高','中','低'])`
`pd.qcut(df1['salary'],3).value_counts()#按照人数或者概率均等分成三个区间`
`df.set_index('name',inplace=True)#inplace表示是否作用于原数据df`
`df.reset_index(inplace=True)`
`df.rename(columns={'age':'年龄'},index={0:4})`
## 8、时间数据的处理
`d=dp.Timestamp('2025-12-20 10:22')`
![[Pasted image 20260419171418.png]]
`a=pd.to_datetime('20150228')`
![[Pasted image 20260419171855.png]]
![[Pasted image 20260419172109.png]]
![[Pasted image 20260419172324.png]]
## 9、分组聚合
![[Pasted image 20260419173937.png]]