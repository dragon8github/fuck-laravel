命名空间最初的设计是为解决命名冲突而产生的一种包装类、函数和常量的方法。

通过对组件化开发和composer使用的了解，应该可以看到命名空间另一个重要的作用是为组件化开发提供了可能，也就是通过命名空间来组织文件，使得某个组件的文件的路径和命名空间具有一定的关系，最终可以直接通过命名空间找到相应的文件。

正因为这种特性、使得composer管理工具可以方便地管理组件包的文件关系、再通过PSR规范将不同人开发的资源包方便地组合在一起。下面介绍有关命名空间及文件加载的相关内容。

## 一、命名空间的定义

命名空间是通过关键字namespace来定义的，如果一段PHP代码要通过命名空间来封装，则命名空间的声明需要在这部分代码之前。

```php
<?php
namespace App\Http;
use Illuminate \Foundation\Http\Kernel as HttpKernel;
class Kernel extends HttpKernel {
    // 其他代码内容
}
```

上述例子中定义了一个命名空间App\Http，并在命名空间下定义了Kernel类，因此Kernel类的完整名称应该为App\Http\Kemel

本质上，Kernel类文件的文件路径与命名空间是相互独立的、即在任何目录下都可以定义App\Http命名空间。

但为了命名的规范及后期文件包含的方便，一般将命名空间与文件路径定义为相同的名称，而文件名和类名定义为相同的名称。这样通过一个类的完整名称，就可以确定这个类所在文件相对于根目录的位置，为后期文件包含提供便利，这也是PSR规范规定的部分内容。

### PHP支持两种获取和使用当前命名空间的方法

* 魔术常量\_\_NAMESPACE\_\_
* namespace关键字

#### 1.1 魔术常量\_\_NAMESPACE\_\_

通过魔术常量 \_\_NAMESPACE\_\_ 可以直接获取当前命名空间名称的宇符串。

如果是全局的代码，即不包括在任何命名空间中的代码，通过该魔术常量将获取一个空的字符串。

#### 1.2 关键字namespace

关键字namespace可用来显式访问当前命名空间。

需要注意的是，如果没有定义命名空间，即为全局空间，相当于根空间，通过“\”来表示。

**Example 1 ：命名空间 App\Http**

```php
<?php
namespace App\Http;
echo __NAMESPACE__;  // "App\Http"
```

**Example 2 ：全局空间**

```php
<?php
echo __NAMESPACE__;  // ""
```

**Example 3 ：命名空间 App\Http**

```php
<?php
namespace App\Http;
class Kernel {}
$a = new namespace\ Kernel(); // 即 new App\Http\Kernel();
```

---

## 二、命名空间的使用

命名空间的使用是通过`use`关键字来实现的，PHP命名空间的使用方式通常有三种形式：

* 非限定名称或不包含前缀的名称
* 限定名称或包含前缀的名称
* 完全限定名称或包含了全局前缀操作符的名称



