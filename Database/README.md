#Everything about Database Technology
---
##introduction for different kind of Database

>####SQLite
 不像常见的客户端/服务器结构数据库管理系统，SQLite引擎不是一个应用程序与之通信的独立进程。SQLite库链接到程序中，并成为它的一个组成部分。这个库也可被动态链接。应用程序经由编程语言内的直接API调用来使用SQlite的功能，这在减少数据库访问延迟上有积极作用，因为在一个单一进程中的函数调用比跨进程通信更有效率。SQLite将整个数据库，包括定义、表、索引以及数据本身，作为一个单独的、可跨平台使用的文件存储在主机中。它采用了在写入数据时将整个数据库文件加锁的简单设计。尽管写操作只能串行进行，但SQLite的读操作可以多任务同时进行。

>SQLite将PostgreSQL作为参考平台。项目将“PostgreSQL可能做些什么”作为SQL标准实现的开发参考。然而与这个目标最重要的偏差在于，除了主键以外，SQLite不强制进行类型检查。一个值的类型是动态的，不被schema所强制限制（虽然如此，但如果可以进行可恢复的类型转换时，schema会在存储数据时触发一个自动转换）。

>####PostgreSQL
>PostgreSQL是自由的对象-关系型数据库服务器
>
>PostgreSQL相对于竞争者的主要优势为可编程性

>PostgreSQL允许用户定义基于正规的SQL类型的新类型，允许数据库自身理解复杂数据。例如，你可以定义一个address来组合一些事物如街道编号、城市和国度的字符串。从这一点上你可以轻易的创建把保存地址的所需要的所有字段包含在一个单一行列中的表。

>PostgreSQL还允许类型包括继承，这是在面向对象编程中的主要概念。例如，你可以定义```post_code```类型，并接着基于它创建```us_zip_code```和```canadian_postal_code```。

>Ref: [wiki](https://zh.wikipedia.org/wiki/PostgreSQL)

