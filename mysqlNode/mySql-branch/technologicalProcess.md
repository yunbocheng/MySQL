## 导入数据
- 第一步：登录mysql数据库管理系统

      doc命令窗口：
       mysql -uroot -p (密码)


- 第二步：查看有哪些数据库

      show databases;  #（这个不是SQL语句，是MySQL的命令）
       #注意：这个是MYSQL命令，在Oracle中不一定能用

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210506161106.png)

- 第三步：创建属于自己的数据库

      create database bjpowernode; （这个不是SQL语句，是MySQL的命令）


- 第四步：使用bjpowernode数据

      use bjpowernode;(这个不是SQL语句，是MySQL的命令)


- 第五步：查看当前使用的数据库中有哪些表

      show tables; (这个不是SQL语句，是MySQL的命令)

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210506161142.png)

(部门表、员工表、工资等级表)
- 第六步：初始化数据

      source C:\Users\YunboCheng\Desktop\bjpowernode.sql


> 注意：
1. bjpowernode.sql，这个文件以 sql结尾，这样的文件被称为”sql“脚本。什么是sql脚本？
2. 当一个文件的扩展名是 .sql，并且该文件中编写了大量的sql语句，我们称这样的文件为sql脚本。

- 第七步：删除数据库

      drop database bjpowernode;
- 第八步 查看表结构

      desc dept；

  ![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210506163116.png)

（部门编号） （部门名称）（部门位置）

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210506213507.png)

（员工编号） （员工姓名）（工作岗位）（上级领导编号）（入职时间）（月薪）（补助/津贴）（部门编号）

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210506213541.png)

（工资等级）（最低薪资）（最高薪资）

- 第九步：查看表中的数据

      select * from emp;

    - 员工表中的所有数据

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210506214419.png)

- 部门表中的所有数据

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210506214618.png)

- 工资等级表中的所有数据

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210506214703.png)
