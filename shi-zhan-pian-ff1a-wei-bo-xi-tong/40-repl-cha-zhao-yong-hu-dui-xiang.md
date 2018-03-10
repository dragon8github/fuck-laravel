我们使用`use`来引用`App\Models\User`Eloquent 模型类：

```
>>> use App\Models\User
```

查找一个 id 为 1 的用户

```
>>> User::find(1)
```

你传给 find 方法的 id 不存在时，Tinker 将会返回 null：

```
>>> User::find(5)
=> null
```

如果你想在查询用户不存在时触发报错的话，可使用 findOrFail：

```
>>> User::findOrFail(5)
Illuminate\Database\Eloquent\ModelNotFoundException with message 'No query results for model [App\Models\User] 5'
```

如果要查找用户表中的首个用户，可以使用 first 方法：

```
>>> User::first()
```

我们还可以用 all 方法取出所有的用户数据：

```
>>> User::all()
```



