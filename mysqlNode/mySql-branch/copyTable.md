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
