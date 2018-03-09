Laravel 默认为我们生成了用户模型文件，代码如下所示：

_app/User.php_

```php
<?php

namespace App;

use Illuminate\Notifications\Notifiable;
use Illuminate\Foundation\Auth\User as Authenticatable;

class User extends Authenticatable
{
    use Notifiable;

    /**
     * The attributes that are mass assignable.
     *
     * @var array
     */
    protected $fillable = [
        'name', 'email', 'password',
    ];

    /**
     * The attributes that should be hidden for arrays.
     *
     * @var array
     */
    protected $hidden = [
        'password', 'remember_token',
    ];
}
```

我们主要将精力放在用户模型中定义的三个属性`table`,`fillable`,`hidden`上。

## 使用`App\Models`命名空间

aravel 为我们默认创建的模型文件放置在`app`文件夹下，为了让新手能够更好理解 MVC 模式的开发流程，本教程中将统一使用

`app/Models`文件夹来放置所有的模型文件。现在让我们先来创建一个`app/Models`文件夹，并将`User.php`文件放置到其中。

```bash
$ mkdir app/Models
$ mv app/User.php app/Models/User.php
```

1、修改 User.php 文件，更改 namespace 为我们新创建的文件夹路径：

```
<?php

namespace App\Models;
```

2、编辑器全局搜索`App\User`替换为`App\Models\User`，在 Sublime Text 中可使用快捷键`shift + cmd(ctrl) + f`来进行全局搜索替换的操作。完成之后，点击右下角的`Replace All`按钮。默认大概是 4 处修改地方。

## 命令创建一个模型文件

```
$ php artisan make:model Article
```

默认是生成在 /app/Article.php 中。我们需要制定命名空间到/app/Models中

```
$ rm app/Article.php
$ php artisan make:model Models/Article
```

![](/assets/13import.png)

### 创建迁移文件

我们尝试删除模型并且使用`--migration`或`-m`选项，让我们将刚刚生成的模型进行删除，尝试生成迁移文件：

```bash
$ rm app/Models/Article.php
$ php artisan make:model Models/Article -m
Model created successfully.
Created Migration: 2016_09_10_023235_create_articles_table
```

可看到模型文件和迁移文件都一并生成了。

### Eloquent 表命名约定

在该文件中，Eloquent Article 模型默认情况下会使用类的「下划线命名法」与「复数形式名称」来作为数据表的名称生成规则。如：

* Article 数据模型类对应`articles`表；
* User 数据模型类对应`users`表；
* BlogPost 数据模型类对应`blog_posts`表；

因此 Eloquent 将会假设 Article 模型被存储记录在 articles 数据表中。如果你需要指定自己的数据表，则可以通过`table`属性来定义，如：

```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Model;

class Article extends Model
{
    protected $table = 'my_articles';
}
```

### 『约定优于配置』解释

『约定优于配置』（convention over configuration），也称作按约定编程，这是一种软件设计范式，旨在减少软件开发人员需做决定的数量，获得简单的好处，而又不失灵活性。如果所用工具的约定与你的期待相符，便可省去配置；反之，你可以配置来达到你所期待的方式。

Eloquent 数据表命名约定机制即属于『约定优于配置』，数据模型类`Article`按照系统约定对应于`articles`数据表，如果我们因为特殊原因需要使用其他表名称，只需要通过配置`$table`即可达到预期。

『约定优于配置』能极大提高开发效率，并且也更有利于团队协作。Laravel 项目中大量的使用了『约定优于配置』这种设计范式，这也是 Laravel 的另一个可爱之处。

