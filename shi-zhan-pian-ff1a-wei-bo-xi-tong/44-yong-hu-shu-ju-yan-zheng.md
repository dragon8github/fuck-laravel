## 用户数据验证

如果你现在填写注册表单并进行提交，则会出现报错，因为表单还不能真正使用。我们还需要在用户控制器中添加一个用于处理表单数据提交后的`store`方法，用于处理用户创建的相关逻辑。

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

    public function store(Request $request)
    {
        $this->validate($request, [
            'name' => 'required|max:50',
            'email' => 'required|email|unique:users|max:255',
            'password' => 'required|confirmed|min:6'
        ]);
        return;
    }
}
```

## 表单提交 与 csrf\_field\(\) 方法

在我们为注册表单添加上验证规则之后，尝试点击注册会发现『页面过期』的报错异常：

[![](https://fsdhubcdn.phphub.org/uploads/images/201708/02/1/rQ20f2xK9w.png "file")  
](https://fsdhubcdn.phphub.org/uploads/images/201708/02/1/rQ20f2xK9w.png)出现该报错的原因是，在我们使用 POST 方法提交表单时，Laravel 为了安全考虑，会让我们提供一个 token（令牌）来防止我们的应用受到 CSRF（跨站请求伪造）的攻击。修复该异常的方法很简单，我们只需要在表单元素中添加 Blade 模板为我们提供的 csrf\_field 方法即可。该方法在 Blade 模板中调用如下：

```html
{{ csrf_field() }}
```

上面这段代码转换为 HTML 如下所示：

```html
<input type="hidden" name="_token" value="fhcxqT67dNowMoWsAHGGPJOAWJn8x5R5ctSwZrAq">
```

由于输入框为 hidden 类型，因此该 input 元素在页面上是不可见的。现在让我们为注册表单添加`csrf_field`方法。  
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
      	  {{ csrf_field() }}
      	  
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



