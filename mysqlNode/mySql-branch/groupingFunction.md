### 分组函数(多行处理函数) / 单行处理函数

2，20 分组函数/聚合函数/多行处理函数

- count 计数
- sum 求和
- avg 平均数
- max 最大值
- min 最小值

记住: 所有的分组函数都是对“某一组”数据进行操作的。

2.20.1 找出工资的总和？
> select sum(sal) from emp;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210601151526.png)

2.20.2 找出最高工资
> select max(sal) from emp;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210601151618.png)

2.20.3 找出最低工资
> select min(sal) from emp;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210601151654.png)

2.20.4 找出平均工资
> select avg(sal) from emp;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210601151810.png)

2.20.5 找出总人数
> select count(*) from emp;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210601152040.png)

> select count(ename) from emp;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210601152205.png)

分组函数一共有5个。分组函数还有另一个名字：多行处理函数。
多行处理函数的特点：输入多行，最终输出的结果是 1 行。

2.20.6 分组函数自动忽略NULL。
> select count(comm) from emp;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210601193734.png)

> select sun(comm) from emp;

// 自动忽略 NULL
![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210601201130.png)

多此一举：不需要添加这个额外的过滤条件，分组函数自动忽略null
> select sum(comm) from emp where comm is not null;

2.20.7 找出工资高于平均工资的员工

第一步 : 找出平均工资
> select avg(sal) from emp;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210601202233.png)

第二步 : 找出工资高于平均工资的员工
> select ename,sal from emp where sal > (select avg(sal) from emp);

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210602175416.png)


// 以下的错误信息：无效的使用了分组函数。
![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210602154549.png)

// 以上的的错误原因：SQL语句当中有一个语法规则，分组函数不可以直接使用在where子句当中。

// 因为group by 是在 where 执行之后才会执行的。

     select  5
     ...
     from    1
     ... 
     where   2
     ...
     group by  3
     ...
     having   4  
     ...
     order by  6
     ...

2.20.8 count(*) 和 count(具体某个字段) , 他们有什么区别？

- count(*) : 不是统计某个字段中数据的个数，而是统计总记录条数。（和某个字段无关）
- count(comm) : 表示统计comm字段中不为NULL的数据总数量。

  > select count(*) from emp;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210602160110.png)

> select count(comm) from emp;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210602160301.png)

> select count(job) from emp;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210602160352.png)

2.20.9 分组函数也可以组合起来用
> select count(*),sum(sal),avg(sal),max(sal),min(sal) from emp;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210602161444.png)
-

2.21 单行处理机
什么是单行处理机？
- 输入一行，输出一行。

2.21.1 计算每个员工的年薪
> select ename,(sal+comm) * 12 as yearsal from emp; // 错误写法

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210601194123.png)

使用ifnull函数处理：
> select ename,(sal + ifnull(comm,0)) * 12 as yearsal from emp; // 正确写法

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210601195530.png)

重点: 所有数据库都是这样规定的，只要有NULL参与的运算结果一定是NULL。

2.21.2 ifnull() 空处理函数？
语法格式：
> ifnull(可能为NULL的数据，被当做什么处理) : 属于单行处理函数。

2.21.3 将津贴中的 NULL 转换为 0
> select ename,ifnull(comm,0) as comm from emp;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210601194931.png)

2.21 分组查询 group by 和 having

- group by : 按照某个字段或者某些字段进行分组。
- having : 是对分组之后的字段再次过滤。

2.21.1 找出每个岗位的最高薪资
> select max(sal) from emp group by job;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210602153733.png)

注意:
- 分组函数一般都会和group by 联合使用。这也是为什么被称为分组函数的原因。
- 并且任何一个分组函数（count,sum,max,min,avg）都是在group by语句执行结束之后才会执行的。
- 当一条 sql 语句没有group by的话，整张表的数据会自成一组。

2.21.2 多字段分组查询
> select ename,max(sal),job from emp group by job;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210602175737.png)

// 以上在 mysql当中，查询结果是有的，但是结果没有意义，在Oracle数据库当中会报错，语法错误。

重点: 记住一个规则，当一条语句中有 group by 的话，select后面只能跟分组函数和参与分组的字段。

2.22.3 每个工作岗位的平均工资
> select obj,avg(sal) from emp group by job;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210602180407.png)

2.22.4 多个字段联合起来一块分组，找出每个部门不同工作岗位的最高薪资。
> select deptno,job,max(sal) from emp group by deptno,job;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210602180708.png)

2.22.5 找出每个部门的最高薪资，要求显示薪资大于2900的数据

第一步: 找出每个部门的最高薪资
> select deptno,max(sal) from emp group by deptno;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210602181225.png)

第二步: 找出薪资大于2900 这种方式效率低
> select deptno,max(sal) from emp group by deptno having max(sal) > 2900;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210602181454.png)

完美方案：效率较高，要求显示薪资大于2900的数据。
> select deptno,max(sal) from emp where sal > 2900 group by deptno;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210602181655.png)

2.22.6 找出每个部门的平均薪资

第一步 : 找出每个部门的平均薪资
> select deptno,avg(sal) from emp group by deptno;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210602182110.png)

第二步 : 要求显示薪资大于2000的数据
> select deptno,avg(sal) from emp group by deptno having avg(sal) > 2000;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210602182325.png)

// 错误，where后边不能使用分组函数，这种情况只能使用 having 过滤

> select deptno,avg(sal) from emp where avg(sal) > 2000 group by deptno; // 错误

2.23 总结一个完整的 DQL 语句怎么写

      select   5 
      ...
      from     1
      ...
      where    2
      ...  
      group by 3 
      ...
      having   4
      ... 
      order by 6
      ... 

