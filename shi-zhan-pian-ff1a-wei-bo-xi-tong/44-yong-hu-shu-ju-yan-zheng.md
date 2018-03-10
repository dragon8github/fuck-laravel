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



