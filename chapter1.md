传送门：[Laravel 安装指南 \| Laravel 5.5 中文文档](https://d.laravel-china.org/docs/5.5/installation)

### 1.1. 下载composer

```php
$ curl -sS https://getcomposer.org/installer | php
```

> 手动下载composer[：https://getcomposer.org/download/](https://getcomposer.org/download/)

### 1.2 将 composer 加入全局变量

当你下载了**composer.phar **后，将它放在全局目录，毕竟会频繁调用。

```php
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

### 1.3 安装 Laravel

首先，使用 Composer 下载 Laravel 安装程序：

```
$ composer global require "laravel/installer"
```

安装完成之后默认在$HOME目录下的~/.composer目录中

```
$ cd ~/.composer/vendor
$ ls

-rw-r--r--   1 lizhaohong  staff  178  2 25 23:59 autoload.php
drwxr-xr-x   3 lizhaohong  staff   96  2 25 23:59 bin
drwxr-xr-x  11 lizhaohong  staff  352  2 25 23:59 composer
drwxr-xr-x   5 lizhaohong  staff  160  2 25 23:59 guzzlehttp
drwxr-xr-x   3 lizhaohong  staff   96  2 25 23:59 laravel
drwxr-xr-x   3 lizhaohong  staff   96  2 25 23:59 psr
drwxr-xr-x   6 lizhaohong  staff  192  2 25 23:58 symfony
```

我们再将`$HOME/.composer/vendor/bin`目录放在你的环境变量 $PATH 中，以便系统可以找到`laravel`的可执行文件。

```
$ export PATH=$PATH:~/.composer/vendor/bin
```

### 1.4 创建一个laravel项目

我们将在桌面创建一个名为blog的laravel项目

```
$ cd ~/Desktop
$ laravel new blog

long time wait...
```

![](/assets/import.png)

1.5 运行laravel项目

我们进入blog目录，运行`$ php artisan serve`命令开启服务器

```php
$ cd ~/Desktop/blog
$ php artisan serve
Laravel development server started: <http://127.0.0.1:8000>
```

访问 [http://127.0.0.1:8000](http://127.0.0.1:8000)![](/assets/1import.png)

