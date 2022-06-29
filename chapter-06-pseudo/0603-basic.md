
## 伪分布模式基本配置

### 检查网络配置

1. 配置主机名
    ```bash
    $ sudo vim /etc/hostname
    ```
    ```bash {.line-numbers}
    name
    ```
2. 查看网卡信息
    ```bash
  	$ ifconfig
    ```
    ```bash {.line-numbers}
    ens33: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
            inet 192.168.1.81  netmask 255.255.255.0  broadcast 192.168.1.255
    ```
3. 配置 IP 地址
    ```bash
    $  sudo vim /etc/netplan/00-installer-config.yaml

    ```
    ```yaml {.line-numbers}
    network:
        ethernets:
            ens33:
                addresses: [192.168.1.81/24]
                gateway4: 192.168.1.254
                dhcp4: true
                optional: true
        version: 2
    ```
4. 执行网卡配置
    ```bash
  	$ sudo netplan apply
    ```
5. 查看网卡信息
    ```bash
    $ ifconfig
    ```
    ```bash {.line-numbers}
    ens33: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
            inet 192.168.1.81  netmask 255.255.255.0  broadcast 192.168.1.255
    ```
6. 配置域名
    ```bash
    $ sudo vim /etc/hosts
    ```
    ```bash {.line-numbers}
    127.0.0.1 localhost
    #127.0.1.1  name

    192.168.1.91 name

    # The following lines are desirable for IPv6 capable hosts
    ::1     ip6-localhost ip6-loopback
    fe00::0 ip6-localnet
    ff00::0 ip6-mcastprefix
    ff02::1 ip6-allnodes
    ff02::2 ip6-allrouters
    ```
7. 配置 DNS 服务器
    ```bash
    $ sudo vim /etc/systemd/resolved.conf
    ```
    ```bash {.line-numbers}
    [Resolve]
    DNS=114.114.114.114 8.8.8.8
    ```
8. 测试 DNS
    ```
    ping www.baidu.com
    ctrl + c
    ```

### Hadoop 配置

1. 配置 core-site.xml
    ```bash
    $ sudo vim /usr/bd/hadoop-3.3.1/etc/hadoop/core-site.xml
    ```
    ```xml {.line-numbers}
    <configuration>
        <property>
            <name>fs.defaultFS</name>
            <value>hdfs://name:9000</value>
        </property>
        <property>
            <name>hadoop.tmp.dir</name>
            <value>/usr/bd/tmp</value>
            <description>for hadoop temporary directories.</description>
        </property>
    </configuration>
    ```
2. 配置 mapred-site.xml
    ```bash
    $ sudo vim /usr/bd/hadoop-3.3.1/etc/hadoop/mapred-site.xml
    ```
    ```xml {.line-numbers}
    <configuration>
        <property>
            <name>mapreduce.jobtracker.address</name>
            <value>name:9001</value>
        </property>
    </configuration>
    ```
3. 配置 hdfs-site.xml
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
            <name>dfs.namenode.http-address</name>
            <value>name:50070</value>
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
4. 配置 workers
    ```bash
    $ sudo vim /usr/bd/hadoop-3.3.1/etc/hadoop/workers
  	```
    ```bash {.line-numbers}
    name
    ```

### 首次启动 Hadoop 系统
1. 清理残留文件
    ```bash
    sudo rm -rf /usr/bd/dfs/data/current /usr/bd/dfs/name/current
    ```
2. 格式化文件系统
    ```bash
    $ hdfs namenode -format
  	```
3. 启动 hadoop
    ```bash
    $ start-dfs.sh
	  ```
4. 查看启动进程
    ```bash
    $ jps
    11424 Jps
    11304 SecondaryNameNode
    10875 NameNode
    11052 DataNode
	  ```
5. 上传数据
    ```bash
    $ hdfs dfs -mkdir /user   
    $ hdfs dfs -mkdir /user/jack   
    $ hdfs dfs -mkdir /user/jack/input   
    $ hdfs dfs -put /usr/bd/hadoop-3.2.2/etc/hadoop/*.xml /user/jack/input
    ```
6. 查看上传数据
    ```bash
    hdfs dfs -ls input/*
    ```
    或者打开网站
    - http://192.168.1.81:50070
    - Utilities -> Browse the file system
    - Browse Directory: /user/jack/input
    - Go!
