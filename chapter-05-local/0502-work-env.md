
## 工作环境准备

我们将规划部署的内容命名为 bd，其目录结构如下：

```bash
/usr/bd
├── dfs
│   ├── data
│   └── name
├── hadoop-3.2.2        注：软件安装时创建（版本可能不同）
├── jdk-11.0.10         注：软件安装时创建（版本可能不同）       
├── logs
└── tmp
```

创建上述目录结构：

1. 创建目录
    ```bash 
    $ sudo mkdir /usr/bd    
    $ cd /usr/bd    
    $ sudo mkdir dfs logs tmp dfs/name dfs/data
    ```
2. 修改目录权限
    ```bash
    $ sudo chown -R jack:jack dfs logs tmp
    ```
3. 查看目录权限
    ```bash
    $ ls -ls
    ```
    ```bash {.line-numbers}
     4 drwxr-xr-x  4 jack  jack                 4096 Mar 19 08:26 dfs
     4 drwxr-xr-x  2 jack  jack                 4096 Mar 19 08:27 logs
     4 drwxr-xr-x  2 jack  jack                 4096 Mar 19 08:27 tmp
    ```
    ```bash
    $ ls -ls dfs
    ```
    ```bash {.line-numbers}
    4 drwxr-xr-x 2 jack jack 4096 Mar 19 08:26 data
    4 drwxr-xr-x 2 jack jack 4096 Mar 19 08:26 name
    ```

    