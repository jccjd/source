---
date: 2018-05-29
tags:
- Android
---

**什么是Sqlite**

- 小型的
- 可嵌入的
- 高效的
- 开源的
- 关系型数据库
- 程序驱动
- 无数据类型
- 跨平台
- 代码量少
- API简单易用
1. sqlite数据库数据类型
   - Integer varchar(10) float double char(10) text
2. 创建表的语句
    - create table person(_id Integer primary key,name varchar(10),age Integer not null)
3. 删除表的语句
    - drop table listname
    - drop table person
4. 插入数据
    - insert into listname[字段,字段] values(值1，值2....)
    - insert into person(_id age) values(1,20)
    - insert into person values(2,"zs",30)
5. 修改数据
    - delete from 表名 where 删除条件
    - delete from person where _id = 2
6. 查询语句
    - select 字段名 from where 查询条件 group by 分组的字段 having 筛选条件 order by 排序字段

    ```
    select * from person；

    select _id,name from person

    select * from person where _id = 1

    select * from person where _id=1 and age>18

    select * from person name like "%小%"

    select * from person where name like "_小%"


    select * from person where name is null


    select * from person where age between 10 and 20


    select * from person where age>18 oreder by _id

    ```
