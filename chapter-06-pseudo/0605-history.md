
## 配置作业历史服务器

1. 修改 mapred-site.xml 文件
    ```bash
    $ sudo vim /usr/bd/hadoop-3.3.1/etc/hadoop/mapred-site.xml
    ```
    ```xml {.line-numbers}
    <configuration>
        <property>
            <name>mapreduce.jobtracker.address</name>
            <value>name:9001</value>
        </property>
        <property>
            <name>yarn.app.mapreduce.am.env</name>
            <value>HADOOP_MAPRED_HOME=/usr/bd/hadoop-3.3.1</value>
        </property>
        <property>
            <name>mapreduce.map.env</name>
            <value>HADOOP_MAPRED_HOME=/usr/bd/hadoop-3.3.1</value>
        </property>
        <property>
            <name>mapreduce.reduce.env</name>
            <value>HADOOP_MAPRED_HOME=/usr/bd/hadoop-3.3.1</value>
        </property>
        <property>
            <name>mapreduce.framework.name</name>
            <value>yarn</value>
        </property>
        <property>
            <name>mapreduce.jobhistory.address</name>
            <value>name:10020</value>
        </property>
    </configuration>
    ```
2. 启动 YARN
    ```bash
	$ start-yarn.sh
    ``` 
3. 查看启动进程
    ```bash
	$ jps
	```
4. 启动 DFS
    ```bash
	$ start-dfs.sh
    ``` 
5. 查看启动进程
    ```bash
	$ jps
	```
6. 启动 historyserver
    ```bash
	$ mr-jobhistory-daemon.sh start historyserver
    ``` 
7. 查看启动进程
    ```bash
	$ jps
    17714 NameNode
    18148 SecondaryNameNode
    16972 ResourceManager
    17916 DataNode
    17148 NodeManager
    18973 JobHistoryServer
    19038 Jps
    ```
8. 进入 history 管理页面
    - http://192.168.1.81:19888
9. 删除输出目录
    ```bash
	$ hdfs dfs -rm -r -f /user/jack/output
    ``` 
10. DFS 文件列表
    ```bash
	$ hdfs dfs -ls /user/jack
	```
11. 执行 MapReduce
    ```bash
    $ hadoop jar /usr/bd/hadoop-3.3.1/share/hadoop/mapreduce/hadoop-mapreduce-examples-3.3.1.jar grep input output 'dfs[a-z.]+'
    ```
12. HDFS 命令查看测试结果
    ```bash
    $ hdfs dfs -cat /user/jack/output/*
    ```
    ```bash {.line-numbers}
    1       dfsadmin
    1       dfs.replication
    1       dfs.permissions
    1       dfs.namenode.name.dir
    1       dfs.namenode.http
    1       dfs.datanode.data.dir
    ```
13. 停止 historyserver
    ```bash
  	$ mr-jobhistory-daemon.sh stop historyserver
    ```
14. 停止 YARN
    ```bash
	$ stop-yarn.sh
    ```
15. 停止 dfs
    ```bash
	$ stop-dfs.sh
    ```
