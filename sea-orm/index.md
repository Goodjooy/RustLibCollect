# Sea-Orm 动态，异步的 ORM 框架

- 辅助工具

  - `sqlx-cli` sqlx 的终端工具，用于辅助建表  
    更多参考 [sqlx](https://crates.io/crates/sqlx-cli)

    1. 安装 `sqlx-cli`

       ```shell
       cargo install sqlx-cli
       ```

    2. 配置连接数据库

       - 在项目目录下新建 `.env` 文件
       - 在`.env`文件内配置数据库连接 URL

         ```txt
         DATABASE_URL=sql://username:password@localhost/database
         ```

    3. 新建数据库

       - 终端使用指令,其中 <name\> 为新`.sql`文件名称  
         通常情况下，文件会新建在 `./migrations`文件夹内  
         格式为`<精确到秒的创建时间>_<name>.sql`

         ```shell
         sqlx migrate add <name>
         ```

       - 在新建的 sql 文件内写上建表 SQL 代码
       - 执行

         ```shell
         sqlx migrate run
         ```

         以创建数据库

    ***

    - 其他常用指令

      -重置数据库（通常在更改数据库结构后使用）

      ```shell
      sqlx database reset
      ```

  - `sea-orm-cli` sea-orm 终端工具，用于从数据库表的信息生成 Entity

    - 安装

    ```shell
    cargo install sea-orm-cli
    ```

    _注意_: 某些情况下，使用 `cargo install`可能会安装失败  
    前往 `{CARGO_HOME}/registry/src/github.com-{XXX}/sea-orm-cli-{version}`目录  
    打开终端，使用 `cargo build --release` 编译  
    进入 `./target/release` 将其中名为 `sea-orm-cli` 拷贝到 `{CARGO_HOME}/bin`即可

    - 配置`.env`文件 （同 sqlx）
    - 生成 `Entity`  
      其中 -o 为输出文件夹路径  
      更多使用[参考](https://www.sea-ql.org/SeaORM/docs/generate-entity/sea-orm-cli)

      ```shell
        sea-orm-cli generate entity -o src/entity
      ```

- orm 生成 Entity 结构

  - `Model` 对应表的模型，用于接受查询结果
  - `ActiveModel` 记录模型变化的模型，用于更新数据库
  - `Entity` 包含所有全部对应 table 的操作
    - 举例: `Entity::find_by_id(1).one(db).await?`
  - `Column` 包含对应表中的每列的信息，用于辅助进行数据库操作

    - 举例:

    ```rust
        let result: Vec<Model> = Entity::find()
        .filter(Column::Name.contains("target"))
        .order_by_asc(Column::Name)
        .all(db)
        .await?;
    ```

  - `Relation` 数据库表之间的关系，用于联合查询

    - 举例(cake 与 fruit 是 many to one 关系):

    ```rust
        let cake_with_fruits: Vec<(cake::Model, Vec<fruit::Model>)> =
        Cake::find()
        .find_with_related(Fruit)
        .all(db)
        .await?;
    ```

- `Condition` orm筛选器构造器 [参考](https://www.sea-ql.org/SeaORM/docs/advanced-query/conditional-expression)
    - `all()` 模式 全部表达式都满足
    - `any()` 模式 一个表达式满足
    - `Condition` 可以嵌套使用

- orm 简单使用

  - Select [参考](https://www.sea-ql.org/SeaORM/docs/basic-crud/select/)
  - Insert [参考](https://www.sea-ql.org/SeaORM/docs/basic-crud/insert/)
  - Update [参考](https://www.sea-ql.org/SeaORM/docs/basic-crud/update)
  - Save [参考](https://www.sea-ql.org/SeaORM/docs/basic-crud/save)
  - Delete [参考](https://www.sea-ql.org/SeaORM/docs/basic-crud/delete)

- Json 序列化支持
