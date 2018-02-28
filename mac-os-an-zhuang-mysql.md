传送门：[Mac下安装与配置MySQL](https://www.jianshu.com/p/a8e4068a7a8)

### 一、下载mysql

进入官方下载地址：[https://www.mysql.com/downloads/](https://www.mysql.com/downloads/)

1、找到 MySQL Community Edition\(GPL\)

2、找到 [MySQL Community Server](https://dev.mysql.com/downloads/mysql/)\(GPL\)

3、找到 Select Operating System  选择Mac OS

4、好到 DMG 版本 下载

5、 No thanks, just start my download.

### 二、安装

![](/assets/9import.png)

### 三、开启Mysql 服务

### ![](/assets/11import.png)![](/assets/10import.png)

### 四、配置Mysql 到全局变量中

1、加入全局变量：[http://www.cnblogs.com/CyLee/p/8486190.html](http://www.cnblogs.com/CyLee/p/8486190.html)

```
$ export PATH=/usr/local/mysql/bin/:$PATH
```

### 五、 配置Mysql 的密码

1、关闭 mysql 服务

2、更改安全级别

```
$ cd /usr/local/mysql/bin/
$ sudo ./mysqld_safe --skip-grant-tables
```

3、新建一个终端，由于我们已经更改了安全级别，现在可以直接不需要密码登录了。

```py
$ mysql -u root

mysql> FLUSH PRIVILEGES;
Query OK, 0 rows affected (0.00 sec)

mysql> ALTER USER 'root'@'localhost' IDENTIFIED by '你的新密码';
Query OK, 0 rows affected (0.01 sec)

mysql> exit
Bye
```



