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
