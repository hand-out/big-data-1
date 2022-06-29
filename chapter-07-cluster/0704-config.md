
## 修改 name 的 hadoop 配置文件

1. 修改 node0 的 workers 
    ```bash
    $ sudo vim /usr/bd/hadoop-3.3.1/etc/hadoop/workers
    ```
    @import "../config/clust-workers.md"
2. 复制 name 的 worker 到其他节点
    ```bash
    scp /usr/bd/hadoop-3.3.1/etc/hadoop/workers node1:/usr/bd/hadoop-3.3.1/etc/hadoop/
    ```
3. 修改 name 的 core-site.xml
    ```bash
	  $ sudo vim /usr/bd/hadoop-3.3.1/etc/hadoop/core-site.xml
    ```
    @import "../config/clust-core-site.xml.md"
4. 复制 node0 的 core-site.xml 到其他节点
    ```bash
    scp /usr/bd/hadoop-3.3.1/etc/hadoop/core-site.xml node1:/usr/bd/hadoop-3.3.1/etc/hadoop/
    ```
5. 修改 name 的 hdfs-site.xml，注意复制份数为 2
    ```bash
	  $ sudo vim /usr/bd/hadoop-3.3.1/etc/hadoop/hdfs-site.xml
    ```
    @import "../config/clust-hdfs-site.xml.md"
6. 复制 name 的 hdfs-site.xml 到其他节点
    ```bash
    scp /usr/bd/hadoop-3.3.1/etc/hadoop/hdfs-site.xml node1:/usr/bd/hadoop-3.3.1/etc/hadoop/
    ```
7. 修改 name 的 mapred-site.xml
    ```bash
	  $ sudo vim /usr/bd/hadoop-3.3.1/etc/hadoop/mapred-site.xml
    ```
    @import "../config/clust-mapred-site.xml.md"
8. 复制 node0 的 mapred-site.xml 到其他节点
    ```bash
    scp /usr/bd/hadoop-3.3.1/etc/hadoop/mapred-site.xml node1:/usr/bd/hadoop-3.3.1/etc/hadoop/
    ```
9. 修改 name 的 yarn-site.xml
    ```bash
	  $ sudo vim /usr/bd/hadoop-3.3.1/etc/hadoop/yarn-site.xml
    ```
    @import "../config/clust-yarn-site.xml.md"
10. 复制 name 的 yarn-site.xml 到其他节点
    ```bash
    scp /usr/bd/hadoop-3.3.1/etc/hadoop/yarn-site.xml node1:/usr/bd/hadoop-3.3.1/etc/hadoop/
    ```
11. 清除遗留数据
    ```bash
	  $ sudo rm -rf /usr/bd/dfs/data/current/   
	  $ ls /usr/bd/dfs/data   
    ```
    ```bash
	  $ sudo rm -rf /usr/bd/dfs/name/current/   
	  $ ls /usr/bd/dfs/name   
    ```
