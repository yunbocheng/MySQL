## SQL语句
### 1.简单查询语句
1.1 简单的查询语句（DQL）
> 语法格式:
select 字段名1,字段名2,字段名3,...from 表名;

1.2 提示：
- 任何一条sql语句以“;”结尾；

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210506225349.png)
- sql语句不区分大小写；

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210506225825.png)

1.3 查询员工的年龄?(字段可以参与数学运算)
> select ename,sal * 12 from emp;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531165204.png)

1.4 给查询结果的列重命名
> select ename,sal * 12 as yearsal from emp; // 取的为英文名字

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531170258.png)
> select ename,sal * 12 as '年薪' from emp; // 取的为中中文名字

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531170150.png)

注意：Mysql 中字符串可以使用 单引号 或者 双引号 括起来
而在 oracle 中字符串只能使用 单引号 括起来
建议以后都使用单引号括起来
重点：语句中的 as 可以省略不写
> select ename,sal * 12 '年薪' from emp;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210531170554.png)

1.5总结 ：

1.5.1 查询一个字段
> select ename from emp;

1.5.2 查询多个字段
> select ename.sal from emp;

1.5.3 查询全部字段
> select * from emp; (不建议使用，*代表全部字段，要将*装换为全部字段，效率低)
