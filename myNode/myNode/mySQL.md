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
1. 简单的查询语句（DQL）
   > 语法格式:
   select 字段名1,字段名2,字段名3,...from 表名;
2. 提示：
- 任何一条sql语句以“;”结尾；

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210506225349.png)
- sql语句不区分大小写；

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210506225825.png)