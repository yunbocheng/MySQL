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
