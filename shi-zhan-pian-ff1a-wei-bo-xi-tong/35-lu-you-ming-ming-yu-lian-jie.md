### 使用命名路由

```py
<li><a href="/help">帮助</a></li>
```

上面的代码链接形式是 Web 开发中较为常用的一种，但在 Laravel 中，我们可以这么写：

```py
<li><a href="{{ route('help') }}">帮助</a></li>
```

如果要使用下面这种方式来渲染 help 链接，则需要先为路由定义 help 路由名称。

```php
Route::get('/help', 'StaticPagesController@help')->name('help');
```

让我们开始动手，命名之前创建的几个路由。

_routes/web.php_

```php
<?php

Route::get('/', 'StaticPagesController@home')->name('home');
Route::get('/help', 'StaticPagesController@help')->name('help');
Route::get('/about', 'StaticPagesController@about')->name('about');
```

_resources/views/layouts/\_header.blade.php_

```py
<nav class="navbar fixed-top navbar-expand-lg navbar-dark bg-dark">
	<div class="container">
	    <a class="navbar-brand" href="#">Laravel App</a>
	    <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarColor01" aria-controls="navbarColor01" aria-expanded="false" aria-label="Toggle navigation">
	      <span class="navbar-toggler-icon"></span>
	    </button>
	    <div class="collapse navbar-collapse" id="navbarColor01">
	      <ul class="navbar-nav mr-auto">
	        <li class="nav-item active">
	          <a class="nav-link" href="{{ route('home') }}">Home</a>
	        </li>
	        <li class="nav-item">
	          <a class="nav-link" href="{{ route('help') }}">Help</a>
	        </li>
	        <li class="nav-item">
	          <a class="nav-link" href="{{ route('about') }}">About</a>
	        </li>
	      </ul>
	      <form class="form-inline">
	        <input class="form-control mr-sm-2" type="search" placeholder="Search" aria-label="Search">
	        <button class="btn btn-outline-info my-2 my-sm-0" type="submit">Search</button>
	      </form>
	    </div>
	</div>
</nav>
```



