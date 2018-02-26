### 一、 组件安装

#### 1.1 composer init

以交互式的方式初始化composer.json，一路回车即可。

然后会生成composer.json文件，这也是使用 `$ composer require <pageage>` 的前提。

#### 1.2 composer require

添加新的依赖包到项目，并更新 composer.json 内容的依赖信息。

当前目录必须存在composer.json才可以使用此命令。

```
$ composer require monolog/monolog
```

#### 1.3 composer.json

手动创建 composer.json ，指定依赖包信息。

```
{
    "name": "lizhaohong/testcomposer",
    "authors": [
        {
            "name": "dragon8github",
            "email": "928532756@qq.com"
        }
    ],
    "require": {
        "monolog/monolog": "^1.23"
    }
}
```

然后执行`$ composer instal`命令，它从当前目录读取 composer.json 文件，处理依赖关系，并安装到verdor目录下。

### 二、 自动加载

#### 2.1 autoload.php

在vendor目录下，提供一个自动加载文件 autoload.php，只需要在项目中通过 `require 'vendor/autoload.php'`语句引入这个文件。在使用组件时就会自动加载了。如上一小节中，我们下载了 monolog 组件，就可以通过 `$myLog = new \monolog\Logger('helloworld')` 语句直接使用组件中的类库，而 autoload.php 文件会自动加载相应的类文件。

#### 2.2 自动加载的四大规范形式

* PSR-0
* PSR-4
* classmap
* files

**其中PSR-4是目前推荐使用的规范。**这四种规范形式本质上是定义了一个命名空间到实际文件的映射关系。通过这个映射关系，可以利用命名空间类精确定位到相应文件的具体丼，进而实现 autoload 自动加载功能。后续实战中我们再详细讲解各个规范的配置使用。

### 三、 composer 命令行简介

![](/assets/2import.png)

