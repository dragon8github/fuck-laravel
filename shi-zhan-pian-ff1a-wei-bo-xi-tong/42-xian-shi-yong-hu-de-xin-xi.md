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

## 添加路由

_routes/web.php_

```
Route::get('/users/{user}', 'UsersController@show')->name('users.show');
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



访问http://127.0.0.1:8000/users/1

![](/assets/14import.png)

