# mysql学习记录

## docker中的安装使用

获取指定版本的mysql镜像

```sh
docker pull mysql:8.0.33
```

创建docker容器，指定3306端口以及root密码1

```sh
docker run --name mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=1 -d mysql:8.0.33
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
| DDL | Data Definition Language | 数据定义语言，用来定义数据库对象（数据库，表，字段） |
| DML | Data Manipulation Language | 数据操作语言，用来对数据库表中的数据进行增删改 |
| DQL | Data Query Language | 数据查询语言，用来查询数据库中表的记录 |
| DCL | Data Control Language | 数据控制语言，用来创建数据库用户、控制数据库的访问权限 |
