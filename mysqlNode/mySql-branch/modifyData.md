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