### 数据库的核心9个动词
![[Pasted image 20231016104140.png]

### 数据库一些对象的定义
![[Pasted image 20231016105521.png]]

### 数据库的一些约束
![[Pasted image 20231016111602.png]]

### 修改基本表的操作
![[Pasted image 20231016130505.png]]
### 增加属性列

>像S表中增加类型为DATE的名为S_entrance数据
><mark style="background: #FFF3A3A6;">alter tabel s add S_entrace DATE;</mark>

### 删除属性列

>直接删除属性列
><mark style="background: #FFB86CA6;">alter table s drop column S_entrance</mark>

### 修改属性列

><mark style="background: #ABF7F7A6;">alter table s alter column Sage smallint</mark>
>><mark style="background: #FF5582A6;">ATTENTION</mark> 修改原有的列定义可能会破坏已有数据


### 增加/删除完整性约束
>##### 增加
>ALTER TABLE s ADD CONSTRAINT S_sname UNIQUE(Sname)
>##### 删除
>ALTER TABLES S DROP CONSTRAINT S sname

### 删除基本表
![[Pasted image 20231016131951.png]]
### 索引的定义
![[Pasted image 20231016132220.png]]