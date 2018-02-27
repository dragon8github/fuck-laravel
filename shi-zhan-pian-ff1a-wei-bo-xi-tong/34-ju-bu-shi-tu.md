我们需要把顶部导航从 default 视图中分离出来，成为一个单独的头部视图和底部视图

## 头部和底部视图

首先，我们需要新建一个头部视图文件。

_resources/views/layouts/\_header.blade.php_

```php
<nav class="navbar fixed-top navbar-expand-lg navbar-dark bg-dark">
	<div class="container">
	    <a class="navbar-brand" href="#">Laravel App</a>
	    <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarColor01" aria-controls="navbarColor01" aria-expanded="false" aria-label="Toggle navigation">
	      <span class="navbar-toggler-icon"></span>
	    </button>
	    <div class="collapse navbar-collapse" id="navbarColor01">
	      <ul class="navbar-nav mr-auto">
	        <li class="nav-item active">
	          <a class="nav-link" href="/">Home</a>
	        </li>
	        <li class="nav-item">
	          <a class="nav-link" href="/Help">Help</a>
	        </li>
	        <li class="nav-item">
	          <a class="nav-link" href="/About">About</a>
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

现在让我们再来为应用创建一个底部视图，用于置放网站的一些基础信息。

_resources/views/layouts/\_footer.blade.php_

```js
<footer class="text-muted">
  <div class="container">
    <p class="float-right">
      <a href="#">Back to top</a>
    </p>
    <p>Album example is © Bootstrap, but please download and customize it for yourself!</p>
    <p>New to Bootstrap? <a href="../../">Visit the homepage</a> or read our <a href="../../getting-started/">getting started guide</a>.</p>
  </div>
</footer>
```

## 引入局部视图

在完成头部视图和底部视图的定义后，接下来便可以在 default 视图中引用这两个视图。

_resources/views/layouts/default.blade.php_

```
<!DOCTYPE html>
<html>
  <head>
    <title>@yield('title', 'Sample App') - Laravel 入门教程</title>
    <link rel="stylesheet" href="/css/app.css">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
  </head>
  <body>
  	@include('layouts._header')
    <div class="container">
      @yield('content')
    </div>   
    @include('layouts._footer') 
  </body>
</html>
```



