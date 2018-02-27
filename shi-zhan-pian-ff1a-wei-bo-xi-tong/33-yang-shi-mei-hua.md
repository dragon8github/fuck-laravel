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



