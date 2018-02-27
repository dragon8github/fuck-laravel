## 配置路由

当用户在查看一个网页时，一个完整的访问过程如下：

1. 打开浏览器在地址栏输入 URL 并访问；
2. 路由将 URL 请求映射到指定控制器上；
3. 控制器收到请求，开始进行处理。如果视图需要动态数据进行渲染，则控制器会开始从模型中读取数据；
4. 数据读取完毕，将数据传送给视图进行渲染；
5. 视图渲染完成，在浏览器上呈现出完整页面；

如下图：

[![](https://fsdhubcdn.phphub.org/uploads/images/201705/13/1/VptHggpp0v.png "file")](https://fsdhubcdn.phphub.org/uploads/images/201705/13/1/VptHggpp0v.png)

> 开发页面时，最开始最重要的事情就是处理好网页路由的关系

routes/web.php

```php
<?php

Route::get('/', 'StaticPagesController@home');
Route::get('/help', 'StaticPagesController@help');
Route::get('/about', 'StaticPagesController@about');
```

## 生成静态页面控制器

Laravel 的控制器命名规范统一使用 驼峰式大小写 和复数形式来命名，在这里我们也应该这么做。一般情况下，我们会使用下面命令来生成静态页面控制器：

```php
$ php artisan make:controller StaticPagesController
```

让我们来看下`StaticPagesController`文件生成的默认代码：

_app/Http/Controllers/StaticPagesController.php_

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;

class StaticPagesControlle extends Controller
{
    //
}
```

现在的静态页面控制器中还没有指定好三个页面对应的动作，让我们来为控制器加上这三个动作来处理从路由发过来的请求：

_app/Http/Controllers/StaticPagesController.php_

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;

class StaticPagesController extends Controller
{
    public function home()
    {
        return '主页';
    }

    public function help()
    {
        return '帮助页';
    }

    public function about()
    {
        return '关于页';
    }
}
```

## 添加静态页面视图

要在控制器中指定渲染某个视图，则需要使用到`view`方法，`view`方法接收两个参数，第一个参数是视图的路径名称，第二个参数是与视图绑定的数据，第二个参数为可选参数。

_app/Http/Controllers/StaticPagesController.php_

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;

class StaticPagesController extends Controller
{
    public function home()
    {
        return view('static_pages/home');
    }

    public function help()
    {
        return view('static_pages/help');
    }

    public function about()
    {
        return view('static_pages/about');
    }
}
```

下面这行代码，将会渲染在`resources/views/static_pages/home.blade.php`文件。

默认情况下，所有的视图文件都存放在`resources/views`文件夹下。

```js
return view('static_pages/home');
```

在控制器中指定渲染的视图之后，接下来便是对视图进行构建了，我们需要在`resources/views`中新增下面三个视图。

resources/views/static\_pages/home.blade.php

```php
<!DOCTYPE html>
<html>
<head>
  <title>Sample App</title>
</head>
<body>
  <h1>主页</h1>
</body>
</html>
```

resources/views/static\_pages/help.blade.php

```php
<!DOCTYPE html>
<html>
<head>
  <title>Sample App</title>
</head>
<body>
  <h1>帮助页</h1>
</body>
</html>
```

resources/views/static\_pages/about.blade.php

```php
<!DOCTYPE html>
<html>
<head>
  <title>Sample App</title>
</head>
<body>
  <h1>关于页</h1>
</body>
</html>
```



