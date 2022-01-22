# RustLibCreateCollect

Marked 的 Rust Crate 收集

以下会简单进行分类

## 基础套件

- `serde` 常用的序列化与反序列化支持库

  - [主页](https://serde.rs/) | [项目地址](https://github.com/serde-rs/serde)
  - [更多](./serde.md)
  - 常用依赖组合

    ```toml
    [dependencies.serde]
    version= "1.0"
    features=["derive"]
    ```

- `serde_json` 配合`serde`使用的[JSON](https://www.json.org/json-en.html)序列化与反序列化 crate

  - [项目地址](https://github.com/serde-rs/json)
  - [更多](./serde_json.md)
  - 常用依赖组合

    ```toml
    [dependencies.serde_json]
    version = "1.0"
    ```

## 框架

## 过程宏相关
