Artisan 是 Laravel 提供的 CLI（命令行接口），它提供了非常多实用的命令来帮助我们开发 Laravel 应用。前面我们已使用过 Artisan 命令来生成应用的 App Key 和控制器。在本教程中，我们会用到以下 Artisan 命令，你也可以使用 `php artisan list` 来查看所有可用的 Artisan 命令。\|

| 命令 | 说明 |
| :--- | :--- |
| php artisan key:generate | 生成 App Key |
| php artisan make:controller | 生成控制器 |
| php artisan make:model | 生成模型 |
| php artisan make:policy | 生成授权策略 |
| php artisan make:seeder | 生成 Seeder 文件 |
| php artisan migrate | 执行迁移 |
| php artisan migrate:rollback | 回滚迁移 |
| php artisan migrate:refresh | 重置数据库 |
| php artisan db:seed | 填充数据库 |
| php artisan tinker | 进入 tinker 环境 |
| php artisan route:list | 查看路由列表 |

后面我们会再对上面每个 Artisan 命令进行具体应用，你也可以使用 help 来查看各个 Artisan 命令的帮助界面，如：

```
$ php artisan help migrate
```



