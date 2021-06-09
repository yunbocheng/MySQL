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