### 5.limit 以及通用分页 / 分页查询

5.1 limit (重点中的重点，以后分页查询全靠他了)

5.2 limit是mysql特有的，其他是数据库中没有，不通用。(oracle中也有一个相同的机制，叫做rownum)

5.3 limit取结果中的部分数据，这时他的作用，

5.4 语法机制 ：

    limit startIndex,length

注意 :
- startIndex代表起始位置吗，从0开始，0代表第一条数据。
- length代表取几个。

5.5 案列 : 取出工资前5名的员工(思路: 降序取出前5)

第一步 : 将工资降序排序
> select ename,sal from emp order by sal desc ;

第二步 : 取出工资前5的员工
> select ename.sal from emp order by sal desc limit 0 , 5;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210604150303.png)

5.5 limit是sql语句最后执行的一个环节 :

    select    5
       ...
    from      1
       ...
    where     2
       ...  
    group by  3
       ...
    having    4
       ... 
    order by  6
       ...
    limit     7
       ...;

5.6 案列 ： 找出工资排名在第四到第九名的员工
> select ename,sal from emp order by sal desc limit 3,6;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210604153633.png)

5.7 通用的标准分页sql

5.7.1 每页显示3条记录 :

第1页 : 0 , 3

第2页 : 3 , 3

第3页 : 6 , 3

第4页 : 9 , 3

第5页 : 12 , 3

重点 : 每页显pagesize条记录 ：

第pageNO页 : (pageNo - 1) * pagesize , pagesize

pagesize是什么？是每页显示多少条记录
pageNo是什么？ 显示第几页

````java
   int pageNo = 2; // 页码是2
   int pagesize = 10; // 每页显示10条

   limit 10,10;
````