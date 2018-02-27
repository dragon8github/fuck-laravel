Laravel 默认会为每个新建的项目自动生成该文件，并会在文件里面默认集成一些较为常用的扩展包。我们可以在编辑器中查看此文件：

_package.json_

```js
{
    "private": true,
    "scripts": {
        "dev": "npm run development",
        "development": "cross-env NODE_ENV=development node_modules/webpack/bin/webpack.js --progress --hide-modules --config=node_modules/laravel-mix/setup/webpack.config.js",
        "watch": "cross-env NODE_ENV=development node_modules/webpack/bin/webpack.js --watch --progress --hide-modules --config=node_modules/laravel-mix/setup/webpack.config.js",
        "watch-poll": "npm run watch -- --watch-poll",
        "hot": "cross-env NODE_ENV=development node_modules/webpack-dev-server/bin/webpack-dev-server.js --inline --hot --config=node_modules/laravel-mix/setup/webpack.config.js",
        "prod": "npm run production",
        "production": "cross-env NODE_ENV=production node_modules/webpack/bin/webpack.js --no-progress --hide-modules --config=node_modules/laravel-mix/setup/webpack.config.js"
    },
    "devDependencies": {
        "axios": "^0.18",
        "bootstrap": "^4.0.0",
        "cross-env": "^5.1.3",
        "jquery": "^3.2",
        "laravel-mix": "^2.0",
        "lodash": "^4.17.4",
        "popper.js": "^1.12",
        "vue": "^2.5.7"
    }
}
```

### 安装yarn

```
$ brew install yarn
```

使用 Yarn 对扩展包进行安装，请在项目根目录下运行以下命令进行安装：

```
$ yarn install --no-bin-links
$ yarn add cross-env
```

安装完成之后，让我们对 Laravel 默认生成的`app.scss`文件进行编辑，删除此文件里的所有内容，只留下面一行，导入 Bootstrap：

_resources/assets/sass/app.scss_

```css
// Bootstrap
@import "node_modules/bootstrap/scss/bootstrap";
```

将 Bootstrap 导入成功之后，我们需要使用以下命令来将 .scss 文件编译为 .css 才能正常使用，编译命令如下：

```
$ npm run dev
```

我们也可以通过下面的命令，在每次检测到 .scss 文件发生更改时，自动将其编译为 .css 文件：

```
$ npm run watch-poll
```

> 请保证在进行项目开发时 npm run watch-poll 一直运行着

所有编译后的资源文件都被存放在`public`文件夹中，你能在`public/css`文件夹中看到刚刚编译成功之后的文件。



接下来让我们更改基础视图的页面结构，为应用添加顶部导航，并加入帮助页和登录页的链接。

_resources/views/layouts/default.blade.php_

```js
<!DOCTYPE html>
<html>
  <head>
    <title>@yield('title', 'Sample App') - Laravel 入门教程</title>
    <link rel="stylesheet" href="/css/app.css">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
  </head>
  <body>
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

    <div class="container">
      @yield('content')
    </div>    
  </body>
</html>
```

现在让我们接着更改首页信息，加多一些页面元素。

_resources/views/static\_pages/home.blade.php_

```php
@extends('layouts.default')

@section('content')
  <div class="jumbotron">
	    <h1 class="display-4">Hello, world!</h1>
	    <p class="lead">This is a simple hero unit, a simple jumbotron-style component for calling extra attention to featured content or information.</p>
	    <hr class="my-4">
	    <p>It uses utility classes for typography and spacing to space content out within the larger container.</p>
	    <p class="lead">
	      <a class="btn btn-primary btn-lg" href="#" role="button">Learn more</a>
	    </p>
  </div>
@stop
```

_resources/assets/sass/app.scss_

```
// Bootstrap
@import "node_modules/bootstrap/scss/bootstrap";


body {
  padding-top: 80px;
}
```



