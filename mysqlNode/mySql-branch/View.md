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