
## Hadoop 的源起

Doug Cutting 想要开发一款软件，类似于 Google 的搜索引擎，能广泛用于个人和企业。于是，用 Java 写了一个开源的搜索引擎，后被 Apache 基金会确认为其子项目 Lucene。

1. Doug Cutting 开创的开源软件，用 Java 书写代码，实现与 Google 类似的全文搜索功能，它提供了全文检索引擎的架构，包括完整的查询引擎和索引引擎。
2. 早期发布在个人网站和 SourceForge，2001 年年底成为 Apache 软件基金会 Jakarta 的一个子项目。
3. Lucene 的目的是为软件开发人员提供一个简单易用的工具包，以方便的在目标系统中实现全文检索的功能，或者是以此为基础建立起完整的全文检索引擎。
4. 对于大数量的场景，Lucene 面对与 Google 同样的困难，迫使 Doug Cutting 学习和模仿 Google 解决这些问题的办法。
5. 于是再写一个类似 Google 的微缩版：Nutch。

Nutch 中学习了 Google 技术，形成了自成系统的 Hadoop。

1. 2003-2004 年，Google 公开了部分 GFS 和 Mapreduce 思想的细节，以此为基础 Doug Cutting 等人用了 2 年的业余时间实现了 DFS 和 Mapreduce 机制，使 Nutch 性能飙升。
2. Yahoo 招安了 Doug Cutting 及其项目。
3. Hadoop 于 2005 年秋天作为 Lucene 的子项目 Nutch 的一部分正式引入 Apache 基金会。2006 年 3 月份，Map-Reduce 和 Nutch Distributed File System (NDFS) 分别被纳入称为 Hadoop 的项目中。
4. Hadoop 这个名字来源于 Doug Cutting 儿子的玩具大象。

目前 Hadoop 达到的高度包括：

1. 是实现云计算的事实标准的开源软件
2. 包含数十个具有强大生命力的子项目
3. 已经能在数千节点上运行，处理数据量和排序时间不断打破世界纪录

Hadoop 子项目家族见下图 [@file:intro16]：

![Intro 16](images/01-intro16.jpg){#fig:intro16}
