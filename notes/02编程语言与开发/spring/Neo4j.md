# Neo4j

## 命令

### 1、根据csv文件导入主体和关系

![image-20240420093408561](C:\Users\20680\AppData\Roaming\Typora\typora-user-images\image-20240420093408561.png)

LOAD CSV with headers FROM 'file:///relation.csv' AS row 

create (n:操作系统{name:row.body1})-[r:relation{property:row.relation}]->(m:操作系统{name:row.body2}) 

### 2、导入rdf

1、CALL n10s.graphconfig.init();

2、CREATE CONSTRAINT n10s_unique_uri FOR (r:Resource) REQUIRE r.uri IS UNIQUE

3、CALL n10s.rdf.import.fetch("file:///D:\\neo4j-community-3.5.5\\import\\some_rdf_file.rdf", "RDF/XML");

### 3、查询

![image-20240420093628806](C:\Users\20680\AppData\Roaming\Typora\typora-user-images\image-20240420093628806.png)

![image-20240420093641897](C:\Users\20680\AppData\Roaming\Typora\typora-user-images\image-20240420093641897.png)

### 4、创建节点

1、create(n:标签{属性名：属性})	例如：create(n:一级标题 {uri:'操作系统引论'})

2、一次性创造多个相同标签的节点：

UNWIND [{uri: '操作系统引论'}, {uri: '操作系统发展的主要动力'},{uri: '操作系统的主要功能'},{uri: '操作系统的作用'},		{uri: '操作系统的发展过程'},{uri: '操作系统的基本特性'},{uri: '操作系统的目标'}] AS nodes

CREATE (n:二级标题)

SET n = nodes

3、批量创建关系

match(a:二级标题{uri:'操作系统的目标'}) 

match(b:三级标题) where id(b)>=50 and id(b)<=53

create (a)-[:subclass]->(b)

### 5、删除

1、清空所有数据：MATCH (n) OPTIONAL  MATCH (n)-[r]-()  DELETE n,r

2、删除有关系的节点：删除关系：match(n:person{name:"戴七"})-[r]->(m) delete r

match(n:person{name:"戴七"}) detach delete n

3、删除无关系的节点：match (n:person{name:"hhh"}) delete n

### 6、修改

match(n:person{name:"肖三"}) 	set n.phone=12345678999	return n.name, n.phone

MATCH (n:concept {grade: '八级概念'})

SET n:八级概念

MATCH (n:Resource)

set n.uri=REPLACE(n.uri, 'http://www.semanticweb.org/20680/ontologies/2024/3/15/untitled-ontology-19#', '')

### 7、导出为csv

call apoc.export.csv.query("MATCH (n)-[r]-(m) return n,r,m","file:/main1.csv",	{format:'plain',cypherFormat:'updateStructure'})

## 导入过程

1、LOAD CSV with headers FROM 'file:///body.csv' AS row 

create (n:操作系统{name:row.body,grade:row.concept})

2、LOAD CSV with headers FROM 'file:///body.csv' AS row 

match (n:操作系统{name:row.body}) where row.concept='一级概念'

set n:一级概念

3、LOAD CSV with headers FROM 'file:///body.csv' AS row 

match (n:操作系统{name:row.body}) where row.importance='high'

set n:important

4、load CSV with headers FROM 'file:///relation.csv' AS row 

match (from:操作系统{name:row.body1})

match (to:操作系统{name:row.body2})

create (from)-[r:relation{type:row.relation}]->(to)

5、create(n:课程{name:'操作系统'}) with n match(m:`一级概念`) create (n)-[r:relation{name:'Include'}]->(m)

**导入之前一定要确保编码为utf-8**