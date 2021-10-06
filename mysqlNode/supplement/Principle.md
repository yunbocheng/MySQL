## 对Mysql的原理补充

**在实际的开发中，SQL中的关键字使用大写，表名和字段名小写。**

**在SQL中，只有给列起别名的时候才使用双引号**

**MySQL中只有int有默认长度为11，其他的类型要给定长度。**

### 1. 数据库的编码方式

查看当前数据库的编码方式

```mysql
show variables like 'character%';
```

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20211005133037.png)

**在数据库中存在一种自动转换编码的机制**：即如果客户端输入的编码方式是gbk，服务端(数据库管理系统)的编码方式是utf8，此时数据库会自动将 **gbk-->utf8之后将数据存储。** 

![image-20211005133155743](https://gitee.com/YunboCheng/imageBad/raw/master/image/image-20211005133155743.png)

**在数据库中是utf8，而不是utf-8** 

## 2.查看建表和建库语句

- 查看建表语句

```mysql
show create table users;
```

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20211005133950.png)

- 查看建库语句

```mysql
show create database test;
```

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20211005134008.png)



### 3.删除语句

-  删除数据表

```mysql
drop table users;
```

- 删除数据库

```mysql
drop database test;
```

### 4. 解决编码问题

即使查看了客户端和服务端的编码格式都是utf8，但是还是不能存储汉字和准确的显示汉字。

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20211005140623.png)

此时解决问题的方式：

修改客户端的输入方式与输出方式

![image-20211005140526544](https://gitee.com/YunboCheng/imageBad/raw/master/image/image-20211005140526544.png)

![image-20211005140706091](https://gitee.com/YunboCheng/imageBad/raw/master/image/image-20211005140706091.png)

*GB2312*一般指*信息交换用汉字编码字符集*。

**注意：以上修改仅限于本次使用，下次从新打开需要再次进行设置**

### 5.新建一个数据库并添加数据流程

- 新建一个数据库

```mysql
create database test;
```

- 在该数据库中创建一张表

```mysql
use test;
create table users(id int(10),name varchar(50));
```

- 向表中添加数据

```mysql
insert into users values(1,'jack')
```

### 6. SQL三大语言分类

- DML : 数据操作语言。
- DDL ：数据定义语言。（外部导入的sql文件）
- DCL ：数据控制语言。

### 7. SQL中的注释

- 单行注释

```mysql
-- 单行注释(注意：在--后边必须加一个空格)
#单行注释
```

- 多行注释

```mysql
/*多行注释*/ 
```

### 8. 空值问题

- **SQL中的空值参与运算结果还是空值。**

此时可以使用 IFNULL 来解决

```mysql
IFNULL(salary,o) #代表当salary为null的时候，将这个salary当做0处理
```

### 9. 给列值起别名问题

- **AS可以省略不写，单引号、双引号都可以省略不写，当名字中含有特殊符号(比如空格的时候，必须写双引号或者单引号)**
- 在SQL语句中，只有起别名的时候使用双引号（不是必须使用，就是建议使用）

### 10. 去重问题

- 使用关键字 distinct

```mysql
SELECT DISTINCT job_id FROM emp;
```

- distinct 不能出现在两个字段之间。
- distinct 出现在两个字段之前：**代表两个字段联合去重**

### 11. 查看表结构

- 使用关键字 describe，这个使用的时候可以简写 **desc**

```mysql
DESC emp;
```

### 12. 比较运算

- **等于是“=”符号，而不是“== "符号。**
- **不等 <> 或者是 ！=**

### 13.其他运算符

- **IN(...,...,...) ** : 这个代表查询的数据是IN括号中的任意一个即可。

### 14.模糊查询

- **&**：代表零个或者多个任意字符。
- **_**：代表任意一个字符。

如果想要查询名字中带有下划线(_)的名字，**此时需要使用转义字符**

```mysql
SELECT name FROM users WHERE name LIKE '%\_%'; # \ 这个是SQL中默认的转义符号
SELECT name FROM users WHERE name LIKE '%$_%' ESCAPE '$'; #使用escape自定义。
```



如果要查询的名字中既包含a也包含e；

```mysql
SELECT name FROM users WHERE name LIKE '%a%e%' or name LIKE '%e%a%';
```

### 15. 空值与非空值查询

- **IS NULL** : 空值  (查询工资为NULL的数据)

```mysql
SELECT salary FROM users WHERE salary IS NULL;
```

- **IS NOT NULL ** : 非空值 (查询工资不为NULL的数据)

```mysql
SELECT salary FROM users WHERE salary IS NULL;
```

### 16. 排序问题

- **注意：在MySQL中，将排序语写在最后一句。**

- **升序排序使用关键字：ASC**  
- **在SQL语句中，默认就是升序排序。**

```mysql
SELECT salary FROM users ORDER BY salary ASC;
```

- **降序排序使用关键字：DESC**

```mysql
SELECT salary FROM users ORDER BY salary DESC;
```

### 17. 使用别名进行排序

- **注意：使用别名排序时，别名不加双引号。**

```
SELECT salary *12*(1+IFNULL(salaryadd)) as "年薪" FROM users ORDER BY 年薪 DESC;
```

### 18. 多列排序

**先将薪水进行降序排序，再将名字按照升序排序。**

**注意：先写哪个属性就先对哪个属性进行排序，按顺序执行。**

```mysql
SELECT salary,name FROM users ORDER BY salary DESC,name ASC;
```

### 19. 在MySQL中还可以进行计算

![image-20211005173023041](https://gitee.com/YunboCheng/imageBad/raw/master/image/image-20211005173023041.png)

### 20. Union 结果集相加

Union在使用的时候要求两个结果集的列数一致。

**注意：在Mysql中没有要求这两个列的类型一致，但是在Oracle中要求两个列的数据类型也要一致。**

- 将年龄为10岁和20岁的查询出来。

```mysql
SELECT age,name FROM users WHERE age = 10;
UNION
SELECT age,name FROM users WHERE age = 20;
```

### 21.limlit  分页

- 在MySQL中，limit在order by 之后执行。
- 语法格式：limit startIndex,length  （startIndex 是起始下标，length代表长度）
- 起始下标从0开始。
- **缺省写法：limlit 5** 代表取到是这组数据中的前5个。

找出工资排行前5的

```mysql
SELECT name,sal FROM emp order by sal desc  limlt 5;
```

找出工资排行在 [3-5] 的员工

```mysql
SELECT name,sal FROM emp order by sal desc limit 2,3;
```

```markdown
分页公式：设定pageSize代表每页显示的数据条数
int pageNO = 5; // 第五页
int pageSize = 10;  // 每页显示10条
int startIndex = (pageNO - 1) * pageSize;
得出分页的范围就是 ： limit startIndex,pageSize;
```

### 22.group by 分组函数 与  having 分组后继续筛选。

- sum 求和
- avg 平均值
- max 最大值
- min  最小值
- count 计数

**分组函数在使用的时候自动忽略NULL。不用对NULL使用IFNULL处理。**

**NULL并不是代表0，而是什么都没有。所以用is null 与 is not null 处理**

**数据库中不存在所有字段都是null的数据，但凡这条数据在数据库中存在，那么至少有一个字段不为null**

**在where中不能直接使用分组函数 group by **

分组函数可以联合使用

```mysql
SELECT avg(sal),max(sal),min(sal) FROM emp;
```

使用分组函数找出每个工作岗位的工资和。

```mysql
SELECT　job,sum(sal) from emp group by job;
```

使用having与group by解决：找出每个部门最高薪资，要求显示最高薪资大于3000的。

```mysql
SELECT depton,max(sal) AS maxsal FROM emp group by depton having maxsal>3000;
```

**注意：having不可以单独使用，having不可以代替where，having必须和group by 联合使用**

**having的效率要比where的效率低，在开发中尽量使用where**

使用where与group by 解决以上问题

```mysql
SELECT depton,max(sal) FROM emp WHERE sal > 3000 group by depton; 
```

where没有办法解决的

```mysql
SELECT depton,avg(sal) FROM emp group by depton having avg(sal) > 2500;
```

### 23.几种特殊的加法计算

- **两个数值类型计算结果就为数值型。**

```mysql
SELECT 100+90;  # 结果为:190
```

- **这是与Java的区别：在mysql中，只要进行计算，那么就会把字符类型转换为数值类型然后计算（此时字符型可以转换为数字）**

```mysql
SELECT '100'+90;  # 结果为：190
SELECT '100'+'90' # 结果为：190
```

- **当字符型不可以转化为数值型，此时就将字符型转换为0进行计算**

```mysql
SELECT 'haha'+100;  # 结果为：100
SELECT 'haha'+'houhouhou' # 结果为0
```

- **当有一方为NULL的时候，此时的计算结果为NULL，在mysql中只要有null参与的计算，其结果一定是null，除了分组函数(max()、sum())会自动忽略null，如果不想让其输出的为null，需要使用if null 处理，此时会将这个null视为用户给定的值处理**

```mysql
SELECT NULL+90; #结果为：null
```

- 使用**ifnull**处理。

```mysql
SELECT IFNULL(NULL,10)+90; // 结果为：100
SELECT IFNULL(NULL,0)+90;  // 结果为：90
```

### 24.查询常量 

```mysql
SELECT 100;
```

```mysql
SELECT 'String';
```

### 25.查询运算

```mysql
SELECT 100*100;
```

```mysql
SELECT 100%98;
```

### 26.查询函数(查询版本号)

```mysql
SELECT　VERSION();
```

### 27.拼接结果集（concat）

```mysql
SELECT CONCAT(first_name,last_name) as "姓名" FROM emp;
```

### 28.mysql中的数据类型

**varchar与char的区别：**

- varchar可以动态的分配用户输入数据的空间大小。
- char不可以动态的分配数据空间大小。

比如：如果用户设定的为 char(10)、varchar(10)，**用户输入男**，此时varchar会动态分配的空间为1，而char分配的空间是10。

**数据类型的最大长度**

- varchar 最长为255
- char 最长为255
- int 最长为11

**clob类型**

- 字符大对象，最多可以存储4G的字符串。比如：存储一篇文章，自我介绍等。**超过255个字符的采用CLOB字符大对象来存储**

blob
