---
layout: default
---

> mysql中没有提供递归查询的语句，我们通过mysql函数实现这种查询。

对于如下一张表privilege，递归查询**系统管理**下的记录。

id | name | parent_id
- | - | -
1 | 系统管理 | NULL
2 | 角色管理 | 1
3 | 用户管理 | 1
4 | 用户添加 | 3
5 | 用户删除 | 3
6 | 角色添加 | 2
7 | 角色删除 | 2

##### 需要使用的函数/sql
1. 假如要查询**系统管理**及其下级菜单，对应的sql语句如下所示。我们通过自定义函数把IN中的id查出来即可。
```sql
SELECT * FROM privilege WHERE IN (1,2,3,4,5,6,7);
```
2. FIND_IN_SET()函数:
&nbsp;&nbsp;&nbsp;&nbsp;假如字符串str 在由N 子链组成的字符串列表strlist 中，则返回值的范围在 1 到 N 之间。一个字符串列表就是一个由一些被‘,’符号分开的子链组成的字符串。如果第一个参数是一个常数字符串，而第二个是type SET列，则   FIND_IN_SET() 函数被优化，使用比特计算。如果str不在strlist 或strlist 为空字符串，则返回值为 0 。如任意一个参数为NULL，则返回值为 NULL。这个函数在第一个参数包含一个逗号(‘,’)时将无法正常运行。 
```sql
示例：SELECT FIND_IN_SET('2','1,A,2,4'); 返回值：3
```
3. GROUP_CONCAT()函数
> &nbsp;&nbsp;该函数将group by产生的同一个分组中的值连接起来，返回一个字符串结果。
4. 自定义函数
```sql
DROP FUNCTION IF EXISTS selectPrivilegeList;
CREATE FUNCTION selectPrivilegeList(id INT)
RETURNS VARCHAR(2000)
BEGIN
DECLARE sTemp VARCHAR(2000);
DECLARE subTemp VARCHAR(2000);
SET sTemp='$';
SET subTemp = CAST(id AS CHAR);
WHILE subTemp IS NOT NULL DO
SET sTemp= CONCAT(sTemp,',',subTemp);
SELECT GROUP_CONCAT(id) INTO subTemp FROM privilege WHERE FIND_IN_SET(parentId,subTemp)>0;
END WHILE;
RETURN sTemp;
END;
```
##### 调用
```sql
SELECT * FROM privilege WHERE FIND_IN_SET(id,selectPrivilegeList(1));
```
