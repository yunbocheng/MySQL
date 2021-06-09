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