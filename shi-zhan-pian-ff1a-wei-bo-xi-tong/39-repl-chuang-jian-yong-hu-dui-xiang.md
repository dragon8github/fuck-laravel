接下来让我们尝试使用 Eloquent 模型来创建一个用户对象，并将该用户对象存储到数据库。虽然我们现在还没有用户注册表单，但是通过 Laravel 提供的 Tinker 环境可以让我们完成对用户对象创建。Tinker 是一个 REPL \(read-eval-print-loop\)，REPL 指的是一个简单的、可交互式的编程环境，通过执行用户输入的命令，并将执行结果直接打印到命令行界面上来完成整个操作。REPL 对于学习一门新的编程语言具有很大的帮助，因为它能立刻对初学者做出的动作进行响应。接下来我们将使用 Tinker 来操作用户对象。

  
首先让我们使用此命令进入 Tinker 环境：

```
$ php artisan tinker
```

通过下面命令我们可以很轻松的创建一个用户对象：

```
>>> App\Models\User::create(['name'=> 'Aufree', 'email'=>'aufree@yousails.com','password'=>bcrypt('password')])
```

在以上命令中，我们使用`App\Models\User`Eloquent 模型提供的`create`方法，通过传入一个关联数组来新建一个用户对象。在我们对用户的`password`进行赋值时，调用了一个叫`bcrypt`的方法，将`password`的值进行加密。这是因为所有保存到数据库的用户密码在经过加密保存后安全性更高，这样当我们的数据库不幸被黑客脱库时，泄露出去的用户密码也都是有经过加密处理的。在读取用户密码的时候，Laravel 会先对密码进行解密再返回，这块的具体操作逻辑我们不必太担心，因为 Laravel 已为我们做好了一切防范措施。

