### 13.索引

- 创建索引对象 ：
  > create index 索引名称 on 表名(字段名);

- 删除索引对象 ：
  > drop index 索引名称;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210608164550.png)

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210609175933.png)

查看sql语句的执行计划
> explain select ename,sal from emp where sal = 50000;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210609180157.png)
注意 : 此时还没有给sal字段添加索引，type字段值为ALL，代表需要查询的是所有sal的数据，rows为14代表查询的数据为14条。

给薪资sal字段添加索引 ：
> create index emp_sal_index on emp(sal);

查看此时的执行计划
> explain select ename,sal from emp where sal = 50000;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210609181019.png)

索引的实现原理 :
![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210609181218.png)

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210609181324.png)

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210609181409.png)
