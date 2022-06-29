
# Windows 实验环境

大数据的存储和计算能力给我带来了很多机会，大数据技术值得学习和拥有。本课程假设你是一个 Java 语言的使用者，我们通过 Java 语言编写和运行用于大数据存储和分析的各种程序。具体包括 Map/Reduce 程序，HDFS 文件访问程序，Pig 程序，Hive 程序和 HBASE 程序等，并将数据分析的结果才 R 语言或 Web 的方式进行展示发表。

本课程需要 3~4 台 Ubuntu Server 作为 Hadoop 集群的节点，一台 Windows 计算机用于程序开发。你可以采用任何方法准备在同一网段内的 Ubuntu Server 和 Windows，如准备几台真是的物理机，或者在一台安装了 ESXi 的服务上，部署这些 Ubuntu Server 和 Windows。或者 Windows 是一台笔记本，其他 Ubuntu Server 部署在 ESXi 上。

本课程做两种假设
1. 你只有一台 PC 机或笔记本电脑操作系统恰巧是 Windows，硬件拥有 i5 以上的 CPU，8G 以上的内存，200G 以上的硬盘存储，你可以把那些 Ubuntu Server 部署到 VMWare Workstations 或 Virtual Box 上。本文选择 VMWare Workstations。
2. 你有一台 PC 机或笔记本电脑正在运行 Windows 10 1204 以上版本的操作系统，i5 以上的 CPU，4G 以上的内存，100G 以上的硬盘，可以考虑在 Widnows 10 上安装 WSL 2 ，部署 Ubuntu Server 安装 Docker ，然后通过 Docker 部署 Hadoop 集群。

我们先按第一种方案准备你的个人计算机。
