### union (可以将查询结果集相加)

4.6.1 案例 : 找出工作岗位是SALESMAN和MANAGER的员工

第一种 : or
> select ename,job from emp where job = 'MANAGER' or 'SALESMAN';

第二种 : in
> select ename,job from emp where job in('MANAGER','SALESMAN');

第三种 : union
> select ename,job from emp where job = 'MANAGER'
union  
select ename,job from emp where job = 'SALESMAN';

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210603190304.png)

注意 : 两张不相干的表中的数据拼接在一起显示？

    select ename from emp
    union 
    select dname from dept;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210603190515.png)