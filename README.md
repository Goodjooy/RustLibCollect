# RustLibCollect

Marked 的 Rust Crate 收集

[扩展参考](./Expand-rule.md)

以下会简单进行分类

## 基础套件

- `serde` 常用的序列化与反序列化支持库

  - [主页](https://serde.rs/) | [项目地址](https://github.com/serde-rs/serde)
  - [更多](./serde.md)
  - 常用 features
    - `derive` : `derive macro`将可用

- `serde_json` 配合`serde`使用的[JSON](https://www.json.org/json-en.html)序列化与反序列化库

  - [项目地址](https://github.com/serde-rs/json)

- `state` 线程安全的全局变量，`thread local`变量以及数据容器

  - [项目地址](https://github.com/SergioBenitez/state)

- `url` 网址转换库，将 `&str` 转换为`url`

  - [项目地址](https://github.com/servo/rust-url)

- `hex` 解码和编码二进制到十六进制字符串

  - [项目地址](https://github.com/KokaKiwi/rust-hex)

- `dashmap` 线程安全的`HashMap`,与标准库中`HashMap`接口基本一致

  - [项目地址](https://github.com/KokaKiwi/rust-hex)
  - 注意
    - `dashmap::DashMap` 使用内部可变性，在使用可变引用时使用不可变引用可能导致死锁
  - 常用 features
    - `serde` 启用序列化功能

- `uuid` UUID 生成

  - [项目地址](https://github.com/uuid-rs/uuid)
  - 常用 features
    - `serde` : 使得`uuid::Uuid`可以序列化与反序列化
    - `v4` : 使得 `Uuid::new_v4()`可用

- `regex` 正则表达式

  - [项目地址](https://github.com/rust-lang/regex)
  - 常用 features
    - `std` : 使用标准库

- `chrono` 日期与时间库，扩展标准库

  - [项目地址](https://github.com/chronotope/chrono)

- `figment` 配置文件解析库

  - [项目地址](https://github.com/SergioBenitez/Figment)
  - 常用 features
    - `env` : 可以使用来自环境变量的配置内容
    - `toml` : 可以使用来自 toml 文件的配置内容
    - `json` : 可以使用来自 json 文件的配置内容
    - `yaml` : 可以使用来自 yaml 文件的配置内容

- `lazy_static` 解除部分 static 限制， 惰性 static

  - [项目地址](https://github.com/rust-lang-nursery/lazy-static.rs)

- `rust-crypto` rust 加密库，提供常见加密算法

  - [项目地址](https://github.com/DaGenix/rust-crypto/)

- `log` rust 官方提供的日志使用形态（需要配合 logger 使用）

  - [项目地址](https://github.com/rust-lang/log)
  - [可用`logger`s](https://docs.rs/log/latest/log/#available-logging-implementations)

- `dotenv` 环境变量获取库
  - [项目地址](https://github.com/dotenv-rs/dotenv)

## `async` 运行时以及附属套件

- `tokio` 异步运行时
  - **_待添加_**

## 框架

- `sea-orm` 动态，异步的 ORM (基于 sqlx)

  - [项目地址](https://github.com/SeaQL/sea-orm) | [主页](https://www.sea-ql.org/SeaORM/)
  - features 配置[参考](https://www.sea-ql.org/SeaORM/docs/install-and-config/database-and-async-runtime)
  - [更多](./sea-orm/index.md)

- `diesel` 静态, 同步阻塞 ORM
  - **_待添加_**
- `rocket` Http web 服务器框架
  - **_待添加_**
- `pest` 优雅的语法解析器
  - **_待添加_**

## 过程宏相关

## 开发辅助
