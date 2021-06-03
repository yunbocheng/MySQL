# MySQl 笔记()

## sql、DB、DBMS 分别是什么，他们之间的关系？
-   DB:DateBase（数据库，数据库实际上在硬盘以文件的形式存在）
-   DBMS：DateBase Management System(数据库管理系统，常见有：MySQl、Oracle、DB2、Sybase、sqlServer...)
-   SQL：结构化查询语言，是一门标准通用的语言。标准的sql适合于所有的数据库产品。
    SQl属于高语言。只要能看懂英语单词的，写出来的sql语句，可以读懂什么意思。
    SQl语句在执行的时候，实际上内部也会先进行编译，然后在执行sql。（sql语句的编译由DBMS完成）
-   DBMS负责执行sql语句，通过执行sql语句来操作DB当中的数据。
-   DBMS-（执行）-> SQl -（操作）-> DB

## MySQL 概述
- MySQL最初是由”MySQL AB”公司开发的一套关系型数据库管理系统
- 在2008年初，Sun Microsoft收购了MySQL AB公司，在2009年，Oracle收购了Sun公司，使MySQL并入Oracle的数据库产品线

## 什么是表 ?
表：table是数据库的基本组成单元，所有的数据都以表格的形式组织，目的是可读性强。

一个表包含行和列：
- 行：被称为数据/记录（date）
- 被称为字段（column）

每一个字段应该包含哪些属性 ？
- 字段名（学号、姓名、年龄）
- 数据类型（int 、varchar 、int）
- 相关的约束（比如姓名一定要填写）

## 学习MySQL主要是学习通用的SQL语句
      DQL（数据查询语言）：查询语句，凡是select语句都是DQL。
      DML（数据操作语言）：insert delete update ,对表当中的数据进行增删改。
      DDL（数据定义语言）：create drop alter ，对表结构进行增删改。
      TCL（事务控制语言）：commit提交事务，rollback回滚事务。（TCL中的T是 Transaction）
      DCL（数据控制语言）：grant授权、revoke撤销权限等。
## 导入数据
- 第一步：登录mysql数据库管理系统

      doc命令窗口：
       mysql -uroot -p (密码)


- 第二步：查看有哪些数据库

      show databases;  #（这个不是SQL语句，是MySQL的命令）
       #注意：这个是MYSQL命令，在Oracle中不一定能用

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210506161106.png)

- 第三步：创建属于自己的数据库

      create database bjpowernode; （这个不是SQL语句，是MySQL的命令）


- 第四步：使用bjpowernode数据

      use bjpowernode;(这个不是SQL语句，是MySQL的命令)


- 第五步：查看当前使用的数据库中有哪些表

      show tables; (这个不是SQL语句，是MySQL的命令)

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210506161142.png)

(部门表、员工表、工资等级表)
- 第六步：初始化数据

      source C:\Users\YunboCheng\Desktop\bjpowernode.sql


> 注意：
1. bjpowernode.sql，这个文件以 sql结尾，这样的文件被称为”sql“脚本。什么是sql脚本？
2. 当一个文件的扩展名是 .sql，并且该文件中编写了大量的sql语句，我们称这样的文件为sql脚本。

- 第七步：删除数据库

      drop database bjpowernode;
- 第八步 查看表结构

      desc dept；

  ![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210506163116.png)

（部门编号） （部门名称）（部门位置）

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210506213507.png)

（员工编号） （员工姓名）（工作岗位）（上级领导编号）（入职时间）（月薪）（补助/津贴）（部门编号）

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210506213541.png)

（工资等级）（最低薪资）（最高薪资）

- 第九步：查看表中的数据

      select * from emp;
  
    - 员工表中的所有数据

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210506214419.png)

- 部门表中的所有数据

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210506214618.png)

- 工资等级表中的所有数据

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210506214703.png)

## mysql中常用的命令
1. 查询当前使用的数据库
   
   > select database();
2. 查询数据库版本也可以使用
   
   > select version();
3. 终止一条语句
   
   > 如果想要终止一条正在编写的语句，可键入 \c 不用加分号；
4. 退出 mysql
   
   > exit
5. 查看和指定现有的数据库
   
   > show databases;
6. 指定当前缺省数据库
   
   > use bjpowernode;
7. 查看当前使用的库
   
   > select database();
8. 查看当前库中的表
   
   > show tables;
9. 查看其他库中的表
   
   > show tables from test;(查看test中的表)
10. 查看表的结构
    
    > desc <teble name>
11. 查看创建表的语句
    
    > show create table emp;
>
![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210506222417.png)

## SQL语句
### 1.简单查询语句
1.1 简单的查询语句（DQL）
   > 语法格式:
   select 字段名1,字段名2,字段名3,...from 表名;

1.2 提示：
- 任何一条sql语句以“;”结尾；

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210506225349.png)
- sql语句不区分大小写；

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210506225825.png)

1.3 查询员工的年龄?(字段可以参与数学运算)
   > select ename,sal * 12 from emp;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531165204.png)

1.4 给查询结果的列重命名
   > select ename,sal * 12 as yearsal from emp; // 取的为英文名字

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531170258.png)
   > select ename,sal * 12 as '年薪' from emp; // 取的为中中文名字

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531170150.png)

注意：Mysql 中字符串可以使用 单引号 或者 双引号 括起来
     而在 oracle 中字符串只能使用 单引号 括起来
     建议以后都使用单引号括起来
重点：语句中的 as 可以省略不写
   > select ename,sal * 12 '年薪' from emp; 

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531170554.png)

1.5总结 ：

1.5.1 查询一个字段
   > select ename from emp;

1.5.2 查询多个字段
   > select ename.sal from emp;

1.5.3 查询全部字段
   > select * from emp; (不建议使用，*代表全部字段，要将*装换为全部字段，效率低)

### 2.条件查询语句

2.1 语法格式
  > select
>     字段1，字段2...
>   from
>     表名
>   where 
>     条件;

执行顺序：先from ，然后where，最后select

2.2 查询工资等于 5000 的员工姓名？
   > select ename from emp where sal = 5000;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531172036.png) 

2.3 查询 SMITH 的工资
   > select sal from emp where ename = 'SMITH'; // 字符串用单引号括起来

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531172358.png)

2.4 找出工资高于 3000 的员工
   > select ename,sal from emp where sal > 3000;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531172824.png)

> select ename,sal from emp where sal >= 3000;

> select ename,sal from emp where sal < 3000;

> select ename,sal from emp where sal <= 3000;

2.5 找出工资不等于3000的
   > select ename,sal from emp where sal <> 3000;

   > select ename,sal from emp where sal != 3000;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531173254.png)

注意：不等于可以是 <> 或者 != ，两个都可以的

2.6 找出工资在1100和3000之间的员工，包括1100和3000；
   > select ename,sal from emp where sal >=1100 and sal <= 3000; // 使用的是 and

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531173742.png)

2,7 使用的是 between...and...是闭区间[a,b] [1100,3000];
   > select ename,sal from emp where sal between 1100 and 3000;

注意：between...and...在使用的时候必须左小右大

2.8 between...adn...除了可以使用在数字方面，还可以使用在字符串方面
     
字符串使用 between...and... 判断的是字符串的第一个字符，所得的结果是 左闭右开区间 [a,b);,

   > select ename from emp where ename between 'A' and 'B';

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531175029.png)

2.9 找出哪些人津贴为NULL;
注意: 在数据库当中NULL不是一个值，代表什么都没有，为空。
     空不是一个值，不能用等号衡量。
     必须使用 is null 或者 is not null
     0.0 也属于 NUll ,他代表 0 数值。
     
select ename,comm from emp where comm = null; 错误写法，不能进行赋值。

   > select ename,comm from emp where comm is null;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531175628.png)

2.10 找出哪些人津贴不为 NULL
   > select ename,sal,comm from emp where comm is not null;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531180643.png)

2.11 找出那些人没有津贴
   > select ename,sal,comm from emp where comm is null or comm = 0;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531180956.png)

2.12 找出工作岗位是 MANAGER 和 SALESMAN 的员工
   > select ename,job from emp where job = 'MANAGER' or job = 'SALESMAN';

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531182005.png)

2.13 and 和 or 联合起来用：找出薪资大于1000并且部门是20或者30部门的员工
  > select ename,sal,deptno from emp where sal > 1000 and (deptno = 20 or deptno = 30);

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531183104.png)

注意: 当运算符的优先级不确定的时候，可以加括号调整计算顺序。

2.14 in 等同于 or :找出工作岗位是 MANAGER 和 SALESMAN 的员工 
   > select ename,job from emp where job = 'MANAGER' or 'SALESMAN';
   > select ename,job from emp where job in('MANAGER','SALESMAN');

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531183650.png)

注意：in后面的值不是区间，是具体的值。
   > select ename,job from emp where sal in(800,5000);

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531184451.png)

2.15 not in 不在这几个值当中
  > select ename,job,sal from emp where sal not in(800,5000);

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531184955.png)

2.15 模糊查询 like 

在模糊查询中，必须掌握两个特殊的符号，一个是%，一个是_

%代表任意多个字符，_代表任意一个字符

2.15.1找出名字中含有o的？
   > select ename from emp where ename like "%o%";

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531203650.png)

2.15.2 找出名字中第二个字母是A的？
   > select ename from emp where ename like '_A%';

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531204101.png)

2.15.3 取出名字里有下划线的名字
  > select ename from emp where ename like '%\_%';

注意: 此时 \_ 代表一个普通的 下划线 _

2.15.4 找出名字最后一个字母是T的
   > select ename from emp where ename like '%T';

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531204859.png)

2.16 排序 （升序，降序）
语法格式：
      select 
         字段值1，字段值2...
      from 
         表明
      order by
         字段值;
2.17 按照工资升序，找出员工名和薪资
   > select ename,sal from emp order by sal; (这个为默认，默认升序)

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531210041.png)

注意：默认是升序。怎么指定升序或者降序？asc表示升序，desc表示降序。
   > select ename,sal from emp order by sal; (默认升序)
> 
   > select ename,sal from emp order by sal asc;
> 
   > select ename,sal from emp order by sal desc;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531210537.png)

2.18 按照工资的降序排列，当工资相同的时候在按照名字的升序排列。
  > select ename,sal from emp order by sal desc,ename asc;

注意: 越靠前的字段越能起主导作用。只有当前面的字段无法完成排序的时候，才会启用后面的字段

练手:
   > select ename,sal from emp order by 1;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531212631.png)

   > select ename,sal from emp order by 2;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531212716.png)

  > select * from emp order by 6;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531212816.png)

2.19 找出工作岗位是 SALESMAN 员工，并且要求按照薪资的降序排序
     
     select
         ename,job,sal
     from
        emp
     where
        job = 'SALESMAN'
     order by 
        sal desc;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531214327.png)

执行顺序 ： 先执行from,在执行where，在执行select,最后在执行order by 。
select 
      *    3
from
tablename  1
where          
条件        2
order by    
...        4

order by 是最后执行的。

2，20 分组函数/聚合函数/多行处理函数

- count 计数
- sum 求和
- avg 平均数
- max 最大值
- min 最小值

记住: 所有的分组函数都是对“某一组”数据进行操作的。

2.20.1 找出工资的总和？
   > select sum(sal) from emp;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210601151526.png)

2.20.2 找出最高工资
   > select max(sal) from emp;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210601151618.png)

2.20.3 找出最低工资
   > select min(sal) from emp;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210601151654.png)

2.20.4 找出平均工资
   > select avg(sal) from emp;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210601151810.png)

2.20.5 找出总人数
   > select count(*) from emp;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210601152040.png)

   > select count(ename) from emp;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210601152205.png)

分组函数一共有5个。分组函数还有另一个名字：多行处理函数。
多行处理函数的特点：输入多行，最终输出的结果是 1 行。

2.20.6 分组函数自动忽略NULL。
   > select count(comm) from emp;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210601193734.png)

  > select sun(comm) from emp;

// 自动忽略 NULL
![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210601201130.png)

多此一举：不需要添加这个额外的过滤条件，分组函数自动忽略null
  > select sum(comm) from emp where comm is not null;

2.20.7 找出工资高于平均工资的员工

   第一步 : 找出平均工资 
   > select avg(sal) from emp;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210601202233.png)

   第二步 : 找出工资高于平均工资的员工
   > select ename,sal from emp where sal > (select avg(sal) from emp);

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210602175416.png)


// 以下的错误信息：无效的使用了分组函数。
![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210602154549.png)

// 以上的的错误原因：SQL语句当中有一个语法规则，分组函数不可以直接使用在where子句当中。 

// 因为group by 是在 where 执行之后才会执行的。

     select  5
     ...
     from    1
     ... 
     where   2
     ...
     group by  3
     ...
     having   4  
     ...
     order by  6
     ...

2.20.8 count(*) 和 count(具体某个字段) , 他们有什么区别？
     
- count(*) : 不是统计某个字段中数据的个数，而是统计总记录条数。（和某个字段无关）
- count(comm) : 表示统计comm字段中不为NULL的数据总数量。

   > select count(*) from emp;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210602160110.png)

  > select count(comm) from emp;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210602160301.png)

  > select count(job) from emp;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210602160352.png)

2.20.9 分组函数也可以组合起来用
   > select count(*),sum(sal),avg(sal),max(sal),min(sal) from emp;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210602161444.png)
-

2.21 单行处理机
  什么是单行处理机？
  - 输入一行，输出一行。

2.21.1 计算每个员工的年薪
   > select ename,(sal+comm) * 12 as yearsal from emp; // 错误写法

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210601194123.png)

  使用ifnull函数处理：
  > select ename,(sal + ifnull(comm,0)) * 12 as yearsal from emp; // 正确写法

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210601195530.png)

重点: 所有数据库都是这样规定的，只要有NULL参与的运算结果一定是NULL。

2.21.2 ifnull() 空处理函数？
语法格式：
  > ifnull(可能为NULL的数据，被当做什么处理) : 属于单行处理函数。

2.21.3 将津贴中的 NULL 转换为 0
  > select ename,ifnull(comm,0) as comm from emp;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210601194931.png)

2.21 分组查询 group by 和 having

- group by : 按照某个字段或者某些字段进行分组。
- having : 是对分组之后的字段再次过滤。

2.21.1 找出每个岗位的最高薪资
   > select max(sal) from emp group by job;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210602153733.png)

注意: 
- 分组函数一般都会和group by 联合使用。这也是为什么被称为分组函数的原因。
- 并且任何一个分组函数（count,sum,max,min,avg）都是在group by语句执行结束之后才会执行的。
- 当一条 sql 语句没有group by的话，整张表的数据会自成一组。

2.21.2 多字段分组查询
  > select ename,max(sal),job from emp group by job;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210602175737.png)

// 以上在 mysql当中，查询结果是有的，但是结果没有意义，在Oracle数据库当中会报错，语法错误。

重点: 记住一个规则，当一条语句中有 group by 的话，select后面只能跟分组函数和参与分组的字段。

2.22.3 每个工作岗位的平均工资
   > select obj,avg(sal) from emp group by job;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210602180407.png)

2.22.4 多个字段联合起来一块分组，找出每个部门不同工作岗位的最高薪资。
   > select deptno,job,max(sal) from emp group by deptno,job;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210602180708.png)

2.22.5 找出每个部门的最高薪资，要求显示薪资大于2900的数据

  第一步: 找出每个部门的最高薪资
  > select deptno,max(sal) from emp group by deptno;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210602181225.png)

  第二步: 找出薪资大于2900 这种方式效率低
> select deptno,max(sal) from emp group by deptno having max(sal) > 2900;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210602181454.png)

  完美方案：效率较高，要求显示薪资大于2900的数据。
  > select deptno,max(sal) from emp where sal > 2900 group by deptno;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210602181655.png)

2.22.6 找出每个部门的平均薪资

   第一步 : 找出每个部门的平均薪资
  > select deptno,avg(sal) from emp group by deptno;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210602182110.png)

   第二步 : 要求显示薪资大于2000的数据 
  > select deptno,avg(sal) from emp group by deptno having avg(sal) > 2000;   

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210602182325.png)

 // 错误，where后边不能使用分组函数，这种情况只能使用 having 过滤

 > select deptno,avg(sal) from emp where avg(sal) > 2000 group by deptno; // 错误

2.23 总结一个完整的 DQL 语句怎么写

      select
      ...
      from
      ...
      where
      ...
      group by
      ...
      having
      ...
      order by
      ... 

### 3.连接查询

3.1.1 关于查询结果的去重 (关键字 distinct ,去除重复记录)
  > select distinct job from emp;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210602183210.png)

3.1.2 以下语句是错误的
  > select ename,distinct job from emp;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210602183435.png)

重点: distinct只能出现在所有字段的最前面。

3.1.3多个字段联合去重
  > select distinct deptno,job from emp;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210602183742.png)

3.1.4 统计岗位数量
  > select count(distinct job) from emp;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210602183849.png)

3，2 链接查询的概念 

- 在实际的开发中，大部分的情况下都不是从单表中查询数据，一般都是多张表联合查询取出最终的结果。
- 在实际的开发中，一般一个业务都会对应多张表，比如 ：学生和班级，起码两张表。

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210603131936.png)

如果学生和班级信息存储到一张表中，结果就像上面一样，数据会存在大量的重复，导致数据的沉余。。

3.3 连接查询的分类

1. 根据语法出现的年代划分的话，包括：
  - SQL92 (一些老的DBA可能还在使用这种语法。DBA : DataBase Administrator,数据库管理员)
  - SQL99 (比较新的语法)

2. 根据表的连接方式来划分，包括:
- 内连接 ：
  1. 等值连接
  2. 非等值连接
  3. 自连接
- 外连接 ： 
  1. 左外连接 (左连接)
  2. 右外连接 (右连接)
- 全连接 (这个不经常使用！！)

3.4 连接查询有一种现象: 笛卡尔积现象。

3.4.1 案例 ；找出每一个员工的部门名称，要求显示员工名和部门名。
  > select ename.deptno from emp;

EMP 表：
![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210603133405.png)

 > select deptno,dname from dept;

DEPT 表 :
![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210603134027.png)

// ename 和 dname要联合在一块显示，粘到一块。
 > select ename,dname from emp,dept;


![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210603134210.png)

// 其中一共有 14 * 4 行数据，一个名字对应四个部门名称

原理 : 两张表通过 deptno 进行查询连接

笛卡尔积现象 : 当两张表进行连接查询的时候，没有任何条件的限制，最终的查询结果条数是两张表记录条数的乘积。

3.4.2 关于表的别名 ： 
  > select e.ename,d.dname from emp e,dept d; (此处省略了 as )

3.4.3 表的别名有什么好处: 

- 执行效率高
- 可读性好

3.4.4 
- 怎么避免笛卡尔积现象？当然是加入条件进行过滤
- 避免了笛卡尔积现象，会减少记录的匹配次数嘛？
  1.不会，次数还是 56 次，只不过显示的都是有效记录。

3.4.5 找出每一个员工的部门名称，要求显示员工名和部门名。
     
     这个是SQL92，以后不用
     select 
     e.ename,dname
     from
     emp e,dept d
     where
     e.deptno = d.deptno

3.5 内连接之等值连接

3.5.1 最大的特点是 : 条件是等量关系。

3.5.2 查询每个员工的部门名称，要求显示员工名和部门名

SQL92: (太老，不用了)

    select 
       e.ename,d.dname
    from
       emp e,dept d
    where 
       e.deptno = d.deptno;

SQL99: (常用的)

这个是省略inner的写法.inner可以省略，带着inner的目的是可读性好一些。

    select 
      e.ename,d.dname
    from 
      emp e
    join 
      dept d
    on 
      e.deptno = d.deptno;
这是不省略inner的写法，

      select 
      e.ename,d.dname
    from 
      emp e
    inner join 
      dept d
    on 
      e.deptno = d.deptno;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210603143614.png)

语法格式 ：

    ...
      A
    join 
      B
    on 
      连接条件
    where 
       ...

SQL99语法结构更清晰一些 ： 表的连接条件和后来的where条件分离。

3.6 内连接之非等值连接

3.6.1 最大的特点是 : 连接条件中的关系是非等量关系。

3.6.2 案例：找出每个员工的工资等级，要求显示员工名、工资、工资等级。
    
    // 省略了 inner
    select 
       e.ename,e.sal,s.grade
    from 
       emp e
    join 
      salgrade s
    on 
      e.sal between s.losal and s.hisal;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210603150717.png)

3.6  内连接之自连接

3.6.1 最大的特点 : 一张表看做两张表。自己连接自己。

3.6.2 找出每个员工的上级领导，要求显示员工和对应的领导名
  > select empno,ename,mgr from emp;

EMP a表 : 员工表
![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210603152815.png)

EMP b表 : 领导表

| empno | ename |
| ----- | ----- |
| 7566  | JONES |
| 7698  | BLAKE |
| 7782  | CLARK |
| 7788  | SCOTT |
| 7839  | KING  |
| 7902  | FORD  |

员工的领导编号 = 领导的员工编号

    select 
       a.ename as '员工名',b.ename as '领导名'
    from
       emp a
    inner join 
       emp b
    on 
       a.mgr = b.empno;

// 注意： 这个有13条数据，因为 KING 没有上级领导
![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210603162615.png)

3.7 外连接

3.7.1 什么是外连接，和内连接的区别

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210603153936.png)

3.7.2 找出每个员工的上级领导（所有的员工都要查询出来，KING也要查询出来）

EMP a表 : 员工表
![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210603152815.png)

EMP b表 : 领导表

| empno | ename |
| ----- | ----- |
| 7566  | JONES |
| 7698  | BLAKE |
| 7782  | CLARK |
| 7788  | SCOTT |
| 7839  | KING  |
| 7902  | FORD  |

内连接:

    select 
      a.ename '员工',b.ename '领导'
    from
      emp a
    join 
      emp b
    on 
      a.mgr = b.empno;

外连接 :
(左外连接/左连接)

    select 
      a.ename '员工',b.ename '领导'
    from 
      emp a
    left outer join
      emp b
    on 
      a.mgr = b.empno;
    其中 outer 可以省略
(右外连接/右连接)
 
    select 
      a.ename '员工',b.ename '领导'
    from 
      emp b
    right outer join
      emp a
    on 
      a.mgr = b.empno;
    其中 outer 可以省略
重点 : left 和 right 区分的是以左表还是以右表为主表。

注意 : 这个有14条数据，其中 KING 没有上级 ，会自动匹配NULL
![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210603162542.png)

外连接最重要的特点是 ： 主要的数据无条件的全部查询出来。

3.7.3 案例 : 找出哪个部门没有员工

    select 
       d.*
    from 
       emp e
    right join 
       dept d
    on 
       e.deptno = d.deptno
    where 
       e.sal is null;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210603171505.png)
 

3.8 三张表连接查询

3.8.1 案例：找出每一个员工的部门名称以及工资等级
    
    select 
      e.ename,d.dname,s.grade
    from 
      emp e
    join 
      dept d 
    on 
      e.deptno = d.deptno
    join 
      salgrade s
    on 
      e.sal between s.losal and s.hisal;

注意 : emp 表先和dept表连接，连接完成之后在和 salgrade 表连接

3.8.2 找出每一个员工的部门名称、工资等级、以及上级领导。

    select 
      e.ename,d.dname,s.grade
    from
      emp e
    join 
      dept d
    on 
      e.deptno = d.deptno
    join 
      salgrade s 
    on 
      e.sal between s.losal and hisal
    left join 
      emp e1
    on
      e.mgr = e1.empno;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210603174409.png)

### 4.子查询

4.1 什么是子查询
   
select语句当中嵌套select语句，被嵌套的select语句是子查询

4.2 子查询可以出现在哪里
    
    select 
       ..(slect).
    from 
       ..(select).
    where 
       ..(select).

4.3 where 子句中使用子查询

4.3.1 找出高于平均工资的员工信息
// 错误写法，where 后面不能直接使用分组函数。
  > select * from emp where sal > avg(sal); 
   
第一步: 找出平均工资
   > select avg(sal) from emp;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210603180246.png)

第二步 : where过滤
   > select * from emp where sal > 2073.214286;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210603180518.png)

第一步和第二步合并 : 
  > select * from emp where sal > (select avg(sal) from emp);

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210603182737.png)

4.4 from后面嵌套子查询

4.4.1 案例 : 找出每个部门平均薪水的薪资等级。

第一步 : 找出每个部门平均薪水 (按照部门编号分组，求sal的平均值)
  > select deptno,avg(sal) as avgsal from emp group by deptno;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210603183702.png)

第二步 : 将上边的查询结果当作临时表 t,让 t 表和 salgrade表连接，条件是 ：t.avgsal between s.losal and s.hisal;

    select 
      t.*,s.grade
    from 
      (select deptno,avg(sal) as avgsal from emp group by deptno) t
    join 
      salgrade s
    on 
      t.avgsal between s.losal and s.hisal;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210603184800.png)

4.5 在select后面嵌套子查询

4。5.1 案例 ： 找出每个员工所在的部门名称，要求显示员工名和部门名

 > select e.ename,(select d.dname from dept d where e.deptno = d.deptno) as dname from emp e;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210603185313.png)

4.6 union (可以将查询结果集相加)

4.6.1 案例 : 找出工作岗位是SALESMAN和MANAGER的员工

第一种 : or
   > select ename,job from emp where job = 'MANAGER' or 'SALESMAN';

第二种 : in
   > select ename,job from emp where job in('MANAGER','SALESMAN');
 
第三种 : union 
   > select ename,job from emp where job = 'MANAGER'
     union
     select ename,job from emp where job = 'SALESMAN';

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210603190304.png)

注意 : 两张不相干的表中的数据拼接在一起显示？

    select ename from emp
    union 
    select dname from dept;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210603190515.png)
