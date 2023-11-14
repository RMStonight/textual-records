# mysql学习记录

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

## 基础知识

SQL分类

| 分类 | 全称 | 说明 |
| ---- | ---- | ---- |
| [DDL](#ddl) | Data Definition Language | 数据定义语言，用来定义数据库对象（数据库，表，字段） |
| [DML](#dml) | Data Manipulation Language | 数据操作语言，用来对数据库表中的数据进行增删改 |
| [DQL](#dql) | Data Query Language | 数据查询语言，用来查询数据库中表的记录 |
| [DCL](#dcl) | Data Control Language | 数据控制语言，用来创建数据库用户、控制数据库的访问权限 |

### DDL

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

### DCL
