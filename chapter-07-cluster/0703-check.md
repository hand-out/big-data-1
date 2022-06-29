
## 复查每个节点的基础环境

1. 复查每个节点的工作目录
    ```bash
    $ tree -L 2 /usr/bd
    ```
    ```bash {.line-numbers}
    /usr/bd
    ├── dfs
    │   ├── data
    │   └── name
    ├── hadoop-3.3.1
    ├── jdk-11.0.13
    ├── logs
    └── tmp
    ```
2. 复查每个节点的/etc/profile
    ```bash
    sudo vim /etc/profile
    ```
3. 使每个节点的 profile 生效
    ```bash
    source /etc/profile
    ```
3. 复查每个节点的 java 路径配置
    ```bash
    $ java -version
    ```
4. 设置节点 name 的`hadoop-env.sh`
    ```bash
    sudo vim /usr/bd/hadoop-3.3.1/etc/hadoop/hadoop-env.sh
    ```
    ```bash
    export JAVA_HOME=/usr/bd/jdk-11.0.13
    export HADOOP_LOG_DIR=/usr/bd/logs
    ```
5. 复制 name 的 hadoop-env.sh 到其他节点
    ```bash
    scp /usr/bd/hadoop-3.3.1/etc/hadoop/hadoop-env.sh node1:/usr/bd/hadoop-3.3.1/etc/hadoop/
    ```
4. 复查 hadoop 路径配置
    ```bash
    $ hadoop
    $ hadoop version
    ```
