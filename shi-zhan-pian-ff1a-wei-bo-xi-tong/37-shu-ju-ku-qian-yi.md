传送门：[Laravel 的数据库迁移 Migrations](http://d.laravel-china.org/docs/5.5/migrations)

## 简介

**数据库迁移就像是数据库的版本控制**，可以让你的团队轻松修改并共享应用程序的数据库结构。

如果你曾经试过让同事手动在数据库结构中添加字段，那么数据库迁移可以让你不再需要做这样的事情。不仅如此，

Migration 建表要比直接手动创建表或者`.sql`文件具备额外的管理数据库的功能，如回滚、重置、更新等。Migration 的建表方法大部分情况下能兼容 MySQL, PostgreSQL, SQLite 甚至是 Oracle 等主流数据库系统。

