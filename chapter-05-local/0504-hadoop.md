
## 准备 Hadoop

在 Windows 环境去 Apache [^apache_home] 的官网 [^hadoop_home] 下载 [^hadoop_down] Hadoop 部署文件到 D:/students/20211202/bd1/tool/hadoop-3.3.1.tar.gz。

打开 PowerShell
```
scp D:/students/20211202/bd1/tool/hadoop-3.3.1.tar.gz jack@192.168.1.81:/home/jack
```

1. 登录 Ubuntu Server
2. 进入家目录
    ```
    cd ~
    ls
    ```
3. 解压 Hadoop
    ```bash
    $  sudo tar -zxvf hadoop-3.3.1.tar.gz
    ```
4. 部署 Hadoop
    ```
    sudo mv hadoop-3.2.2 /usr/bd
    ls /usr/bd
    ```
5. 配置 Path
    ```bash
    $ sudo vim /etc/profile 
    ```
    ```bash {.line-numbers}
    export JAVA_HOME=/usr/bd/jdk-11.0.11
    export PATH=$PATH:$JAVA_HOME/bin

    export HADOOP_HOME=/usr/bd/hadoop-3.2.2
    export PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin
    ```
5. 执行/etf/profile 使配置生效
    ```bash
    $ source /etc/profile
    ```
6. 检查系统环境变量
    ```bash
    $ env
    hadoop
    hadoop version
    ```
7. 配置 hadoop-env.sh
    ```bash
    $ cd /usr/bd/hadoop-3.2.2/   
    $ sudo vim etc/hadoop/hadoop-env.sh
    ```
    ```bash {.line-numbers}
    # The java implementation to use. By default, this environment
    # variable is REQUIRED on ALL platforms except OS X!
    export JAVA_HOME=/usr/bd/jdk-11.0.13
    ... ...
    # Where (primarily) daemon log files are stored.
    # ${HADOOP_HOME}/logs by default.
    # Java property: hadoop.log.dir
    # export HADOOP_LOG_DIR=${HADOOP_HOME}/logs
    export HADOOP_LOG_DIR=/usr/bd/logs
    ```
8. 测试 Hadoop 命令
    ```bash
    cd ~
    $ hadoop
    $ hadoop version
    ```

[^apache_home]: Apache 官网，https://www.apache.org/
[^hadoop_home]: Hadoop 官网，http://hadoop.apache.org/
[^hadoop_down]: Hadoop 下载地址，https://hadoop.apache.org/releases.html
