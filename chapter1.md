传送门：[Mac下homebrew安装及php.mysql.nginx环境安装及配置](http://blog.qiji.tech/archives/132)

###  1.1. 下载composer

```
$ curl -sS https://getcomposer.org/installer | php
```

手动下载composer[：https://getcomposer.org/download/](https://getcomposer.org/download/)



### 1.2 将 composer 加入全局变量

当你下载了**composer.phar **后，默认放在家目录中，可以将它放在全局目录中，但每次当你建立新目录时，你必須再复制一个副本到新目录中，这样比较麻烦。所以最佳做法是将它放到 usr/local/bin 目录中中，成为全域指令。

```
$ echo $PATH
/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin

$ cd ~/
$ ls 
drwx------@  3 lizhaohong  staff       96  2 11 19:01 Applications
drwx------+  6 lizhaohong  staff      192  2 25 23:19 Desktop
drwx------+  4 lizhaohong  staff      128  2 22 18:24 Documents
drwx------+ 10 lizhaohong  staff      320  2 25 23:14 Downloads
drwx------@ 65 lizhaohong  staff     2080  2 25 07:49 Library
drwx------+  3 lizhaohong  staff       96  1 16 15:00 Movies
drwx------+  3 lizhaohong  staff       96  1 16 15:00 Music
drwx------+  3 lizhaohong  staff       96  1 16 15:00 Pictures
drwxr-xr-x+  4 lizhaohong  staff      128  1 16 15:00 Public
-rwxr-xr-x@  1 lizhaohong  staff  1861877  2 25 23:18 composer.phar

$ mv composer.phar /usr/local/bin/composer
$ composer
```

当看到composer信息的时候，说明安装成功了！

