## 配置路由

当用户在查看一个网页时，一个完整的访问过程如下：

1. 打开浏览器在地址栏输入 URL 并访问；
2. 路由将 URL 请求映射到指定控制器上；
3. 控制器收到请求，开始进行处理。如果视图需要动态数据进行渲染，则控制器会开始从模型中读取数据；
4. 数据读取完毕，将数据传送给视图进行渲染；
5. 视图渲染完成，在浏览器上呈现出完整页面；

如下图：

[![](https://fsdhubcdn.phphub.org/uploads/images/201705/13/1/VptHggpp0v.png "file")](https://fsdhubcdn.phphub.org/uploads/images/201705/13/1/VptHggpp0v.png)

> 开发页面时，最开始最重要的事情就是处理好网页路由关系

routes/web.php

```
<?php

Route::get('/', 'StaticPagesController@home');
Route::get('/help', 'StaticPagesController@help');
Route::get('/about', 'StaticPagesController@about');
```



