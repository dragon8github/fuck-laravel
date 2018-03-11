_app/Http/Controllers/UsersController.php_

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use App\Http\Requests;
use App\Models\User;

class UsersController extends Controller
{
    public function create()
    {
        return view('users.create');
    }

    public function show(User $user)
    {
        return view('users.show', compact('user'));
    }
}
```

注意引入命名空间 `use App\Models\User;`

我们将用户对象`$user`通过[`compact`](http://php.net/manual/zh/function.compact.php)方法转化为一个关联数组，并作为第二个参数传递给`view`方法，将数据与视图进行绑定。

`show`方法添加完成之后，我们便能在视图中使用`user`变量来访问通过`view`方法传递给视图的用户数据。

## resource 路由

Laravel 遵从 RESTful 架构的设计原则，将数据看做一个资源，由 URI 来指定资源。对资源进行的获取、创建、修改和删除操作，分别对应 HTTP 协议提供的 GET、POST、PATCH 和 DELETE 方法。当我们要查看一个 id 为 1 的用户时，需要向`/users/1`地址发送一个 GET 请求，当 Laravel 的路由接收到该请求时，默认会把该请求传给控制器的`show`方法进行处理。

Laravel 为我们提供了`resource`方法来定义用户资源路由。

_routes/web.php_

```php
<?php
Route::get('/', 'StaticPagesController@home')->name('home');
Route::get('/help', 'StaticPagesController@help')->name('help');
Route::get('/about', 'StaticPagesController@about')->name('about');
Route::get('/signup', 'UsersController@create')->name('signup');
Route::resource('users', 'UsersController');
```

新增的 resource 方法将遵从 RESTful 架构为用户资源生成路由。该方法接收两个参数，第一个参数为资源名称，第二个参数为控制器名称。

```php
Route::resource('users', 'UsersController');
```

上面代码将等同于：

```php
Route::get('/users', 'UsersController@index')->name('users.index');

Route::get('/users/{user}', 'UsersController@show')->name('users.show');

Route::get('/users/create', 'UsersController@create')->name('users.create');

Route::post('/users', 'UsersController@store')->name('users.store');

Route::get('/users/{user}/edit', 'UsersController@edit')->name('users.edit');

Route::patch('/users/{user}', 'UsersController@update')->name('users.update');

Route::delete('/users/{user}', 'UsersController@destroy')->name('users.destroy');
```

## Gravatar 头像

现在，我们要为用户的个人页面添加头像显示的功能。接下来的项目开发将使用[Gravatar](https://en.gravatar.com/)来为用户提供个人头像支持。Gravatar 为 “全球通用头像”，当你在 Gravatar 的服务器上放置了自己的头像后，可通过将自己的 Gravatar 登录邮箱进行 MD5 转码，并与 Gravatar 的 URL 进行拼接来获取到自己的 Gravatar 头像。

接下来让我们在用户模型中定义一个`gravatar`方法，用来生成用户的头像。

_app/Models/User.php_

```php
public function gravatar($size = '100') {
    $hash = md5(strtolower(trim($this->attributes['email'])));
    return "http://www.gravatar.com/avatar/$hash?s=$size";
}
```

接下来让我们来构建一个全局通用的局部视图，用于展示用户的头像和用户名等基本信息。

_resources/views/layouts/\_user\_info.blade.php_

```html
<a href="{{ route('users.show', $user->id) }}">
  <img src="{{ $user->gravatar('140') }}" alt="{{ $user->name }}" class="gravatar"/>
</a>
<h1>{{ $user->name }}</h1>
```

_resources/views/users/show.blade.php_

```html
@extends('layouts.default')
@section('title', $user->name)
@section('content')
<div class="row">
  <div class="col-md-offset-2 col-md-8">
    <div class="col-md-12">
      <div class="col-md-offset-2 col-md-8">
        <section class="user_info">
          @include('shared._user_info', ['user' => $user])
        </section>
      </div>
    </div>
  </div>
</div>
@stop
```

访问[http://127.0.0.1:8000/users/1](http://127.0.0.1:8000/users/1)，并且满足路由 + 控制器两个条件时，Laravel 将会自动查找 ID 为 1 的用户并赋值到变量

`$user`中，如果数据库中找不到对应的模型实例，会自动生成 HTTP 404 响应。

![](/assets/14import.png)

