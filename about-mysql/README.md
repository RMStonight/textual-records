# mysql学习记录

[docker相关点击此处](#docker中的安装使用)

## 基础知识

学习链接：[B站黑马程序员]

SQL分类

| 分类 | 全称 | 说明 |
| ---- | ---- | ---- |
| [DDL](#ddl) | Data Definition Language | 数据定义语言，用来定义数据库对象（数据库，表，字段） |
| [DML](#dml) | Data Manipulation Language | 数据操作语言，用来对数据库表中的数据进行增删改 |
| [DQL](#dql) | Data Query Language | 数据查询语言，用来查询数据库中表的记录 |
| [DCL](#dcl) | Data Control Language | 数据控制语言，用来创建数据库用户、控制数据库的访问权限 |

### DDL

[返回](#基础知识)

#### 数据库操作

查看当前有哪些数据库

```sh
show databases
```

创建数据库

```sh
create database <name>
create database <name> if not exist
```

切换到（使用）某个数据库

```sh
use <name>
```

查看当前处于哪个数据库中

```sh
select database()
```

删除数据库

```sh
drop database <name> if exist
```

#### 表操作

查看当前数据库所有的表

```sh
show tables
```

创建表

```sh
create table 表名 (字段 字段类型，字段 字段类型)
```

查看当前表的字段

```sh
desc <name>
```

查询当前表的建表语句

```sh
show create table <name>
```

表结构修改，添加字段/修改字段类型/修改字段名称及类型/删除字段/修改表名

```sh
alter table <name> add/modify/change/drop/rename to...
```

删除表

```sh
drop table <name>
```

### DML

[返回](#基础知识)

#### 添加数据

```sh
insert into employee(id, workno, name, gender, age, idcard, entrydate) values (1,'1','Itcast','男',10,'123456789012345678','2000-01-01') ;

insert into employee values (2,'2','张无忌','男',18,'123456789012345670','2005-01-01') ;

insert into employee values (3,'3','韦一笑','男',38,'123456789712345670','2005-01-01'),(4,'4','赵敏','女',18,'12345675712345670','2005-01-01') ;

select * from employee ;
```

#### 修改数据

修改id为1的数据，将name修改为itheima

```sh
update employee set name = 'itheima' where id = 1;
```

修改id为1的数据，将name修改为小昭，gender修改为女

```sh
update employee set name = '小昭', gender = '女' where id = 1;
```

将所有的员工入职日期修改为2008-01-01

```sh
update employee set entrydate = '2008-01-01';
```

#### 删除数据

删除gender为女的员工

```sh
delete from employee where gender = '女';
```

删除所有员工

```sh
delete from employee;
```

### DQL

[返回](#基础知识)

#### 向名为emp的table填入数据，方便后续查询测试

```sh
insert into emp (id, workno, name, gender, age, idcard, workaddress, entrydate)
value (1, '1', '柳岩', '女', 20, '123456789012345678', '北京', '2000-01-01'),
    (2, '2', '张无忌', '男', 18, '123456789012345670', '北京', '2005-09-01'),
    (3, '3', '韦一笑', '男', 38, '123456789712345670', '上海', '2005-08-01'),
    (4, '4', '赵敏', '女', 18, '123456757123845670', '北京', '2009-12-01'),
    (5, '5', '小昭', '女', 16, '123456769012345678', '上海', '2007-07-01'),
    (6, '6', '杨逍', '男', 28, '12345678931234567X', '北京', '2006-01-01'),
    (7, '7', '范瑶', '男', 40, '123456789212345670', '北京', '2005-05-01'),
    (8, '8', '黛绮丝', '女', 38, '123456157123645670', '天津', '2015-05-01'),
    (9, '9', '范凉凉', '女', 45, '123156789012345678', '北京', '2010-04-01'),
    (10, '10', '陈友谅', '男', 53, '123456789012345670', '上海', '2011-01-01'),
    (11, '11', '张士诚', '男', 55, '123567897123465670', '江苏', '2015-05-01'),
    (12, '12', '常遇春', '男', 32, '123446757152345670', '北京', '2004-02-01'),
    (13, '13', '张三丰', '男', 88, '123656769012345678', '江苏', '2020-11-01'),
    (14, '14', '灭绝', '女', 65, '123456719012345670', '西安', '2019-05-01'),
    (15, '15','胡青牛', '男', 70, '12345674971234567X', '西安', '2018-04-01'),
    (16, '16', '周芷若', '女', 18, null, '北京', '2012-06-01');
```

#### 基本查询

查询指定字段 name, workno, age 返回

```sh
select name,workno,age from emp;
```

查询所有字段返回

```sh
select id, workno, name, gender, age, idcard, workaddress, entrydate from emp;
select * from emp;
```

查询所有员工的工作地址，起别名

```sh
select workaddress as '工作地址' from emp;
select workaddress '工作地址' from emp;
```

查询公司员工的上班地址（不要重复）

```sh
select distinct workaddress '工作地址' from emp;
```

#### 条件查询

查询年龄等于 88 的员工

```sh
select * from emp where age = 88;
```

查询年龄小于 20 的员工信息

```sh
select * from emp where age < 20;
```

查询年龄小于等于 20 的员工信息

```sh
select * from emp where age <= 20;
```

查询没有身份证号的员工信息

```sh
select * from emp where idcard is null;
```

查询有身份证号的员工信息

```sh
select * from emp where idcard is not null;
```

查询年龄不等于 88 的员工信息

```sh
select * from emp where age != 88;
select * from emp where age <> 88;
```

查询年龄在15岁（包含） 到20岁（包含）之间的员工信息（使用between时不能交换最大和最小值的顺序）

```sh
select * from emp where age >= 15 && age <= 20;
select * from emp where age >= 15 and age <= 20;
select * from emp where age between 15 and 20;
```

查询性别为 女 且年龄小于 25岁的员工信息

```sh
select * from emp where gender = '女' and age < 25;
```

查询年龄等于18 或 20 或 40 的员工信息

```sh
select * from emp where age = 18 or age = 20 or age = 40;
select * from emp where age in(18,20,40);
```

查询姓名为两个字的员工信息

```sh
select * from emp where name like '__';
```

查询身份证号最后一位是X的员工信息

```sh
select * from emp where idcard like '%X';
select * from emp where idcard like '_________________X';
```

### DCL

[返回](#基础知识)

## docker中的安装使用

获取指定版本的mysql镜像

```sh
docker pull mysql:8.0
```

创建docker容器，指定3306端口以及root密码1

```sh
docker run --name mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=1 -d mysql:8.0
```

A.进入容器-->容器中启动mysql客户端

```sh
docker exec -it mysql /bin/bash
mysql -u root -p
```

B.直接进入mysql客户端

```sh
docker exec -it mysql mysql -uroot -p
```

[B站黑马程序员]:https://www.bilibili.com/video/BV1Kr4y1i7ru?p=15&vd_source=9504fc54477a587558fbab1417ea6a08