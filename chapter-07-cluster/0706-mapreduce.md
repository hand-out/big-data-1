
## Mapreduce

1. 启动集群
    ```bash
	$ startall.sh
    ```
2. 在集群上创建输入文件夹
    ```bash
	$ hdfs dfs -mkdir /user   
	$ hdfs dfs -mkdir /user/jack   
	$ hdfs dfs -mkdir /user/jack/input
    ```
3. 复制文件到输入文件夹
    ```bash
	$ hdfs dfs -put /usr/bd/hadoop-3.3.1/etc/hadoop/*.xml /user/jack/input
    ```
4. 查看输入文件情况
    ```bash
	$ hdfs dfs -ls /user/jack/input
    ```
5. 在集群上做 MapReduce 任务测试
    ```bash
	$ hadoop jar /usr/bd/hadoop-3.3.1/share/hadoop/mapreduce/hadoop-mapreduce-examples-3.3.1.jar wordcount /user/jack/input /user/jack/output
    ```
6. 查看执行结果
    ```bash
	$ hdfs dfs -cat /user/jack/output/*
    ```
7. Web 查看 MapReduce 执行情况
    - http://192.168.1.81:9870
    - http://192.168.1.81:8088
    - http://192.168.1.81:19888
8. 其他测试练习
    ```bash
    $ hadoop jar /usr/bd/hadoop-3.3.1/share/hadoop/mapreduce/hadoop-mapreduce-examples-3.3.1.jar pi 5 5
    ```	
    ```bash
    $ hadoop jar /usr/bd/hadoop-3.3.1/share/hadoop/mapreduce/hadoop-mapreduce-examples-3.3.1.jar wordmean input output1
    ```	
    ```bash
    $ hadoop jar /usr/bd/hadoop-3.3.1/share/hadoop/mapreduce/hadoop-mapreduce-examples-3.3.1.jar wordmedian input output2
    ```	
