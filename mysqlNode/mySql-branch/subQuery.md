### 4.子查询

4.1 什么是子查询

select语句当中嵌套select语句，被嵌套的select语句是子查询

4.2 子查询可以出现在哪里

    select 
       ..(slect).
    from 
       ..(select).
    where 
       ..(select).

4.3 where 子句中使用子查询

4.3.1 找出高于平均工资的员工信息
// 错误写法，where 后面不能直接使用分组函数。
> select * from emp where sal > avg(sal);

第一步: 找出平均工资
> select avg(sal) from emp;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210603180246.png)

第二步 : where过滤
> select * from emp where sal > 2073.214286;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210603180518.png)

第一步和第二步合并 :
> select * from emp where sal > (select avg(sal) from emp);

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210603182737.png)

4.4 from后面嵌套子查询

4.4.1 案例 : 找出每个部门平均薪水的薪资等级。

第一步 : 找出每个部门平均薪水 (按照部门编号分组，求sal的平均值)
> select deptno,avg(sal) as avgsal from emp group by deptno;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210603183702.png)

第二步 : 将上边的查询结果当作临时表 t,让 t 表和 salgrade表连接，条件是 ：t.avgsal between s.losal and s.hisal;

    select 
      t.*,s.grade
    from 
      (select deptno,avg(sal) as avgsal from emp group by deptno) t
    join 
      salgrade s
    on 
      t.avgsal between s.losal and s.hisal;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210603184800.png)

4.5 在select后面嵌套子查询

4。5.1 案例 ： 找出每个员工所在的部门名称，要求显示员工名和部门名

> select e.ename,(select d.dname from dept d where e.deptno = d.deptno) as dname from emp e;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210603185313.png)
