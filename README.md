# 使用智谱api+graphrag的测试demo

[点击查看graphrag官方文档>>](https://microsoft.github.io/graphrag/get_started/)


### 准备环境

- 创建环境
    ```shell
    conda create -n graphrag-test python=3.10.13 -y
    ```

- 激活环境
    ```shell
    conda activate graphrag-test
    ```

- 安装依赖（几分钟）
    ```shell
    pip install graphrag
    ```

- 创建输入目录
    ```shell
    mkdir -p ./ragtest/input
    ```

- 下载书籍到输入目录（或者自行到[z-lib.gs](https://zh.z-lib.gs)下载其他书籍），这里用的`英文书籍`
    ```shell
    curl https://www.gutenberg.org/cache/epub/24022/pg24022.txt -o ./ragtest/input/book.txt
    ```

- 初始化配置（几十秒）
    ```shell
    python -m graphrag.index --init --root ./ragtest
    ```

### 更新配置

- 替换[.env](./ragtest/.env)中的`GRAPHRAG_API_KEY`配置为`智谱的key`

- 替换[settings.yaml](./ragtest/settings.yaml)中的`model`为 `glm-4-plus`

- 替换[settings.yaml](./ragtest/settings.yaml)中的`api_base`为 `https://open.bigmodel.cn/api/paas/v4`

- 替换[settings.yaml](./ragtest/settings.yaml)中的e`mbeddings`的`model`为 `embedding-3`


### 构建知识图谱+向量化处理
`126k`大小的`txt文本`处理大概要`5分多钟`，以此类推
```shell
python -m graphrag.index --root ./ragtest
```


### 执行查询
windows系统下需要将命令行分隔符的 \ 替换为 `

- 查询(202410230201~202410230203，耗时2分钟)
```shell
python -m graphrag.query \
--root ./ragtest \
--method global \
"What are the top themes in this story?"
```

- 查询2
```shell
python -m graphrag.query \
--root ./ragtest \
--method local \
"Who is Scrooge, and what are his main relationships?"
```

### 相关截图
![image](https://github.com/user-attachments/assets/e44d241c-af8b-4c64-b662-ee267175e4e8)

![image](https://github.com/user-attachments/assets/21ec2c43-969b-490f-bc5e-8ebca320134f)



