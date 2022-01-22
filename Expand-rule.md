# 扩展该搜集仓库的约定

1. 根据目前根目录下 `READEME.md` 分类方式，添加索引词条  
    如果添加的库使用简单，可以不添加额外的文件  
    格式如下

      ```markdown
        - `<crate-name>` <crate的一句话介绍>
          - <crate的相关链接，至少包含仓库，多个链接用 "|" 分割>
          <!-- 可选部分，如果添加额外文件则必须 -->
          - [更多](path/to/extra)
          <!-- 可选，如果没有features 或者使用default 即可可以不添加 -->
          - 常用features
            - `<feature-falg>` : <一句话介绍>
      ```

2. 额外文件格式

- 额外文件只有一个，直接在项目根目录下创建`<crate-name>.md`  
  使用 `[更多](./<crate-name>.md)`
- 额外文件有多个，创建 `<crate-name>`文件夹,并在内部创建`index.md`文件
  使用 `[更多](./<crate-name>/index.md)`
