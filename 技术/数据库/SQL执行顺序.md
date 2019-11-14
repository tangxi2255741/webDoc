# SQL语句执行顺序

(8)SELECT (9)DISTINCT <select_list>

(1)FROM <left_table> 

(3)<join_type> JOIN <right_table> 

(2)ON <join_condition>

(4)WHERE <where_condition>

(5)GROUP BY <group_by_list>

(6)WITH {CUBE | ROLLUP}

(7)HAVING <having_condition>

(10)ORDER BY <order_by_list>

(11)LIMIT <limit_number>

## 分析

> 每一步操作都会产生一个虚拟的表

​    (1)FROM：对FROM子句中的左右表执行笛卡尔积，产生虚拟表VT1

​    (2)ON：对虚拟表VT1应用ON筛选，符合<join_condition>的行被插入虚拟表VT2中

​    (3)JOIN：若指定了左外连接或右外连接，那么保留表中未匹配的行作为外部行添加到虚拟表VT2中，产生虚拟表VT3，若from包含两个以上的表，则对VT3和下一个表重复执行(1)(2)(3)

​    (4)WHERE：对虚拟表VT3应用WHERE过滤条件，符合<where_condition>的记录插入到虚拟表VT4中

​    (5)GROUP BY：据GROUP BY字句中的列，对VT4进行分组，产生虚拟表VT5

​    (6)WITH：对表VT5进行CUBE或ROLLUP，产生虚拟表VT6

​    (7)HAVING：对VT6应用HAVING过滤器，符合<having_condition>的记录才被插入虚拟表VT7

​    (8)SELECT：选择指定的列，插入虚拟表VT8中

​    (9)DISTINCT：对VT8去重复数据，产生虚拟表VT9

​    (10)ORDER BY：对VT9中的行根据<order_by_list>进行排序，产生虚拟表VT10

​    (11)LIMIT：从VT10中取出指定行，产生虚拟表VT11，并返回查询结果给用户