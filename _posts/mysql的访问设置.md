---
date: 2019-11-04
tags:
- mysql
---

Docs

-----------

### 远程连接mysql

> 本意是为了将MySQL放到ECS服务器，本地不用开mysql服务了，好处呢
>
> - 如果本机关机不用每次都重开启服务
> - 数据能有一个备份
> - 可以缓解本机的内存压力



### 开启服务器权限：

不管是阿里云，还是腾讯云他们的端口都没有默认开放`3306`端口，需要手动开启

### 设置mysql的配置文件

```bash
cd /etc/mysql/mysql.conf.d
vi mysql.conf -- #bind-address =127.0.0.1
systemctl restart mysql
```

### 更改库字段

```mysql
mysql -u root -p
use mysql;
select user, host from user;
update user set host='%' where user='root'
flush privileges;
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'yourpwd' WITH GRANT OPTION;
```
