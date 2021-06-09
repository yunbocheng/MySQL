### 6.创建表

6.1 建表语言的语法格式 :

    creat table 表名(
      字段名1 数据类型,
      字段名2 数据类型,
      字段名3 数据类型,
      ...
    );

6.2 关MySQL当中字段的数据类型，以下只说常见的
![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210604155543.png)

6.3 char 和 varchar 怎么选择
- 在实际开发中，当某个字段中的数据长度不发生改变的时候，是定长，例如；性别、生日等都是采用char；
- 当一个字段的书库长度不确定，例如 ：简介、姓名都是采用的 varchar

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210604162050.png)

6.4 表明在数据库当中一般建议以 ： t_ 或者 tbl_ 开始

6.5 案例 ： 创建学生表

6.5.1 学生信息包括：学号、姓名、性别、班级编号、生日

- 学号 : bigint
- 姓名 : varchar
- 性别 : char
- 班级编号 : int
- 生日 : char

创建学生表语言格式:

    create table t_student(
        no bigint,
       name varchar(255),
       sex char(1),
       classno varchar(255),
       birth char(10)
    ); 

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210604162955.png)

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210604163231.png)

6.5.2 删除t_student表
注意 ： 当这个表存在的时候删除掉
> drop table if exists t_student;

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210604163355.png)
