## 注册路由

_outes/web.php_

```php
<?php
Route::get('/', 'StaticPagesController@home')->name('home');
Route::get('/help', 'StaticPagesController@help')->name('help');
Route::get('/about', 'StaticPagesController@about')->name('about');


Route::get('signup', 'UsersController@create')->name('signup');
```

## 生成用户控制器

现在我们还没有用户控制器，让我们运行下面命令来生成。

```
$ php artisan make:controller UsersController
```

以上命令会生成`app/Http/Controllers/UsersController.php`文件。

_app/Http/Controllers/UsersController.php_

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use App\Http\Requests;

class UsersController extends Controller
{
    public function create()
    {
        return view('users.create');
    }
}
```

## 注册页面视图

接下来让我们来添加一个简单的注册视图，后面再为该视图加上表单，让用户可以提交自己的个人信息。

_resources/views/users/create.blade.php_

```py
@extends('layouts.default')
@section('title', '注册')

@section('content')
<h1>注册</h1>
@stop
```

最后我们让我们修改首页注册按钮的链接，提供给用户一个进入注册页面的入口。

_resources/views/static\_pages/home.blade.php_

```php
@extends('layouts.default')

@section('content')
  <div class="jumbotron">
	    <h1 class="display-4">Hello, world!</h1>
	    <p class="lead">This is a simple hero unit, a simple jumbotron-style component for calling extra attention to featured content or information.</p>
	    <hr class="my-4">
	    <p>It uses utility classes for typography and spacing to space content out within the larger container.</p>
	    <p class="lead">
	      <a class="btn btn-primary btn-lg" href="{{ route('signup') }}" role="button">Learn more</a>
	    </p>
  </div>
@stop
```

保存后刷新首页看看吧。试试看点击按钮是否会跳转到`signup`页面呢？

![](/assets/6import.png)

