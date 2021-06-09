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

    select
     字段1，字段2...
    from
     表名
    where 
     条件;

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
    表名
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
        *      3
    from
    tablename  1
    where          
        条件    2
    order by    
        ...    4

order by 是最后执行的。


### 分组函数(多行处理函数) / 单行处理函数

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

### union (可以将查询结果集相加)

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

### 5.limit 以及通用分页 / 分页查询

5.1 limit (重点中的重点，以后分页查询全靠他了)

5.2 limit是mysql特有的，其他是数据库中没有，不通用。(oracle中也有一个相同的机制，叫做rownum)

5.3 limit取结果中的部分数据，这时他的作用，

5.4 语法机制 ：
    
    limit startIndex,length

注意 : 
- startIndex代表起始位置吗，从0开始，0代表第一条数据。
- length代表取几个。      

5.5 案列 : 取出工资前5名的员工(思路: 降序取出前5)

第一步 : 将工资降序排序
  > select ename,sal from emp order by sal desc ;

第二步 : 取出工资前5的员工
  > select ename.sal from emp order by sal desc limit 0 , 5;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210604150303.png)

5.5 limit是sql语句最后执行的一个环节 : 

    select    5
       ...
    from      1
       ...
    where     2
       ...  
    group by  3
       ...
    having    4
       ... 
    order by  6
       ...
    limit     7
       ...;

5.6 案列 ： 找出工资排名在第四到第九名的员工
   > select ename,sal from emp order by sal desc limit 3,6;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210604153633.png)

5.7 通用的标准分页sql

5.7.1 每页显示3条记录 :

第1页 : 0 , 3

第2页 : 3 , 3

第3页 : 6 , 3

第4页 : 9 , 3

第5页 : 12 , 3

重点 : 每页显pagesize条记录 ：

第pageNO页 : (pageNo - 1) * pagesize , pagesize

pagesize是什么？是每页显示多少条记录
pageNo是什么？ 显示第几页

````java
   int pageNo = 2; // 页码是2
   int pagesize = 10; // 每页显示10条

   limit 10,10;
````

### 6.创建表

6.1 建表语言的语法格式 :

    creat table 表名(
      字段名1 数据类型,
      字段名2 数据类型,
      字段名3 数据类型,
      ...
    );

6.2 关MySQL当中字段的数据类型，以下只说常见的
![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210604155543.png)

6.3 char 和 varchar 怎么选择
- 在实际开发中，当某个字段中的数据长度不发生改变的时候，是定长，例如；性别、生日等都是采用char；
- 当一个字段的书库长度不确定，例如 ：简介、姓名都是采用的 varchar

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210604162050.png)

6.4 表明在数据库当中一般建议以 ： t_ 或者 tbl_ 开始

6.5 案例 ： 创建学生表

6.5.1 学生信息包括：学号、姓名、性别、班级编号、生日

- 学号 : bigint
- 姓名 : varchar
- 性别 : char
- 班级编号 : int 
- 生日 : char

创建学生表语言格式:

    create table t_student(
        no bigint,
       name varchar(255),
       sex char(1),
       classno varchar(255),
       birth char(10)
    ); 

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210604162955.png)

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210604163231.png)

6.5.2 删除t_student表
注意 ： 当这个表存在的时候删除掉
  > drop table if exists t_student;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210604163355.png)

### 7.insert插入数据

7.1 语法格式 ： 

    insert into 表名(字段名1,字段名2,字段名3,...) values(值1,值2,值3,...)

要求 : 字段的数量和值的数量相同，并且数据类型要对应相同。

7.2 案例 ： 向 t_student表中插入数据

7.2.1 按照建表时字段名的顺序进行插入
// 插入数据 
  > insert into t_student(no,name,sex,classno,birth) values(1.'zhangsan’,'1','gaosan3ban');
  
// 查看插入后的数据
  > select * from t_student;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210604170502.png)

7.2.2  不按照建表时字段名的顺序进行插入

// 插入数据 
  > insert into t_student(name,sex,classno,birth,no) values('lisi','1','gaosan3ban','2020-01-02',2);

// 查看插入后的数据
  > select * from t_student;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210604171936.png)

7.2.3 只插入部分字段的数值 (一个字段或者多个字段)

// 插入数据
  > insert into t_student(name) values('wangwu');

// 查看插入后的数据
  > select * from t_student;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210604174358.png)
  
注意 ： 除了name字段以外，其他的字段自动插入NULL。

7.3 删除 t_student 这张表

// 当这个表存在的话删除
  > drop table if exists t_student; 

7.4 创建包含默认值的 t_student 表

     create table t_student(
        no bigint,
       name varchar(255),
       sex char(1) default 1,
       classno varchar(255),
       birth char(10)
    ); 

// 查看此时的表结构，发现 sex 字段中的 Default有默认值1
> desc t_student;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210604175324.png)

// 插入数据
  > insert into t_student(name) values('zhangsan');

// 查看数据
  > select * from t_student;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210604175721.png)

上表注意 ：此时并没有输入 sex 的值，建表的时候将sex赋值为1 所以在sex中存在默认值 1

关于insert语句的注意 ：

- 当一条insert语句执行成功之后，表格当中必然会多出一行记录。
- 即使多的这一行记录当中有某些字段是NULL，后期也没有办法在执行insert语句插入数据
- 只能使用 update 进行更新。

7.5 省略的 insert 查询语句
  > insert into t_student values(4,'lisi','1','gaosan3ban','2020-01-02');

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210605181020.png)

  > insert into t_student values(2,'wangwu','1','gaosan3abn');

// 此时输入的字段值数量不够，会报错。
![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210605182537.png)

注意 ：

- 字段可以省略不写，但是后面的value对数量和顺序都有要求。
- 这个省略了字段名称，直接输入的就是字段的值。
- 输入字段值的时候一定要注意输入字段值的顺序要和表中的字段顺序保持一致。

7.6 一次插入多行数据
  > insert into t_student(no,name,sex,classno,birth) values(3,'wangwu','1','gaosan3ban','2020-01-02'),(5,'zhouliu','0','gaosan2ban','2020-02-03');

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210605183600.png)\

### 8.表的复制以及批量插入

8.1 表的复制语法:

    creat table 表名 as select语句；
    将查询的结果常见出来。

8.1.1 将整张表进行复制

第一步 : 创建一个新表并进行复制整张表的字段
   > create table emp1 as select * from emp;

第二步 : 查看表的结构
   > desc emp1;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210605184529.png)

第三步 : 查看表中的数据 
   > select * from emp1;

重点 ： 此时发现 emp1 表的数据完全 copy的就是 emp 表的数据

8.1.2 对某张表的部分字段进行复制

第一步 : 创建一个新表并进行复制某张表的部分字段
   > create table emp2 as select ename,sal from emp;

第二步 : 查看表结构
   > desc emp2;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210605185422.png)

第三步 : 查看表中的数据
   > select * from emp2;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210605185522.png)

重点 : 此时的emp2表只是复制了 emp 表的ename,sal字段的数据。

8.2 将查询结果插入到一张表中

第一步 : 创建一个新表并进行复制
   > create table dept1 as select * from dept;

第二步 : 查询表的结构
   > desc dept1;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210605190333.png)

第三步 : 查询表的数据
  > select * from dept1;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210605190426.png)

第四步 : 向 dept1 中插入数据
  > insert into dept1  select * from dept;

第五步 : 查看表中的数据
  > select * from dept1;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210605190902.png)

重点 : 
- 在创建表的时候复制的就是dept，其中已经有了一份dept的数据
- 并且在插入数据的时候使用的还是dept表中的数据，所以此时dept1中的数据有两份

### 9.修改数据 (update)

9.1 语法格式 ： 

    update 表名 set 字段名1=值1,字段值2=值2...where 条件;

注意 ： 没有条件整张表数据全部更新。

9.2 案例 ：将部门10的LOC修改为SHANGHAI，将部门名称修改为RENSHIBU;

第一步 ： 修改数据（loc字段和dname字段，只修改10部门的数据）
  > update dept1 set loc = 'SHANGHAI',dname = 'RENSHIBU' where deptno = 10;

第二步 ： 查看数据
  > select * from dept1;
![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210605192305.png)

重点 ：语句意思，将10部门的loc改为SHANGHAI，dname改为RENSHIBU;

注意 ：一定要注意连接两个字段的是英文下的逗号，而不是and

9.3 跟新所有记录

第一步 ：修改全部数据（修改loc字段和dname字段，全部部门都修改）
  > update dept1 set loc = 'x',dname = 'y';

第二步 ： 查看数据 
   > select * from dept1;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210605195907.png)

### 删除数据  (delete)

9.1 语法格式： 

    delete from 表名 where 条件;

注意 : 没有条件全部删除

9.2 案例 ： 删除10部门数据

第一步 : 删除 10 部门的数据
  > delete from dept1 where deptno = 10;

第二步 : 查看数据
  > select * from dept1;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210605200727.png)

9.3 删除所有数据
  > delete from dept1;
 
9.4 怎么删除大表(重点)
// 表被截断，不可回滚。永久丢失，删除表中的数据马，表结构还在
  > truncate table 表名; 

9.5 删除整个大表，包括表结构和数据
  > drop table 表名; 通用的删除表语言
  > drop table if exists 表名; mysql中特有，oracle中不存在

### 表的结构修改

DQL(select) DML(insert delete update) DDL(create drop alter)

修改表结构的语句不会出现在java代码中，出现在java代码当中的sql包括：insert、delete、update、select（这些都是表中的数据操作）
增删改查有一个术语 : CRUD操作
Creat (增) Retrieve (检索) Update (修改) Delete (删除)


### 10.约束

10.1 什么书约束? 常见的约束有哪些？

注意：比如注册一个新的用户，底层就相当于执行一次insert语句

在创建表的时候，可以给表的字段添加相应的约束，添加约束的目的是为了保证表中数据的合法性、有效性、完整性。

常见的约束有哪些 ？

- 非空约束 (not null) : 约束的字段不能为 NULL
- 唯一性 (unique)  : 约束的字段不能重复
- 主键约束 (primary key) : 约束的字段既不能为NULL，也不能重复(简称pk)
- 外键约束 (foreign key) : ...(简称FK)
- 检查约束 (check) ： 注意oracle数据库有check约束，但是mysql没有，目前mysql不支持该约束。

10.2 非空约束 (not null)

第一步 ：创建一个新的表

    drop table if exists t_user;
    create table t_user(
      id int,
      username varchar(255) not null,
      password varchar(255)
    );

第二步 : 向表中插入数据
   > insert into t_user(id,username,password) values(1,'zhangsan','123');

第三步 ：查看表的数据
  > select * from t_user;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210606123125.png)

错误案例 ：
   > insert into t_user(id,password) values(1,'444');

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210606123703.png)

注意 ： 

错误原因，在创建表的时候已经声明username不能为null

查看表的结构可以发现，在username字段的NULL为NO，说明username必须有值，不能为null
> desc t_user;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210606124010.png)

10.3 唯一性约束 (unique)

10.3.1 唯一性约束修饰的字段具有唯一性，不能重复，但可以为NULL

10.3.2 案列 ：给一个字段(列)加约束条件

第一步 ：判断是否存在t_user表，如果存在将整个表删除并创建一个新的表,使用的是
    drop table if exists t_user;
    create table t_user(
      id int,
      username varchar(255) unique
    );

第二步 : 插入数据
   > insert into t_user values(1,'zhangsan');
   > insert into t_user values(2,'zhangsan');

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210606141233.png)

注意：
- 第一条语句可以插入成功，但是执行第二条语句插入失败，错误原因：
- 第二条语句中的username字段的值与第一条语句中username的值一样，报错
- 因为在建表的时候username字段加入了约束条件，该字段的值不能重复。

第三步 ： 查看表的结构
   > desc t_user;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210606141144.png)

注意 ： 查看表结构的时候发现，表结构中的username中的Key字段有UNI关键字，说明这个字段的值不能重复。

10.3.3 username可以为NULL

第一步 ：插入数据，不给定username的值，默认值为NULL(空)
> insert into t_user(id) values(2);
> insert into t_user(id) values(3);
> insert into t_user(id) values(4);

第二步 : 查看表的数据
> select * from t_user;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210606142708.png)

10.3.4 给多个字段(列)加约束条件

10.3.4.1 表级约束 多个字段联合起来添加一个约束unique
第一步 ：判断是否存在t_user表，如果存在将整个表删除并创建一个新的表

重点 ：
- 这样的语法格式，代表将usercode与username合并为一个字段，使用的是一个约束条件，
- 即只有当usercode与username的字段值都与上一次的字段值相同值相同时，才会报错，当作同一个数据。
  

    drop table if exists t_user;
    create table t_user(
      id int,
      usercode varchar(255),
      username varchar(255), 
      unique(usercode,username)
    );

第二步 : 插入数据
> insert into t_user values(1,'111','zhangsan');
> insert into t_user values(2,'111','wangwu');
> insert into t_user values(3,'222','zhangsan');

第三步 ：查看表的结构
> desc t_user;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210606145619.png)

注意 : 此时即表级约束中，发现usercode与username中只有usercode中的Key字段都为UNI；而username不为UNI，此时他两是绑在一起的。

第四步 ： 查看表中的数据
> select * from t_user;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210606145712.png)

第五步 ： 插入重复的数据
> insert into t_user values(4,'111','zhangsan');

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210606145812.png)

注意:此时会报错(usercode”键的重复条目“111 zhangsan)，因为插入的数据与第一次插入的数据usercode字段值和username字段值都一样.

10.3.4.2 列级约束 各自管自己的，只有当约束的字段值全不重复的时，才会成功，不会报错。

第一步 ：判断是否存在t_user表，如果存在将整个表删除并创建一个新的表

重点 ：
- 这样的语法格式，代表将usercode与username各为一个字段，使用的是两个个约束条件，
- 即当usercode与username的字段值只要有一个不一样的时候就会报错。


    drop table if exists t_user;
    create table t_user(
      id int,
      usercode varchar(255) unique,
      username varchar(255) unique
    );

第二步 : 插入数据
> insert into t_user values(1,'111','zhangsan');
> insert into t_user values(2,'222','wangwu');
> insert into t_user values(2,'111','wangwu');
> insert into t_user values(3,'222','zhangsan');

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210606151747.png)

注意 ：
- 此时只有1行与2行的数据插入成功，因为前两行usercode与username的字段值都不行同
- 而后来两行数据中，usercode与username的字段值其中有一个字段是重复的，报错
第三步 ：查看表的结构
> desc t_user;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210606152111.png)

注意 : 此时即列级约束中，发现usercode与username中的Key字段都为UNI；

第四步 ： 查看表中的数据
> select * from t_user;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210606152146.png)

注意 ：只有前两行数据，后边的两行插入失败，因为有重复。

10.4  注意 : not null约束只有列级约束，没有表级约束。

10.5 主键约束

重点 : 一张表只有一个主键，必须记住。

10.5.1 怎么给一张表添加主键约束 (使用列级约束加入主键约束)

第一步: 判断是否存在t_user表，如果存在将整个表删除并创建一个新的表
   
    drop table if exists t_user;
    create table t_user(
       id int primary key,
       username varchar(255),
       email varchar(255)
    );

第二步: 插入数据
> insert into t_user(id,username,email) values(1,'zs','zs@123.com');
> insert into t_user(id,username,email) values(3,'ls','ls@123.com');
> insert into t_user(id,username,email) values(2,'ww','ww@123.com');

第三步 : 查看表结构
> desc t_user;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210606160027.png)

第四步 : 查看表中的数据

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210606160227.png)

插入错误的数据
> insert into t_user(id,username,email) values(1,'ww','ww@123.com');

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210606160618.png)
解释 ：报错的原因是插入的id的字段值与以前插入的字段值重复。

> insert into t_user(username,email) values('ww','ww@123.com');

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210606161143.png)
解释 : 字段id没有默认值，报错的原因是插入id字段值为NULL。

10.5.2 根据以上的测试得出的结论：

- id是主键，因为添加了主键约束，主键字段中的数据不能为NULL，也不能重复。

10.5.3
主键的特点 : 
- 不能为NULL
- 不能重复

10.5.3 主键的相关的术语
- 主键约束 : primary key
- 主键字段 : i字段添加primary key之后，id叫做主键字段
- 主键值  : id字段中的每一个值都是主键值

10.5.4 主键有什么作用

- 表的设计三范式中有要求，第一范式就要求任何一张表都应该有主键。
- 主键的作用 : 主键值是这行记录在这张表当中的唯一标识。（就像一个人的身份证号一样）

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210606164720.png)


10.5.5  使用表级约束方式定义主键 ：

第一步 ：删除表并创建新表

    drop table if exists t_user;
    create table t_user(
      id int,
      username varchar(255),
      primary key(id)
    );

第二步 : 插入数据
  > insert into t_user(id,username) values(1,'zs');
  > insert into t_user(id,username) values(2,'ls');
  > insert into t_user(id,username) values(3,'ww');
  > insert into t_user(id,username) values(4,'cs');

第三步 : 查看表结构
> desc t_user;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210606165510.png)
注意 : id此时为主键，所以NULL不能为YES，key字段为PRI，代表为主键。

第四步 : 查看表的数据
> select * from t_user;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210606165842.png)

插入错误的数据
> insert into t_user(id,username) values(4,'cx');

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210606170134.png)
解释： 出现错误，原因是插入的id数据重复。

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210606170233.png)

10.6 主键值自增 (重点)

10.6.1 mysql提供主键值自增：

删除旧表，创建新表

    drop table if exists t_user;
    create table t_user( 
       id int primary key auto_increment,
       username varchar(255)
    );

注意 ：id字段自动维护一个自增的数字，从1开始，以1递增。

插入数据 ：
> insert into t_user(username) values('a');
> insert into t_user(username) values('a');
> insert into t_user(username) values('a');
> insert into t_user(username) values('a');
> insert into t_user(username) values('a');
> insert into t_user(username) values('a');
 
查看此时表的结构
![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210606171516.png)

注意 ：extra代表的是 额外的,可以看到这个表结构中添加了额外的数据，即主键值自增。

查看表的数据
![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210606171846.png)

注意 ：可以看出id是从1开始自增的，

提示 ；在oracle中也提供了一个相同的自增机，叫做：序列(sequence)对象。

10.7 外键约束

10.7.1 关于外键约束的相关术语

- 外键约束 : foreign key
- 外键字段 : 添加有外键约束的字段
- 外键值 : 外键字段中的每一个值

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210607173738.png)

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210607174016.png)

10.7.2 将以上表的建表语句写出来 : 

注意 : t_student中的classno字段引用t_class表中的cno字段，此时t_student表叫做子表。t_class表叫做父表。

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210607174313.png)

    先删除子表在删除父表
    drop table if exists t_student;
    drop table if exists t_class;
    
    先创建父表在创建子表
    
    create table t_class(
        cno int,
        cname varchar(255),
        primary key(cno)
    );

    create table t_student(
      son int,
      sname varchar(255),
      classno int,
      foreign key(classno) references t_class(cno)
    );

    insert into t_class values(101,'xxxxxxxxxxxxx');
    insert into t_class values(102,'yyyyyyyyyyyyy');

    insert into t_student values(1,'zs1',101);
    insert into t_student values(1,'zs1',101);
    insert into t_student values(1,'zs1',101);
    insert into t_student values(1,'zs1',101);
    insert into t_student values(1,'zs1',101);

    select * from t_class;
    select * from t_student;

插入错误数据
> insert into t_student values(7,'lisi',103);

错误信息 :

mysql> insert into t_student values(7,'lisi',103);
ERROR 1452 (23000): Cannot add or update a child row: a foreign key constraint fails (`bjpowernode`.`t_student`, CONSTRAINT `t_student_ibfk_1` FOREIGN KEY (`classno`) REFERENCES `t_class` (`cno`))

10.7.3 外键可以为你NULL嘛？
  
外键值可以为 NULL。

第一步 : 插入外键为空的
   > insert into t_student(son,sname) values(6,'zs6');

第二步 : 查看数据
   > select * from t_student;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210608142841.png)

10.7.4 外键字段引用其他表的某个字段的时候，被引用的字段必须是主键嘛？

注意: 被引用的字段不一定是主键，但至少具有unique约束。

### 11.存储引擎

11.1 查看建表语句，其中就带有存储引擎
   > show create table emp;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210608143726.png)

注意 : 其中注意 : 其中ENGINE=InnoDB代表引擎 DEFAULT CHARSET=utf8代表字符集是哪个类型的。

11.2 案例 ： 创建一个新表 查看默认的存储引擎

第一步 ： 创建一个新表
> create table t_x(id int);

第二步 : 查看表的存储引擎
> show create table t_x;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210608144319.png)

11.3 完整的建表语句

Create  TABLE `t_x` (
`id` int(11) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

注意 ：
- 在mysql中，凡是标识符可以使用飘号括起来。最好别用，不通用。
- `1`或者``1``都可以。可以加入多个飘号。
- mysql默认使用的存储引擎是InnoDB方式。
- 默认采用的字符集是UTF8

11.4 什么是存储引擎

注意 : 
- 存储引擎这个名字只有在mysql中存在。
- oracle中有对应的机制，但是不叫做存储引擎。oracle中没有特殊的名字，就是“表的存储方式”；

11.5 
- mysql支持很多存储引擎，每一个存储引擎都对应一种不同的存储方式。
- 每一个存储引擎都有自己的优缺点，需要在合适的时机选择合适的存储引擎。

11.6 查看当前mysql支持的存储引擎

第一步 : 查看当前数据库版本
> select version();

第二步 : 查看当前版本数据库中的存储引擎都有什么
> show engines \G;

         mysql> show engines \G;
         *************************** 1. row ***************************
         Engine: FEDERATED
         Support: NO
         Comment: Federated MySQL storage engine
         Transactions: NULL
         XA: NULL
         Savepoints: NULL
         *************************** 2. row ***************************
         Engine: MRG_MYISAM
         Support: YES
         Comment: Collection of identical MyISAM tables
         Transactions: NO
         XA: NO
         Savepoints: NO
         *************************** 3. row ***************************
         Engine: MyISAM
         Support: YES
         Comment: MyISAM storage engine
         Transactions: NO
         XA: NO
         Savepoints: NO
         *************************** 4. row ***************************
         Engine: BLACKHOLE
         Support: YES
         Comment: /dev/null storage engine (anything you write to it disappears)
         Transactions: NO
         XA: NO
         Savepoints: NO
         *************************** 5. row ***************************
         Engine: CSV
         Support: YES
         Comment: CSV storage engine
         Transactions: NO
         XA: NO
         Savepoints: NO
         *************************** 6. row ***************************
         Engine: MEMORY
         Support: YES
         Comment: Hash based, stored in memory, useful for temporary tables
         Transactions: NO
         XA: NO
         Savepoints: NO
         *************************** 7. row ***************************
         Engine: ARCHIVE
         Support: YES
         Comment: Archive storage engine
         Transactions: NO
         XA: NO
         Savepoints: NO
         *************************** 8. row ***************************
         Engine: InnoDB
         Support: DEFAULT
         Comment: Supports transactions, row-level locking, and foreign keys
         Transactions: YES
         XA: YES
         Savepoints: YES
         *************************** 9. row ***************************
         Engine: PERFORMANCE_SCHEMA
         Support: YES
         Comment: Performance Schema
         Transactions: NO
         XA: NO
         Savepoints: NO
         9 rows in set (0.00 sec)

在此版本中存在9大存储引擎。

11.7 MyISAM 存储引擎

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210608150937.png)

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210608151015.png)

11.8 InnoDB 存储引擎

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210608151220.png)

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210608151313.png)

11.9 MEMORY 存储引擎

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210608151436.png)

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210608151844.png)

注意 ：
- 其中的TEXT文件和BLOB文件都是存储的二进制文件，而CLOB可以直接存储文本。
- 表数据及索引被存储在内存中，笔记本关机之后会数据消失。

### 12.事务的相关知识

12.1 什么是事务 ？

- 一个事务是一个完整的业务逻辑单元，不可再分。

比如 : 银行账户转账，从A账户向B账户转账10000，需要执行两条update语句：
> update t_act set balance = balance - 10000 where catno = 'act-001';
> update t_act set balance = balance + 10000 where catno = 'act-002';

以上两条DML语句必须同时成功，或者失败，不允许出现一条成功，一条失败。
![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210608152240.png)

要想保证以上的两条DQL语句同时成功或者失败，那么就需要使用数据库的“事务机制”。

12.2 
12.2.1和事务相关的语句只有 : DML语句。(insert delete update)

因为他们这三个语句都是和数据库表当中的“数据”相关的。
事务的存在是为了保证数据的完整性，安全性。

12.2.3 假设所有的业务都能使用1一条DML语句搞定，还需要事务机制嘛

不需要，但是实际情况不是这样的，通常是一个”事儿（事务【业务】）“需要多条DML语句联合完成。

12.3 事务的原理

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210608154752.png)

12.4 事务的特性 : 事务包括四大特性 ACID
- A: 原子性 ：事务是最小的工作单元，不可再分。
- C: 一致性 ：事务必须保证多条DML语句同时成功或者失败。
- I: 隔离性 ：事务A与事务B之间具有隔离（线程）
- D: 持久性 ：持久性说的是最终数据必须持久化到硬盘中,事务才算成功。

12.5 关于事务之间的隔离性

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210608155505.png)

oracle数据库默认的隔离级别是 : 读已提交。
mysql数据库默认的隔离级别是 : 可重复读。

12.6 演示事务

12.6.1 mysql事务默认情况下是自动提交的。

什么是默认提交 ？ 只要执行任意一条DML语句则提交一次。

怎么关闭自动提交 ？ start transaction;

12.6.2 演示不关闭DML语句自动提交事务： 

第一步：删除已经存在的表并创建一个新表
    
    drop table if exists t_user;
    create table t_user(
     id int primary key auto_increment,
     username varchar(255)
     );
    
第二步: 插入数据
     
     insert into t_user(username) values('zs');

第三步 : 查看没有回滚之前的数据
    
     select * from t_user;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210608160722.png)

第四步 : 回滚数据
    
    rollback';

第五步 : 查看回滚之后的表数据

    select * from t_user;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210608161208.png)

重点 : 此时没有使用commit进行提交，使用DML语句自动进行了提交。

12.6.3 演示关闭DML语句自动提交事务：

第一步 ：关闭默认提交事务

    start transaction;

第二步 : 插入数据

    insert into t_user(username) values('lisi');

第三步 : 查看没有回滚之前的数据
   
    select * from t_user;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210608162231.png)

第四步 : 回滚数据
    
    rollback;

第五步 : 查看回滚后的数据

    select * from t_user;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210608162259.png)

重点 ：此时关闭了DML语句自动提交事务，回滚之后没有提交的事务将被删除，此时必须使用commit进行提交。

第六步 : 使用commit提交事务
    
    插入数据
    insert into t_user(username) values('lisi');
    查看提交之前的数据
    select * from t_user;
    提交数据
    commit;
    查看提交之后的数据
    select * from t_user;
    回滚数据
    rollback;
    查看回滚后的数据
    select * from t_user;

查看提交之前的数据

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210608163916.png)

查看提交之后的数据

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210608163916.png)

查看回滚之后的数据

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210608163916.png)

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210608164342.png)

### 13.索引

- 创建索引对象 ： 
  > create index 索引名称 on 表名(字段名);

- 删除索引对象 ：
  > drop index 索引名称;
  
![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210608164550.png)

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210609175933.png)

查看sql语句的执行计划 
  > explain select ename,sal from emp where sal = 50000;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210609180157.png)
注意 : 此时还没有给sal字段添加索引，type字段值为ALL，代表需要查询的是所有sal的数据，rows为14代表查询的数据为14条。

给薪资sal字段添加索引 ：
   > create index emp_sal_index on emp(sal);

查看此时的执行计划
  > explain select ename,sal from emp where sal = 50000;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210609181019.png)

索引的实现原理 : 
![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210609181218.png)

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210609181324.png)

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210609181409.png)

### 14.视图

14.1 什么是视图

站在不同的角度去看到数据，（同一张表的数据，通过不同的角度去看待）

14.2 创建视图

    create view myview as select empno,ename from emp;

14.3 删除视图

    drop view myview;

注意 : 只有DQL语句才能以视图对象的方式常见出来。

14.3 对视图进行增删改查，会影响到原表中的数据。（通过视图影响原表数据的，不是直接操作的原表）。可以对视图进行CRUD操作。

14.4 面向视图操作

14.4.1 查看视图中的数据
   > select * from myview;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210609183158.png)

14.5 复制一个emp表进行操作，为了不影响原来的emp表
    
第一步 ：复制整张emp表
  > create table emp_bak as select * from emp;

第二步 ：创建emp_bak的视图
  > create view myview1 as select empno,ename,sal from emp_bak;

第三步 ：查看修改前视图中的数据
  > select * from myview1;

第四步 ： 修改myview1中的数据
   > update myview1 set ename='hehe',sal=1 where empno = 7369;

第五步： 查看修改后myview1中的数据
   > select * from myview1;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210609184229.png)

注意通过视图修改原始表中的数据

第五步 ： 查看此时emp_bak中的数据
   > select * from emp_bak;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210609184732.png)

注意 ： 可以看到此时部门号为7369的部门数据进行了修改

第六步 ：删除emp_bak的视图myview1  
   > drop view myview1;
 
视图的作用 

视图可以隐藏表的实现细节。保密级别较高的系统，数据库只对外提供相关的视图，java程序员只对视图对象进行CRUD;

### 15.数据的导入和导出

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210609185518.png)

### 16.数据库的三范式

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210609190046.png)

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210609190136.png)

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210609190325.png)

提醒 : 在实际的开发中，以满足客户的需求为主，有的时候会拿冗余换执行速度。

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210609190640.png)

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210609190705.png)



