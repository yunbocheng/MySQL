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
