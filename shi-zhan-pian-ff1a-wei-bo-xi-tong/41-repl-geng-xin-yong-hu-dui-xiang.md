有两种方式可以完成用户的更新操作：

* 第一种是通过给用户对象属性进行赋值，赋值成功后再调用 `save` 方法进行保存更新；
* 第二种则是直接调用 `update` 方法进行更新。

## 通过 save 方法更新

```
>>> $user->name = 'Summer'
>>> $user->save()
```

## 通过 update 方法更新

```
>>> $user->update(['name'=>'Aufree'])
```



