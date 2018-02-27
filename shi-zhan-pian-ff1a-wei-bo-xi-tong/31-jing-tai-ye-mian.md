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

## Blade 模板

细心的你可能会留意到这三个文件的后缀名均为`.blade.php`，而不是`.php`。这是因为 Blade 是 Laravel 中提供的一套模板引擎，在 Blade 视图中我们可以使用 Laravel 为这套引擎定义的一些默认方法，并完全兼容 PHP 语法的书写。在项目运行时，Laravel 会把所有的 Blade 视图进行编译缓存成普通的 PHP 代码，因此你不必担心 Blade 会对应用产生负担。

## 使用通用视图

你可能已经注意到了，前面我们创建的几个视图里面包含着一些重复的代码，这明显违反了 DRY（Don't repeat yourself）原则，导致代码变得不够灵活、简洁。因此我们需要对页面进行重构，把多余的代码从视图中抽离出来，单独创建一个默认视图来进行存放通用代码。

我们给应用创建了一个 default 视图，并将其放在 `layouts` 文件夹中，default 视图将作为整个应用的基础视图。实际上你只要保证视图文件被放置在 `resources/views` 目录下即可，**Laravel 对视图的文件夹和文件命名并没有限制**，我将 default 文件放在 `layouts` 文件下，只是为了让应用的目录结构让人更好理解。

_resources/views/layouts/default.blade.php_

```php
<!DOCTYPE html>
<html>
  <head>
    <title>Sample App</title>
  </head>
  <body>
    @yield('content')
  </body>
</html>
```

下面的这行代码表示该占位区域将用于显示 content 区块的内容，而 content 区块的内容将由继承自 default 视图的子视图定义。

```
@yield('content')
```

Laravel 的 Blade 模板支持继承，这意味多个子视图可以共用父视图提供的视图模板。接下来让我们修改之前创建的首页视图文件，来学习下如何使用 Blade 模板的继承。

_resources/views/static\_pages/home.blade.php_

```
@extends('layouts.default')
@section('content')
  <h1>主页</h1>
@stop
```

接下来让我们对其它两个视图也进行更改，统一使用父视图的代码。

修改完成之后，再次在网页上访问这几个静态页面，你会发现父视图的代码已被成功嵌入到子视图中。

现在还有一点不足的地方，就是所有的网站标题名字都为 Sample，这可太没个性了。因此我们接下来要做的就是针对页面标题进行优化，让不同页面显示不同的标题。

首先我们要修改默认视图文件，在代码显示标题的位置嵌入 @yield 区块：

_resources/views/layouts/default.blade.php_

```php
<!DOCTYPE html>
<html>
  <head>
    <title>@yield('title', 'Sample')</title>
  </head>
  <body>
    @yield('content')
  </body>
</html>
```

我们给 @yield 传了两个参数，第一个参数是该区块的变量名称，第二个参数是默认值，表示当指定变量的值为空值时，使用 Sample 来作为默认值。

```
<title>@yield('title', 'Sample')</title>
```

下面让我们来为帮助页和关于页加上指定标题。

_resources/views/static\_pages/help.blade.php_

```
@extends('layouts.default')
@section('title', '帮助')

@section('content')
  <h1>帮助页</h1>
@stop
```

resources/views/static\_pages/about.blade.php

```
@extends('layouts.default')
@section('title', '关于')

@section('content')
  <h1>关于页</h1>
@stop
```



