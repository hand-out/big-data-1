
## Hadoop 的架构

Hadoop 的整体架构包括网络系统和节点系统两个部分。节点系统包括管理节点 Namenode 和 JobTacker（可部署在一台计算机），每个工作节点包括 DataNode 和 TaskTracker 两个工作分工。[@flg:intro17]

![Intro 17](images/01-intro17.jpg){#fig:intro17}

###  Namenode

Namenode 的主要工作包括：

1. HDFS 的守护程序
2. 记录文件是如何分割成数据块的，以及这些数据块被存储到哪些节点上
3. 对内存和 I/O 进行集中管理
4. 是个单点，发生故障将使集群崩溃

Namenode 的部署位置见下图 [@fig:intro18]：

![Intro 18](images/01-intro18.jpg){#fig:intro18}

### Secondary Namenode

Secondary Namenode 的主要工作包括：

1. 监控 HDFS 状态的辅助后台程序
2. 每个集群都有一个
3. 与 NameNode 进行通讯，定期保存 HDFS 元数据快照
4. 当 NameNode 故障可以作为备用 NameNode 使用

Secondary Namenode 的部署架构见下图 [@fig:intro19]：

![Intro 19](images/01-intro19.jpg){#fig:intro19}

### DataNode

DataNode 的主要工作包括：

1. 每台从服务器都运行一个
2. 负责把 HDFS 数据块读写到本地文件系统

DataNode 的工作架构见下图 [@fig:intro20]：

![Intro 20](images/01-intro20.jpg){#fig:intro20}

### JobTracker

JobTracker 的主要工作包括：

1. 用于处理作业（用户提交代码）的后台程序
2. 决定有哪些文件参与处理，然后切割 task 并分配节点
3. 监控 task，重启失败的 task（于不同的节点）
4. 每个集群只有唯一一个 JobTracker，位于 Master 节点

JobTracker 的部署架构见下图 [@fig:intro21]：

![Intro 21](images/01-intro21.jpg){#fig:intro21}

### TaskTracker

TaskTracker 的主要工作包括：

1. 位于 slave 节点上，与 datanode 结合（代码与数据一起的原则）
2. 管理各自节点上的 task（由 jobtracker 分配）
3. 每个节点只有一个 tasktracker，但一个 tasktracker 可以启动多个 JVM，用于并行执行 map 或 reduce 任务
4. 与 jobtracker 交互

TaskTracker 的部署架构见下图 [@fig:intro22]：

![Intro 22](images/01-intro22.jpg){#fig:intro22}

### Master 与 Slave

Master 和 Slave 的具体分工包括：

1. Master：Namenode、Secondary Namenode、Jobtracker。浏览器（用于观看管理界面），其它 Hadoop 工具
2. Slave：Tasktracker、Datanode
3. Master 不是唯一的

Master 和 Slave 的结构分工见下图 [@fig:intro23]：

![Intro 23](images/01-intro23.jpg){#fig:intro23}
