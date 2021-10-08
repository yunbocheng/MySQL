## 对Mysql的原理补充

**在实际的开发中，SQL中的关键字使用大写，表名和字段名小写。**

**在SQL中，只有给列起别名的时候才使用双引号**

**MySQL中只有int有默认长度为11，其他的类型要给定长度。**

**数据库中的命名规则：全部使用小写字母，多个单词之间使用"_" 进行分隔。**

**MySQL中存在一种自动修改列名机制，当两个表联接时，如果两个表的列名相等时，此时mysql会自动将第二章表的列名修改，按照出现的表的顺序修改。**

![image-20211007163113529](https://gitee.com/YunboCheng/imageBad/raw/master/image/image-20211007163113529.png)

**在DOS中编写mysql语句时，可以写上注释，系统会自动忽略。**

**查询时候的执行顺序**

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20211008094433.png)

**以下代码是正确的，在group by 和 having还有ordey by 之后是支持别名的(在mysql是支持的，但是在Oracle中不支持)，但是在where后不支持别名，在显示开发中尽量不用别名处理。**

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20211008094622.png)、

**gak编码方式中汉字占两个字节，utf8中汉字占3个字节，英文和数字都占一个字节。**

### 1. 数据库的编码方式

查看当前数据库的编码方式

```mysql
show variables like 'character%';
```

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20211005133037.png)

**在数据库中存在一种自动转换编码的机制**：即如果客户端输入的编码方式是gbk，服务端(数据库管理系统)的编码方式是utf8，此时数据库会自动将 **gbk-->utf8之后将数据存储。** 

![image-20211005133155743](https://gitee.com/YunboCheng/imageBad/raw/master/image/image-20211005133155743.png)

**在数据库中是utf8，而不是utf-8** 

### 2.查看建表和建库语句

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

#### 5.1 if exist与 if not exists 的用法

- if exists ：代表如果存在。这个多用于在删除表和数据库的时候使用。

```mysql
DROP table IF EXISTS peolpe;  # 这个代表如果people这张表存在就删除，即使不存在不会报错
DROP database IF EXISTS test; 
```

- if not exists : 代表如果不存在。这个多用于在创建表和数据库的时候使用。

```mysql
CREATE database IF NOT EXISTS test; # 代表如果不存在，就创建这个数据库，存在不会报错。
CREATE table IF NOT EXISTS test;
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

```mysql
SELECT SUM(DISTINCT salary),SUM(salary) FROM emp; 
# 第一个结果是工资去重后的和 第二个是不去重的结果。
```

- distinct与分组函数联合使用

```mysql
SELECT SUM(distinct salary),count(distinct salsry) from emp;
```

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

- **排序的列中含有NULL，此时将NULL看作是无穷大** 
- 降序的时候NULL在第一个。
- 升序的时候NULL在最后一个。

### 17. 使用别名进行排序

- **注意：使用别名排序时，别名不加双引号。**

```
SELECT salary *12*(1+IFNULL(salaryadd)) as "年薪" FROM users ORDER BY 年薪 DESC;
```

### 18. 多列排序

**先将薪水进行降序排序，再将薪水相同的名字按照升序排序。**

**注意：先写哪个属性就先对哪个属性进行排序，按顺序执行。**

```mysql
SELECT salary,name FROM users ORDER BY salary DESC,name ASC;
```

### 19. 在MySQL中还可以进行计算

![image-20211005173023041](https://gitee.com/YunboCheng/imageBad/raw/master/image/image-20211005173023041.png)

### 20. Union 结果集相

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

### 22.group by 分组函数(聚合函数) 与  having 分组后继续筛选。

#### 22.1 分组函数（聚合函数）

- sum() 求和
- avg() 平均值
- max() 最大值
- min()  最小值
- count() 计数

**在分组函数中给数值类型，如果给字符类型，产生的结果都是0.**

**分组函数在使用的时候自动忽略NULL。不用对NULL使用IFNULL处理。**

**sum，avg 一般用于处理数值型，max min count 可以处理任何类型**

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

#### 22.1 count()函数的详细介绍

```mysql
SELECT COUNT(salary) FROM emp；  #此时统计的是salary这一列不为null的行数。
SELECT COUNT(*) FROM emp;  # 统计这一组数据的行数(每列都为NULL的数据不会存储到数据库)
SELECT COUNT(1) FROM emp; 
# 以上这条sql语句的含义和第二种的意思一样，相当于在每行数据的前边加上一个1，然后统计1的个数。
# 括号里边可以是任意类型的值，COUNT('天气')、COUNT('2')
```

**效率问题**

- MYISAM存储引擎下，COUNT(*)的效率要高。
- INNODB存储引擎下，COUNT(*)和COUNT(1)的效率差不多，比COUNT(字段)要高些。

#### 22.2 MAX() 与 MIN() 函数详解

- **使用这两个函数作用与varchar等数据类型的字段，会自动将其转换为长度，相当于MAX(LENGTH(字段));  汉字占两个或者三个长度。**

```mysql
SELECT MAX(name) FROM emp;  # 此时返回的是姓名中最长的那个
SELECT MIN(name) FROM emp;  # 此时返回的是姓名中最短的那个
```

#### 22.3 分组函数(聚合函数)与去重(distinct)联合使用

- 实现去重的统计。

```mysql
SELECT SUM(DISTINCT salary) FROM emp;
```

- **去除重复的工资，然后在将所有的相加。**

#### 22.4 分组查询（group by）

- **查询列表比较特殊，要求是分组函数和group by 后出现的字段。**

例题：查询每个部门的最高薪资（简单的分组查询，不添加任何的分组条件，整个表就是一组。）

```mysql
SELECT MAX(salary),dept FROM emp GROUP BY dept;
```

例题：查询邮箱中包含a字符的，每个部门的平均工资。(添加简单的过滤条件)

```mysql
SELECT AVG(salary),dept FROM emp WHERE email like '%a%' GROUP BY dept;
```

例题：查询哪个部门的员工个数大于2（使用到了having但是没有使用到where）

```mysql
SELECT COUNT(*),dept FROM emp CROUP BY HAVing COUNT(*) > 2;
```

例题：查询每个部门有奖金的员工的最高薪资大于12000部门和最高薪资。

```mysql
SELECT MAX(salary),dept FROM emp WHERE aad_salary IS NOT NULL GROUP BY dept HAVING MAX(salary) > 12000;
```

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20211008093503.png)

- **多个字段分组，并且联合排序使用**

例题：查询每个部门每个工种的员工的平均薪资 。

```mysql
SELECT AVG(salalary),dept,type FROM emp GROUP BY dept,type ORDER BY AVG(sala) DESC;  #部门的顺序可以改变。
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

**注意：这个代表的是长度，不是所代表的字节数，一个汉字和英文都算一个长度。**

**clob类型**

- 字符大对象，最多可以存储4G的字符串。比如：存储一篇文章，自我介绍等。**超过255个字符的采用CLOB字符大对象来存储**

**blob类型**

- 二进制大对象，专门用来存储图片、声音、视频等流媒体数据。往blob类型的字段上插入数据的时候，列入插入一张图片、视频等，你需要使用IO流才行。

### 29.IFNULL的用法

- ifnull是针对处理null的一个关键字，使用格式

```mysql
SELECT salary FROM emp WHERE IFNULL(salary,0) + 100; 
#此时IFNULL代表的含义是当薪资为NULL的时候，会把这个salary当作0处理。如果不写IFNULL，则输出结果一定是NULL。

SELECT salary FROM emp WHERE IFNULL(salary,10) + 100; 
#此时IFNULL代表的含义是当薪资为NULL的时候，会把这个salary当作10处理。
```

### 30.删除表

- 使用 **if exists**关键字即使没有这张表也不会报错，比普通的删除表语言要健壮。

```mysql
DROP table IF EXISTS users;
```

### 31.插入日期

**mysql提供的日期格式**

- %Y 年
- %m 或者 %c 月 
- %d 日
- %h 时
- %i 分
- %s 秒

**str_to_date('日期字符串','日期转换格式')函数**：将varchar类型转换为date类型。 

```mysql
# 调用函数转换，可以自定义输入格式
INSERT INTO users(id,name,brith) values(1,'张三',str_to_date('01-10-1999','%d-%m-%Y'));
```

**注意：这个函数主要用于插入数据。我们插入数据时输入的只能是varchar类型，需要使用str_to_date函数进行转换**

**mysql给我们提供了一种自动转换机制，当输入的字符串格式是 %Y-%m-%d 的时候，这个时候不需要我们在调用转换函数，mysql会自动进行转换**

```mysql
# mysql自动转换，不可以自定义输入格式
INSERT INTO users(id,name,brith) values(1,'张三','1999-10-01);
```



**date_format(日期类型数据,'日期格式')函数**：将日期类型转换成特定格式的字符串。

```mysql
# 调用函数转换，可以自定义输出格式
SELECT id,name,data_format(birth,'%m/%d/%Y') as birth from users;
```

 **注意：这个函数主要用于查询语句，设置展示的日期的格式。这个时候也发生了一个日期到varchar的转换。**

如果我们直接打印日期类型，这个时候mysql会发生自定转换，将date转换成varchar类型。

```mysql
# mysql自动转换，不可以自定义输出格式
SELECT id,name,birth as birth from users;
```

- **Java中的日期格式：yyyy-MM-dd HH:mm:ss SSS**

### 32.date和datetime的区别

- date为短日期：只包含年月日信息。
- datetime为长日期：只包含年月日时分秒信息。

- 短日期默认格式：%Y-%m-%d 
- 长日期默认格式：%Y-%m-%d %h:%i:%s 

### 33.获取当前时间（now()函数）

- now()函数获取的是当前系统的时间，包括时、分、秒。是datetime类型的。

### 34.关于修改和删除数据

- 修改数据

```mysql
UPDATE users SET WHERE id = 1;
```

- 删除数据

```mysql
DELETE FROM users WHERE id = 1;
```

**注意：如果不添加条件，会将表中的所有数据修改或者删除。**

### 35.一次插入多条记录

- 语法格式：

```mysql
INSERT INTO users(字段值1，字段值2) values(),(),();
```

### 36.快速创建表

- 快速创建表其实就是复制一张其他的表。(就是将查询到的一张表的数据作为另一张表的数据)

```mysql
CREATE TABLE users2 as SELECT * FROM users;  #这个是将整个表的数据进行复制
```

- 快速创建表（取出一张表的其中一部分数据创建一张新表）

```mysql
CREATE TABLE users2 as SELECT name,id FROM users where id = 1;
```

### 37.快速删除表

- 使用delete删除数据（不加where条件代表将整张表的数据删除）语法格式 **DML**

```mysql
DELETE FROM users;
```

**delete删除数据的原理：**

- 只是将表中的这个数据删除了，但是这个数据所占的空间还是存在的，不会被释放。这种删除数据的方式速度比较慢，删除效率低。但是这种删除方式支持回滚，后悔了可以在恢复数据。
- **delete可以使用where语句删除单条数据。**
- 使用truncate删除数据（是删除表中的数据，而不是删除表）**DDL**

```mysql
TRUNCATE table users;
```

**truncate删除数据的原理：**

- 将数据永久的删除，不可以进行回滚，释放数据存储的空间。效率高。
- **truncate是删除全部数据，不可以删除单条。**

**上亿条数据delete需要删除一个小时，truncate只需要1秒。**

### 38.<=> 符号

- **<=> 符号相当于is 或者是 = **

```mysql
SELECT salary FROM emp WHERE salary <=> null;  #此时获取的是薪水为null的数据
```

```mysql
SELECT salary FROM emp WHERE salary <=> not null； # <=> not null 语法是错误
```

- **<=> 相当于等号**

```mysql
SELECT salary FROM emp WHERE salary <=> 1200;
```

### 39.常用函数

#### 39.1 字符函数

1. **length(str)：获取参数值（字符串）的字节个数。**

```mysql
SELECT LENGTH('123hhh哈哈');  # gbk输出10 utf输出12
```

注意：汉字所占的长度和编码方式有关系，如果是**gbk编码格式汉字占两个长度，英文和数字占一个长度**，如果是**utf8编码格式汉字占三个长度，英文和数字占一个长度。**

注意：只有length()函数计算的才是字符所占的字符长度，区分汉字，而其他的函数计算的都是字符所占的长度，汉字、英文和数字都占一个字符长度。

```mysql
SELECT LENGTH(name) FROM users WHERE id = 1;
```

2. **查看数据库编码方式**

```mysql
show variables like 'character%';
show variables like 'char%';  # 两者效果相同
```

3. **upper(str)：小写字母转大写字母（全部转化为大写）**

```mysql
SELECT id,UPPER(name) FROM users;
```

4. **lower(str)：大写转小写**

```mysql
SELECT id,LOWER(name) FROM users;
```

5. **substr或者substring(str，截取下标)：截取指定字符后面的所有字符。**

```mysql
SELECT SUBSTR('今天的天气不错',4);  # 天气不错。包含第四位到最后的字符。
```

**注意：在mysql中截取字符串时下标是从1开始的，分页查询的时候下标是从0开始的。**

```mysql
SELECT SUBSTR(name,3) from users; 
```

6. **substr(str,begin,end)：截取指定范围的字符。**

```mysql
SELECT　SUBSTR('今天天气不错',3,5);  // 天气
```

7. **concat(字符串1，字符串2，字符串3)：拼接字符串**

```mysql
SELECT CONCAT(last_name,'_',first_name) as 姓名 FROM users;  # 云博_程
```

- **函数可以嵌套使用**

```mysql
SELECT CONCAT(UPPER(last_name),LOWER(first_name)) 姓名 FROM users;
```

- **综合案列：姓名中的首字符大写，其他字符小写然后拼接，显示出来。**

```mysql
select concat(upper(substring(name,1,1)),'_',lower(substr(name,2))) name  from emp1;
```

**instr(str,str2)：返回子字符串第一次出现的索引，如果找不到返回0**

```mysql
SELECT INSTR('今天的天气很是不错，天气晴朗','天气') as out_put; # 3
```

- 注意：双引号中的逗号并不影响查询的结果

8. **trim(str)：去除字符串前后的空格，但是不会去除字符串之间的空格。**

```mysql
SELECT LENGTF(TRIM('  天气    '));  #6 因为汉字在utf8中占三个字节长度，gbk中占2个。
SELECT TRIM('  天气   ');  #天气。
```

9. **去除前后指定的字符**

```mysql
SELECT TRIM('a' FROM 'aaaaa天aaaa气aaaaa');  # 天aaaa气
```

10. **lpad(str,结果长度,填充字符)：用指定的填充字符左填充到结果长度。**

```mysql
SELECT　LPAD('天气不错',10,'*');  # ******天气不错
SELECT　LPAD('天气不错',2,'*');   # 天气 
```

11. **rpad(str,结果长度,填充字符)：用指定的填充字符右填充到结果长度。**

```mysql
SELECT　RPAD('天气不错',10,'*');  # 天气不错******
SELECT　RPAD('天气不错',2,'*');   # 天气
```

- 注意：当结果长度比字符串短的时候，从原有字符串的左侧开始保留，截取掉右侧的字符。

12. **replace(str,被替换字符,替换字符)：替换字符串中所有的字符。**

```mysql
SELECT REPLACE('今天的天气不错，天气晴朗','天气','乌云') // 今天的乌云不错，乌云晴朗
```

#### 39.2 数学函数

1. **round(数字)：四舍五入，如果是负数，先取其绝对值，然后再将符号补回来即可。**

```mysql
SELECT ROUND(1.45);  # 1
SELECT ROUND(1.55);  # 2
SELECT ROUND(-1.45);  # -1
SELECT ROUND(-1.55);  # -2
```

2. **round(数字,保留小数位数)：四舍五入，如果是负数，先取其绝对值，然后再将符号补回来即可。**

```mysql
SELECT ROUND(1.457,2);   # 1.46
SELECT ROUND(1.454,2);   # 1.45
SELECT ROUND(-1.457,2);  # -1.46
SELECT ROUND(-1.454,2);  # 1.45
```

3. **ceil(数字)：向上取整，返回>=该参数的最小整数**

```mysql
SELECT CEIL(1.02);  # 2
SELECT CEIL(1.00);  # 1
SELECT CEIL(-1.02);  # -1
```

4. **floor(数字)：向下取整，返回<=该参数的最大整数**

```mysql
SELECT FLOOR(1.02);  # 1
SELECT FLOOR(1.00);  # 1
SELECT FLOOR(-1.02);  # -2
```

5. **truncate(小数，小数点后保留几位)：截断小数点后边的位数。**

```mysql
SELECT TRUNCATE(1.65,1);  # 1.6
SElECT TRUNCATE(1.677,2); # 1.67
```

6. **MOD(数字，数字)：除整求余。**

```mysql
SELECT MOD(10,3);  #  1 相当于 SELECT 10%3;
SELECT MOD(-10,3); #  -1
SELECT MOD(10,-3); #  1
SELECT MOD(-10,-3); # -1
```

7. **rand()：获取[0,1)之间的随机数，左闭右开，和Java中的Random一样。**

#### 39.3 日期函数

1. **now()：返回当前系统时间**

```mysql
SELECT NOW();  # 2021-10-07 20:16:09 返回的是datetime类型
```

2. **curtdate()：返回当前系统时间，不包含时间**

```mysql
SELECT CURDATE();  # 2021-10-07
```

3. **curtime()：返回当前时间，不包含日期**

```
SELECT CURTIME();  # 20:16:09
```

4. **获取指定的部分，年(YEAR)、月(MOUTH)、日(DAY)、时(HOUR)、分(MINUTE)、秒（SECOND）**

```mysql
SELECT YEAR(now());
```

5. **datediff(最大时间，最小时间)：计算两个时间之间相差的天数。传递的参数是一个date类型**

```mysql
SELECT DATEDIFF('2020-1-1','1999-1-1'); #这个函数是用于计算日期之间的差值。
```

6. **monthname()：以英文的形式返回月份(英文字母)**

```mysql
SELECT MONTHNAME('2021-10-19'); # October
```

#### 39.4 其他函数

- **select version() : 查看当前数据库版本。**

```mysql
SELECT version();
```

- **select database()：查看当前使用的数据库。**

```mysql
SELECT database();
```

- **select user() ：查当前数据库使用者。**

```mysql
SELECT user();
```

- **password(字符)：返回指定字符的加密形式**

```mysql
SELECT password('程云博'); # *D87E50764614A3D8CDAE81EF88A1D065AE9A5230
```

- **md5(字符)：返回MD5加密形式数据**

```mysql
SELECT MD5('程云博');  # 224a7113e9e509a57b738e977fe3b723
```

### 40.流程控制函数

#### 40.1 if函数

- if函数可以实现if...else的效果。

```mysql
SELECT IF(10>5,'正确','错误');
```

```mysql
SELECT name,IF(salary is null,'呜呜','哈哈') as '备注' FROM emp;
```

#### 40.2 case函数

- case类似于 switch case 的效果。

- **case的语法格式**

```mysql
case 要判断的字段或者表达式
when 常量1 then 要显示的值1或语句1  # 如果是语句的话要加分号，是值的话不加分号
when 常量2 then 要显示的值2或语句2  
...
else 要显示的值n或者语句n
end
```

1. **case函数的第一种写法（值写法）：**

```mysql
SELECT salary 原始工资,department_id,
CASE department_id 
WHEN 30 THEN salary*1.1
WHEN 40 THEN salary*1.2
ELSE salary 
END AS 新工资 
FROM emp;
```

2. **case函数的第二种写法（语句写法）：**

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/5.png)

- **两种写法的区别**

![image-20211008163744502](https://gitee.com/YunboCheng/imageBad/raw/master/image/image-20211008163744502.png)

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20211008163811.png)

### 41.连接查询(多表查询) 92语法

#### 41.1 连接查询分类

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20211008110734.png)

- 在92语法中，将**连接条件和筛选条件**都放到了 **where中**，不利于阅读。

#### 41.2  等值查询（92语法）

- **语法格式**

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20211008165155.png)

#### 41.2.1 查询时给表起别名（92语法）

```mysql
SELECT s.salary,d.dept FROM emp as s,jobs as d WHERE s.job_id = d.job_id;
```

**注意：**

- **给表明起玩别名之后，不可以在使用以前表的名字，只能使用别名。**

- 两张表的顺序可以调换。

案例：查询有奖金的员工名、部门名（使用where进行筛选）

```mysql
SELECT e.name,j.dept FROM emp e,jobs j WHERE e.id = j.id AND e.add_salary IS NOT NULL;
```

#### 41.2.2 查询时与分组函数联合使用（92语法）

![image-20211008114227825](https://gitee.com/YunboCheng/imageBad/raw/master/image/image-20211008114227825.png)

#### 41.2.3 多表连接（92语法）

案例：查询员工名、部门名和所在的城市

![image-20211008114700443](https://gitee.com/YunboCheng/imageBad/raw/master/image/image-20211008114700443.png)

#### 41.3 非等值查询 （92语法）

- **语法格式**

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20211008165407.png)

- 查询工资的等级并且只显示等级为 A的薪资。

```mysql
SELECT e.salary,g.grade FROM emp e,jobs g WHERE salary BETWEEN g.lower_sal AND g.hight_sal AND g.grade = 'A'; 
```

#### 41.4 自连接查询（92语法）

- **语法格式**

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20211008165459.png)

- **自连接的意义在于：把同一张表看作是两张表。**

例题：查询员工名、id值以及上级领导名称、id值。（这两个数据处于同一张表中）

查询的精髓：员工上级领导的id等于上级领导的员工id

```mysql
SELECT e.emp_id,e.last_name,m.emp_id,m.last FROM emp e, emp m WHERE e.manage_id = m.emp_id;  
```

### 

### 42.连接查询(多表查询) 99语法

- 语法格式以及类型

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20211008170912.png)

**使用的时候只需要将类型所对应的关键字替换即可，其结构并不需要变化。**

#### 42.1 内连接

- **语法格式**

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20211008171115.png)

##### 42.1.1 等值连接

案列：查询员工名中包含a的姓名、部门名

```mysql
SELECT e.last_name,j.job_title FROM emp e INNER JOIN jobs j ON e.jod_id=j.job_id WHERE e.last_name LIKE '%a%';
```

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20211008171918.png)

- 等值连接之多表连接

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20211008172355.png)

##### 42.1.2 非等值连接

案例：查询工资级别>20的个数，并且按工资级别降序排序。

```

```

