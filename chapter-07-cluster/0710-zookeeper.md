## Zookeeper

1. 官网下载 apache-zookeeper-3.8.0-bin.tar.gz
    - sudo wget https://dlcdn.apache.org/zookeeper/zookeeper-3.8.0/apache-zookeeper-3.8.0-bin.tar.gz
2. sudo tar -zxvf apache-zookeeper-3.8.0-bin.tar.gz
3. sudo mv apache-zookeeper-3.8.0-bin /usr/bd
4. sudo mkdir /usr/bd/zoo

### 单机模式

1. cd /usr/bd/apache-zookeeper-3.8.0-bin/conf/
2. sudo cp zoo_sample.cfg zoo.cfg
3. sudo vim zoo.cfg
    ```
    tickTime=2000
    initLimit=10
    syncLimit=5
    dataDir=/usr/bd/data
    clientPort=2181
    ```
4. cd ..
5. sudo ./bin/zkServer.sh start
6. sudo ./bin/zkServer.sh status

### 伪分布模式

zookeeper01

sudo tar -zxvf apache-zookeeper-3.8.0-bin.tar.gz
sudo mv apache-zookeeper-3.8.0-bin /usr/bd/zookeeper01
cd /usr/bd/zookeeper01
sudo mkdir data
sudo vim data/myid
```
0
```
cd /usr/bd/zookeeper01/conf
sudo cp zoo_sample.cfg zoo.cfg
sudo vim zoo.cfg
```
tickTime=2000
initLimit=10
syncLimit=5
dataDir=/usr/bd/zookeeper01/data
clientPort=2181
server.0=namenode:2888:3888
server.1=namenode:4888:5888
server.2=namenode:6888:7888
4lw.commands.whitelist=*
```                                
cd /usr/bd/zookeeper01/bin
sudo ./zkCli.sh
    - create /appconfig "My Config"
    - create /appconfig/hosts 192.168.1.81
    - Ctrl+c
sudo ./zkServer.sh start

zookeeper02

sudo tar -zxvf apache-zookeeper-3.8.0-bin.tar.gz
sudo mv apache-zookeeper-3.8.0-bin /usr/bd/zookeeper02
cd /usr/bd/zookeeper02
sudo mkdir data
sudo vim data/myid
```
1
```
cd /usr/bd/zookeeper02/conf/
sudo cp zoo_sample.cfg zoo.cfg
sudo vim zoo.cfg
```
tickTime=2000
initLimit=10
syncLimit=5
dataDir=/usr/bd/zookeeper02/data
clientPort=2182
server.0=namenode:2888:3888
server.1=namenode:4888:5888
server.2=namenode:6888:7888
4lw.commands.whitelist=*
```                                
cd /usr/bd/zookeeper01/bin
sudo ./zkCli.sh
    - create /appconfig "My Config"
    - create /appconfig/hosts 192.168.1.81
    - Ctrl+c
sudo ./zkServer.sh start

zookeeper03

sudo tar -zxvf apache-zookeeper-3.8.0-bin.tar.gz
sudo mv apache-zookeeper-3.8.0-bin /usr/bd/zookeeper03
cd /usr/bd/zookeeper03
sudo mkdir data
sudo vim data/myid
```
2
```
cd /usr/bd/zookeeper03/conf/
sudo cp zoo_sample.cfg zoo.cfg
sudo vim zoo.cfg
```
tickTime=2000
initLimit=10
syncLimit=5
dataDir=/usr/bd/zookeeper03/data
clientPort=2183
server.0=namenode:2888:3888
server.1=namenode:4888:5888
server.2=namenode:6888:7888
4lw.commands.whitelist=*
```                                
cd /usr/bd/zookeeper01/bin
sudo ./zkCli.sh
    - create /appconfig "My Config"
    - create /appconfig/hosts 192.168.1.81
    - Ctrl+c
sudo ./zkServer.sh start

### 集群模式

### zkui

1. cd ~
2. git clone https://github.com/DeemOpen/zkui.git
3. cd zkui
4. mvn clean install
sudo mkdir /usr/bd/zkui
sudo cp config.cfg /usr/bd/zkui
 sudo cp target/zkui-2.0-SNAPSHOT-jar-with-dependencies.jar /usr/bd/zkui/zkui.jar
cd /usr/bd/zkui
sudo vim config.cfg
```
zkServer=namenode:2181,namenode:2182,namenode:2183
```
cd /usr/bd/zkui
sudo  java -jar zkui.jar
http://192.168.1.81:9090/
    - username: admin
    - password: manager
    - username: appconfig
    - password: appconfig

### zabbix

[^zookeeper_home]: https://zookeeper.apache.org/
[^zookeeper_down]: https://zookeeper.apache.org/releases.html
