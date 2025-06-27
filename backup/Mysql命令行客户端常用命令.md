# Mysql命令行客户端常用命令

## 注意点

下面展示的 `database_name`、`table_name`、`column1`、`column2`、`value1`、`value2` 和 `datatype`在自己用的时候需要替换为实际的值

在敲命令的时候要注意，一定要在末尾加上分号

## 操作

安装好Mysql之后，搜索找到以下应用

![image-20240519223119791](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270901949.png)

打开之后即可进入以下界面，并输入好设定的密码，之后即可开始操作

![image-20240519223230509](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270901502.png)

显示所有的数据库：

```
SHOW DATABASES;
```

创建一个新的数据库，名为 `database_name`：

```
CREATE DATABASE database_name;
```

删除名为 `database_name` 的数据库：

```
DROP DATABASE database_name;
```

选择当前会话要操作的数据库：

```
USE database_name;
```

列出当前选择的数据库中的所有表：

```
SHOW TABLES;
```

显示 `table_name` 表的结构信息：

```
DESCRIBE table_name;
```

向 `table_name` 表中插入一行数据，指定列名和对应的值：

```
INSERT INTO table_name (column1, column2, ...) VALUES (value1, value2, ...);
```

从 `table_name` 表中查询数据，根据条件筛选：

```
SELECT * FROM table_name WHERE condition;
```

更新 `table_name` 表中满足条件的数据：

```
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```

从 `table_name` 表中删除满足条件的数据：

```
DELETE FROM table_name WHERE condition;
```

在数据库中创建一张名为 `table_name` 的新表，定义列名和数据类型：

```
CREATE TABLE table_name (column1 datatype, column2 datatype, ...);
```

删除名为 `table_name` 的表：

```
DROP TABLE table_name;
```

显示当前连接到 MySQL 服务器的用户：

```
SELECT USER();
```

退出 MySQL 命令行客户端：

```
EXIT;
```

退出 MySQL 命令行客户端：

```
QUIT;
```

