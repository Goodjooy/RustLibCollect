# Serde 序列化与反序列

[参考文档](https://serde.rs/)

- 常用 featrue

  ```toml
  [dependencies.serde]
  version= "1.0"
  features=["derive"]
  ```

## 常用方法

- 通过`#[derive()]`来自动实现序列化与反序列化

  ```rust
  #[derive(serde::Serialize, serde::Deserialize)]
  struct MockObject{
      mock_string:String,
      mock_int:i32
  }
  ```

  如果序列化为 json，将会这样

  ```json
  {
    "mock_string": "String",
    "mock_int": 0
  }
  ```

- 添加`#[serde(...)]`以改变序列化/反序列化效果

  - `#[serde(rename="newName")]`以重命名字段序列化时名称

    ```rust
    #[derive(serde::Serialize, serde::Deserialize)]
    struct MockObject{
        #[serde(rename="realString")]
        mock_string:String,
        mock_int:i32
    }
    ```

    如果序列化为 json，将会这样

    ```json
    {
      "realString": "String",
      "mock_int": 0
    }
    ```

  - `#[serde(alias="newName")]`以添加字段反序列化序列化时可识别的名称

    ```rust
    #[derive(serde::Serialize, serde::Deserialize)]
    struct MockObject{
        #[serde(alias="realString")]
        mock_string:String,
        mock_int:i32
    }
    ```

    如果从 Json 反序列化，以下的均可成功

    ```json
    {
      "realString": "String",
      "mock_int": 0
    }
    ```

    或者

    ```json
    {
      "mock_string": "String",
      "mock_int": 0
    }
    ```

- 枚举类型序列化

  ```rust
  #[derive(serde::Serialize, serde::Deserialize)]
  enum MockEnum{
      MockType2{
          a:String,
          b:usize
      }
  }
  ```

  通常会序列化为如下形式

  ```json
  {
    "MockType1": [0, 0]
  }
  ```

  或者

  ```json
  {
    "MockType2": {
      "a": "String",
      "b": 0
    }
  }
  ```

  - 使用 `#[serde(tag="typeName")]`将 tag 序列化进 Map 内部

    ```rust
    #[derive(serde::Serialize, serde::Deserialize)]
    #[serde(tag="type")]
    enum MockEnum{
        MockType2{
            a:String,
            b:usize
            }
    }
    ```

    序列化为 json 将是

    ```json
    {
      "type": "MockType2",
      "a": "String",
      "b": 0
    }
    ```

  - 使用 `#[serde(tag="typeName",content="content")]`将tag和数据分组

    ```rust
    #[derive(serde::Serialize, serde::Deserialize)]
    #[serde(tag = "type",content = "content")]
    enum MockEnum{
        MockType2{
            a:String,
            b:usize
            }
    }
    ```

    序列化为 json 将是

    ```json
    {
      "type": "MockType2",
      "content":{
          "a": "String",
          "b": 0
      }
    }
    ```

  - 使用 `#[serde(untagged)]`不区分tag

    ```rust
    #[derive(serde::Serialize, serde::Deserialize)]
    #[serde(untagged)]
    enum MockEnum{
        MockType2{
            a:String,
            b:usize
            }
    }
    ```

    序列化为 json 将是

    ```json
    {
        "a": "String",
        "b": 0
    }
    ```
