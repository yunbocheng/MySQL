### 2.条件查询语句

2.1 语法格式

    select
    字段1，字段2...
    from
    表名
    where
    条件;
执行顺序：先from ，然后where，最后select

2.2 查询工资等于 5000 的员工姓名？
> select ename from emp where sal = 5000;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531172036.png)

2.3 查询 SMITH 的工资
> select sal from emp where ename = 'SMITH'; // 字符串用单引号括起来

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531172358.png)

2.4 找出工资高于 3000 的员工
> select ename,sal from emp where sal > 3000;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531172824.png)

> select ename,sal from emp where sal >= 3000;

> select ename,sal from emp where sal < 3000;

> select ename,sal from emp where sal <= 3000;

2.5 找出工资不等于3000的
> select ename,sal from emp where sal <> 3000;

> select ename,sal from emp where sal != 3000;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531173254.png)

注意：不等于可以是 <> 或者 != ，两个都可以的

2.6 找出工资在1100和3000之间的员工，包括1100和3000；
> select ename,sal from emp where sal >=1100 and sal <= 3000; // 使用的是 and

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531173742.png)

2,7 使用的是 between...and...是闭区间[a,b] [1100,3000];
> select ename,sal from emp where sal between 1100 and 3000;

注意：between...and...在使用的时候必须左小右大

2.8 between...adn...除了可以使用在数字方面，还可以使用在字符串方面

字符串使用 between...and... 判断的是字符串的第一个字符，所得的结果是 左闭右开区间 [a,b);,

> select ename from emp where ename between 'A' and 'B';

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531175029.png)

2.9 找出哪些人津贴为NULL;
注意: 在数据库当中NULL不是一个值，代表什么都没有，为空。
空不是一个值，不能用等号衡量。
必须使用 is null 或者 is not null
0.0 也属于 NUll ,他代表 0 数值。

select ename,comm from emp where comm = null; 错误写法，不能进行赋值。

> select ename,comm from emp where comm is null;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531175628.png)

2.10 找出哪些人津贴不为 NULL
> select ename,sal,comm from emp where comm is not null;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531180643.png)

2.11 找出那些人没有津贴
> select ename,sal,comm from emp where comm is null or comm = 0;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531180956.png)

2.12 找出工作岗位是 MANAGER 和 SALESMAN 的员工
> select ename,job from emp where job = 'MANAGER' or job = 'SALESMAN';

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531182005.png)

2.13 and 和 or 联合起来用：找出薪资大于1000并且部门是20或者30部门的员工
> select ename,sal,deptno from emp where sal > 1000 and (deptno = 20 or deptno = 30);

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531183104.png)

注意: 当运算符的优先级不确定的时候，可以加括号调整计算顺序。

2.14 in 等同于 or :找出工作岗位是 MANAGER 和 SALESMAN 的员工
> select ename,job from emp where job = 'MANAGER' or 'SALESMAN';
> select ename,job from emp where job in('MANAGER','SALESMAN');

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531183650.png)

注意：in后面的值不是区间，是具体的值。
> select ename,job from emp where sal in(800,5000);

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531184451.png)

2.15 not in 不在这几个值当中
> select ename,job,sal from emp where sal not in(800,5000);

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531184955.png)

2.15 模糊查询 like

在模糊查询中，必须掌握两个特殊的符号，一个是%，一个是_

%代表任意多个字符，_代表任意一个字符

2.15.1找出名字中含有o的？
> select ename from emp where ename like "%o%";

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531203650.png)

2.15.2 找出名字中第二个字母是A的？
> select ename from emp where ename like '_A%';

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531204101.png)

2.15.3 取出名字里有下划线的名字
> select ename from emp where ename like '%\_%';

注意: 此时 \_ 代表一个普通的 下划线 _

2.15.4 找出名字最后一个字母是T的
> select ename from emp where ename like '%T';

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531204859.png)

2.16 排序 （升序，降序）
语法格式：

    select
    字段值1，字段值2...
    from
      表名
    order by
       字段值;

2.17 按照工资升序，找出员工名和薪资
> select ename,sal from emp order by sal; (这个为默认，默认升序)

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531210041.png)

注意：默认是升序。怎么指定升序或者降序？asc表示升序，desc表示降序。
> select ename,sal from emp order by sal; (默认升序)
>
> select ename,sal from emp order by sal asc;
>
> select ename,sal from emp order by sal desc;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531210537.png)

2.18 按照工资的降序排列，当工资相同的时候在按照名字的升序排列。
> select ename,sal from emp order by sal desc,ename asc;

注意: 越靠前的字段越能起主导作用。只有当前面的字段无法完成排序的时候，才会启用后面的字段

练手:
> select ename,sal from emp order by 1;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531212631.png)

> select ename,sal from emp order by 2;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531212716.png)

> select * from emp order by 6;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531212816.png)

2.19 找出工作岗位是 SALESMAN 员工，并且要求按照薪资的降序排序

     select
         ename,job,sal
     from
        emp
     where
        job = 'SALESMAN'
     order by 
        sal desc;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531214327.png)

执行顺序 ： 先执行from,在执行where，在执行select,最后在执行order by 。
    
    select
        *      3
    from
    tablename  1
    where          
        条件    2
    order by    
        ...    4

order by 是最后执行的。