
## Cluster Run

关于 Hadoop 集群的网络所有节点都在一个网段，万兆网，编程客户端最好也在相同的网段，一般来讲是内部集群。
另外一种场景是，Hadoop 集群在内部万兆网上，向外部网络用户提供客户端编程。
一般的组织方式采用每个节点安装两块网卡，一块网卡是内网，一块网卡是外网。

Hadoop 集群的内外网访问需要每个节点机上安装两块网卡，还需要对 Hadoop 集群的网络进行额外设置。
我们在虚拟机条件下无法实现上述方案。我给大家的解决方案如下：

### 硬件方案

1. 针对只有热点网络的情况，买一个可以接入热点作为外网，带 Wifi 和网络的路由器，然后所有计算机包括 windows 和 Ubuntu 通过 VMware 的桥接模式都接入路由器。
2. 针对有网线接入外网的情况，可以买一个带 WiFi 的普通路由器，然后所有计算机都接入路由器提供的网络
3. 针对只有 Wifi 接入外网的情况，买一个带 Wifi 接入外网的路由器，然后所有计算机都接入路由器提供的网络

购买设备需要认真选择，花钱，费时间。
我们可以考虑采用软件方案。

### 软件方案

1. 设置 VMware 的网络为 Nat 或主机模式均可，建议采用 Nat 模式，保证 VMware 内的虚拟机能够接入外网
2. 在 VMware 内创建虚拟机 Ubuntu1,2,3（作为 Hadoop 集群）
3. 在 VMware 内创建虚拟机 Windows10（作为 Window 客户端）
4. 上述操作系统在相同网段，可以无限制互通
5. 在 VMware 宿主机上可以通过远程桌面访问 VMWare 内的 Windows，进行软件开发和集群使用

### Eclipse 在 Hadoop 集群上运行 MapReduce 程序

有两种方式：

1. 打包成 Jar 复制到 Hadoop 集群 用 hadoop jar 指令来执行
2. 以开发环境作为客户端与 Hadoop 集群进行交互（不仅是数据交互，包括 Map 和 reduce 交互）

### Eclipse 作为客户端与 Hadoop 交互

1. 在 windows 下设置系统环境变量 HADOOP_USER_NAME=jack
2. 修改 C:/windows/system32/drivers/etc/hosts，增加主机解析
  ```
  192.168.1.202 namenode
  192.168.1.203 datanode1
  192.168.1.204 datanode2
  192.168.1.205 datanode3
  ```
1. 官员身份运行 Eclipse
2. 选择工作空间 D:\students\202222022222\bd1\weido
    - Launch
3. File > New > Other ...
4. Select a wizard > Map/Reduce Project
    - Next
5. MapReduce Project
    - Project name: temp.cluster
    - Next
6. Java Settings
    - Finish

编写测试代码

1. Project Explorer > temp.cluster > src > 鼠标右键 > New > Package
2. New Java Package
    - Source folder: temp.cluster/src
    - Name: temp.cluster.max
    - Finish
3. Project Explorer > temp.cluster > src > temp.cluster.max > 鼠标右键 > New > Class
    - Name: MaxTemperature
    - \[x] public static void main(String[] args)
    - Finish
4. Project Explorer > temp.cluster > src > temp.cluster.max > 鼠标右键 > New > Class
    - Name: MaxTemperatureMapper
    - Finish
5. Project Explorer > temp.cluster > src > temp.cluster.max > 鼠标右键 > New > Class
    - Name: MaxTemperatureReducer
    - Finish

4. 在 项目的 src 下创建 hadoop-cluster.xml 集群配置文件
    ```
    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <property>
        <name>hadoop.job.user</name>
        <value>jack</value>
      </property>
      <property>
        <name>fs.defaultFS</name>
        <value>hdfs://namenode:9000</value>
      </property>
      <property>
        <name>mapred.job.tracker</name>
        <value>namenode:9001</value>
      </property>
      <property>
        <name>mapreduce.framework.name</name>
        <value>yarn</value>
      </property>
      <property>
        <name>yarn.resourcemanager.hostname</name>
        <value>namenode</value>
      </property>  
      <property>
        <name>mapreduce.app-submission.cross-platform</name>
        <value>true</value>
      </property> 
      <property>
        <name>yarn.app.mapreduce.am.env</name>
        <value>HADOOP_MAPRED_HOME=/usr/bd/hadoop-3.2.2</value>
      </property>
      <property>
        <name>mapreduce.map.env</name>
        <value>HADOOP_MAPRED_HOME=/usr/bd/hadoop-3.2.2</value>
      </property>
      <property>
        <name>mapreduce.reduce.env</name>
        <value>HADOOP_MAPRED_HOME=/usr/bd/hadoop-3.2.2</value>
      </property>
      <property>
        <name>mapred.jar</name>
        <value>E:/student/202222022222/bd1/wedo/mapred.temp.max/dist/temperature.jar</value>
      </property>
    </configuration>

    ```
5. 修改 MaxTemperature.java
```
package mapred.temp.max;

import java.net.URI;

import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Job;
import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;

public class MaxTemperature {
	
    static {
        try {
            System.load("D:/students/202222022222/bd1/idea/hadoop-3.2.2/bin/hadoop.dll");
        } catch (UnsatisfiedLinkError e) {
          System.err.println("Native code library failed to load.\n" + e);
          System.exit(1);
        }
    }
	
    public static void main(String[] args) throws Exception {
        Configuration conf=new Configuration();
        conf.addResource("hadoop-cluster.xml");

        String[] otherArgs=new String[]{"temp","tempout"};
        if(otherArgs.length!=2){
            System.err.println("Usage:Temperature <in> <out>");
            System.exit(2);
        }

        Path in = new Path(otherArgs[0]);
        Path out = new Path(otherArgs[1]);
        FileSystem fileSystem = FileSystem.get(new URI(in.toString()), conf);
        if (fileSystem.exists(out)) {
              fileSystem.delete(out, true);
        }

        Job job = Job.getInstance(conf,"Temperature");
        job.setJarByClass(MaxTemperature.class);

        job.setMapperClass(MaxTemperatureMapper.class);
        job.setReducerClass(MaxTemperatureReducer.class);

        job.setOutputKeyClass(Text.class);
        job.setOutputValueClass(IntWritable.class);

        FileInputFormat.addInputPath(job,in);
        FileOutputFormat.setOutputPath(job,out);

    
        System.exit(job.waitForCompletion(true) ? 0 : 1);
    }

}

```
6. 在项目空间 temp 下建立文件夹 dist
7. 鼠标右键项目名 temp > properties
8. Java Compiler
  - Enable project specific settings
  - Compiler compliance level: 1.8
  - Apply and Close
9. 鼠标右键项目名 temp > Export...
10. Select > Java > Runnable JAR file
  - Next
11. Runnable JAR file Specification
  - Launch configurations: MaxTemperature - temp
  - Export destination: temp\dist\temp.jar
  - Package required libraries into generated JAR
  - Finish
12. 鼠标右键项目名 temp > Run As > Run on Hadoop
13. Select Java Application
  - Matching items: MaxTemperature - mapred.temp.max
  - OK
14. 等待结果或调试
