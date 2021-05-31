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


 


