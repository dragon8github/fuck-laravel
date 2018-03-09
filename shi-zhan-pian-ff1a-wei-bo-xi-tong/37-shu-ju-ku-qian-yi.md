传送门：[Laravel 的数据库迁移 Migrations](http://d.laravel-china.org/docs/5.5/migrations)

## 简介

**数据库迁移就像是数据库的版本控制**，可以让你的团队轻松修改并共享应用程序的数据库结构。

如果你曾经试过让同事手动在数据库结构中添加字段，那么数据库迁移可以让你不再需要做这样的事情。不仅如此，

Migration 建表要比直接手动创建表或者`.sql`文件具备额外的管理数据库的功能，如回滚、重置、更新等。Migration 的建表方法大部分情况下能兼容 MySQL, PostgreSQL, SQLite 甚至是 Oracle 等主流数据库系统。

## 默认迁移文件

所有创建的迁移文件都被统一放在`database/migrations`文件夹里。打开该文件夹我们可以看到，Laravel 已默认为我们创建好了两个迁移文件：

* database/migrations/2014\_10\_12\_000000\_create\_users\_table.php
* database/migrations/2014\_10\_12\_100000\_create\_password\_resets\_table.php

Laravel 默认创建的两个迁移文件，一个用于构建用户表，一个用于构建密码重置表。

本章我们先来看下 Laravel 为我们生成的创建用户迁移文件里面都包含了什么内容。

_database/migrations/2014\_10\_12\_000000\_create\_users\_table.php_

```php
<?php

use Illuminate\Support\Facades\Schema;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Database\Migrations\Migration;

class CreateUsersTable extends Migration
{
    /**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        Schema::create('users', function (Blueprint $table) {
            $table->increments('id');
            $table->string('name');
            $table->string('email')->unique();
            $table->string('password');
            $table->rememberToken();
            $table->timestamps();
        });
    }

    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
        Schema::dropIfExists('users');
    }
}
```

可以看到在该文件里面定义了一个`CreateUsersTable`类，并继承自`Migration`基类。CreateUsersTable 有两个方法`up`和`down`：

* 当我们运行迁移时，`up`方法会被调用；
* 当我们回滚迁移时，`down`方法会被调用。

## 创建数据库表

在`up`方法里面，我们通过调用`Schema`类的`create`方法来创建`users`表：

```php
Schema::create('users', function (Blueprint $table) {
    ...
});
```

`create`方法会接收两个参数：一个是数据表的名称，另一个则是接收`$table`（Blueprint 实例）的闭包。

## 定义数据表字段

接下来让我们来详细讲解 Blueprint 实例`$table`的基本用法：

```php
// 由 increments 方法创建了一个 integer 类型的自增长 id。
$table->increments('id');

// 由 string 方法创建了一个 name 字段，用于保存用户名称。
$table->string('name');

// 由 string 方法创建了一个 email 字段，且在最后指定该字段的值为唯一值，用于保存用户邮箱。
$table->string('email')->unique();

// 由 string 方法创建了一个 password 字段，且在 string 方法中指定保存的值最大长度为 60，用于保存用户密码。
$table->string('password', 60);

// 由 rememberToken 方法为用户创建一个 remember_token 字段，用于保存『记住我』的相关信息。
$table->rememberToken();

// 由 timestamps 方法创建了一个 created_at 和一个 updated_at 字段，分别用于保存用户的创建时间和更新时间。
$table->timestamps();
```

若要了解更多 $table 的可用方法，可查阅[官方文档](http://d.laravel-china.org/docs/5.5/migrations#creating-tables)。

## 数据库迁移

第一步：确保你的环境开启了数据库服务并且正常，本节以mysql为例。环境为mac ox，数据库管理工具为：[Sequel Pro](https://pan.baidu.com/s/1slWENqH)

参考 [《第零章：环境安装 - Mac OS 安装MySql》](https://dragon8github.gitbooks.io/fuck-laravel/content/mac-os-an-zhuang-mysql.html)

第二步：在项目 /config/database.php 中配置好你的数据库参数。

```php
'mysql' => [
            'driver' => 'mysql',
            'host' => env('DB_HOST', '127.0.0.1'),
            'port' => env('DB_PORT', '3306'),
            'database' => env('DB_DATABASE', 'sample'),
            'username' => env('DB_USERNAME', 'root'),
            'password' => env('DB_PASSWORD', '202063'),
            'unix_socket' => env('DB_SOCKET', ''),
            'charset' => 'utf8mb4',
            'collation' => 'utf8mb4_unicode_ci',
            'prefix' => '',
            'strict' => true,
            'engine' => null,
]
```

第三步：手动创建一个名为sample的数据库

第四步：执行 `$ php artisan migrate`

![](/assets/12import.png)

