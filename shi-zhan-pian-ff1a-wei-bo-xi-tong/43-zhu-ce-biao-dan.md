首先我们需要把之前在 Tinker 中创建的所有用户数据进行删除，将数据库重置。重置的方法很简单，只需借助`migrate:refresh`命令，即可完成数据库的重置操作。

```
$ php artisan migrate:refresh
```

`refresh`的作用是重置数据库并重新运行所有迁移。

## 表单构建

_resources/views/users/create.blade.php_

```html
@extends('layouts.default')
@section('title', '注册')

@section('content')
<div class="col-md-offset-2 col-md-8">
  <div class="panel panel-default">
    <div class="panel-heading">
      <h5>注册</h5>
    </div>
    <div class="panel-body">
      <form method="POST" action="{{ route('users.store') }}">
          <div class="form-group">
            <label for="name">名称：</label>
            <input type="text" name="name" class="form-control" value="{{ old('name') }}">
          </div>

          <div class="form-group">
            <label for="email">邮箱：</label>
            <input type="text" name="email" class="form-control" value="{{ old('email') }}">
          </div>

          <div class="form-group">
            <label for="password">密码：</label>
            <input type="password" name="password" class="form-control" value="{{ old('password') }}">
          </div>

          <div class="form-group">
            <label for="password_confirmation">确认密码：</label>
            <input type="password" name="password_confirmation" class="form-control" value="{{ old('password_confirmation') }}">
          </div>

          <button type="submit" class="btn btn-primary">注册</button>
      </form>
    </div>
  </div>
</div>
@stop
```

## 路由配置

_routes/web.php_

```php
<?php
Route::get('/', 'StaticPagesController@home')->name('home');
Route::get('/help', 'StaticPagesController@help')->name('help');
Route::get('/about', 'StaticPagesController@about')->name('about');
Route::get('/signup', 'UsersController@create')->name('signup');
Route::resource('users', 'UsersController');
```

请注意 `<form method="POST" action="{{ route('users.store') }}">`，这里本需要设置一个名为`users.store`的路由。

```php
Route::get('/users/store', 'UsersController@store')->name('users.store');
```

但由于`Route::resource('users', 'UsersController')`而省略了

