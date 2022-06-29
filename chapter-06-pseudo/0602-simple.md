
## 伪分布模式最简配置

1. 修改 hadoop 下 etc/hadoop/core-site.xml 文件
    ```bash
    $ sudo vim /usr/bd/hadoop-3.3.1/etc/hadoop/core-site.xml
    ```
    ```xml {.line-numbers}
    <configuration>
        <property>
            <name>fs.defaultFS</name>
            <value>hdfs://localhost:9000</value>
        </property>
        <property>
            <name>hadoop.tmp.dir</name>
            <value>/usr/bd/tmp</value>
            <description>for hadoop temporary directories.</description>
        </property>
    </configuration>
    ```
2. 修改 hadoop 下 etc/hadoop/hdfs-site.xml 文件
    ```bash
    $ sudo vim /usr/bd/hadoop-3.3.1/etc/hadoop/hdfs-site.xml
    ```
    ```xml {.line-numbers}
    <configuration>
        <property>
            <name>dfs.replication</name>
            <value>1</value>
        </property>
        <property>
            <name>dfs.namenode.name.dir</name>
            <value>file:/usr/bd/dfs/name</value>
        </property>
        <property>
            <name>dfs.datanode.data.dir</name>
            <value>file:/usr/bd/dfs/data</value>
        </property>
        <property>
            <name>dfs.permissions</name>
            <value>false</value>
        </property>
    </configuration>
    ```
3. 格式化文件系统
    ```bash
    $ hdfs namenode -format
    ```
4. 启动 dfs
    ```bash
    $ start-dfs.sh
    ```
5. 查看启动进程
    ```bash
    $ jps

    2690 Jps
    2306 DataNode
    2132 NameNode
    2554 SecondaryNameNode
    ```
6. 查看日志信息
    ```bash
    $ ls /usr/bd/logs/
    ```
7. 查看 Namenode 网站
    - http://192.168.1.90:9870
8. 在 dhfs 上创建文件夹
    ```bash
    $ cd ~   
    $ hdfs dfs -mkdir /user   
    $ hdfs dfs -mkdir /user/jack   
    $ hdfs dfs -mkdir /user/jack/input
    ```
9. 复制本地文件到 hdfs
    ```bash
    $ hdfs dfs -put /usr/bd/hadoop-3.2.2/etc/hadoop/*.xml input   
    $ hdfs dfs -ls input
    ```
10. 查看 Namenode 网站
    - http://192.168.1.90:9870
    - Utilities -> Browse the file system
    - Browse Directory: /user/jack/input
    - Go!
11. 离开安全模式
    ```bash
    hadoop dfsadmin -safemode leave
    ```
12. 执行伪分布测试
    ```bash
    $ hadoop jar /usr/bd/hadoop-3.2.2/share/hadoop/mapreduce/hadoop-mapreduce-examples-3.2.2.jar grep input output 'dfs[a-z.]+'
    ```
13. 查看 hdfs 文件信息
    ```bash
    $ hdfs dfs -cat output/*
    ```
    ```bash {.line-numbers}
    1       dfsadmin
    1       dfs.replication
    1       dfs.permissions
    1       dfs.namenode.name.dir
    1       dfs.datanode.data.dir
    ```
14. 复制 hdfs 文件到本地查看
	```bash
    cd ~
    sudo rm -rf output
    $ hdfs dfs -get output output   
    $ cat output/*
    ```
    ```bash {.line-numbers}
    1       dfsadmin
    1       dfs.replication
    1       dfs.permissions
    1       dfs.namenode.name.dir
    1       dfs.datanode.data.dir
    ```
15. 查看 Namenode 网站
    - http://192.168.1.90:9870
    - Utilities -> Browse the file system
    - Browse Directory: /user/jack/output
    - Go!
16. 查看 datanode 网站接口
    - http://192.168.1.81:9864
17. 停止 dfs
    ```bash
    $ stop-dfs.sh
    ```
18. 查看启动进程
    ```bash
    $ jps
    ```

由于网络和 Hadoop 配置并不完善，Eclipse 下的 DFS 文件浏览仍然不能正常使用，MapReduce 程序仍然在本地的 Widnows 上运行。
可以通过 SCP 上传打包的 jar 文件到 Ubuntu，然后在 Ubuntu 上本地运行 MapReduce 程序。
