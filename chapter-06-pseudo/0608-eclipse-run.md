
## Eclipse 远程数据本地执行

启动 Hadoop
```
start-yarn.sh
start-dfs.sh
```

1. 官员身份运行 Eclipse
2. 选择工作空间 D:\students\202222022222\bd1\weido
    - Launch
3. File > New > Other ...
4. Select a wizard > Map/Reduce Project
    - Next
5. MapReduce Project
    - Project name: temp.pseudo
    - Next
6. Java Settings
    - Finish

编写测试代码

1. Project Explorer > temp.windows > src > 鼠标右键 > New > Package
2. New Java Package
    - Source folder: temp.pseudo/src
    - Name: temp.pseudo.max
    - Finish
3. Project Explorer > temp.windows > src > temp.windows.max > 鼠标右键 > New > Class
    - Name: MaxTemperature
    - \[x] public static void main(String[] args)
    - Finish
4. Project Explorer > temp.windows > src > temp.windows.max > 鼠标右键 > New > Class
    - Name: MaxTemperatureMapper
    - Finish
5. Project Explorer > temp.windows > src > temp.windows.max > 鼠标右键 > New > Class
    - Name: MaxTemperatureReducer
    - Finish

5. Define Hadoop location > Advanced parameters （需要先 Run As on Hadoop 一次）
    - dfs.client.use.datanode.hostname=true
    - Finish

1. Project Explorer > DFS Locations > willow > (1) > user > jack > 鼠标右键 
    - Refresh
    - Create new directory...
        - Enter the name of the subfolder = temp
        - OK
    - Refresh
2. Project Explorer > DFS Locations > willow > (1) > user > jack > temp > 鼠标右键
    - Upload files to DFS...
    - Refresh
3. Project Explorer >  temp > 鼠标右键 > Run As > Run Configurations...
4. Run Configurations > Java Application > MaxTemperature > Arguments 
    - Program arguments = hdfs://namenode:9000/user/jack/temp hdfs://namenode:9000/user/jack/tempout
    - Close
5. src > hdfs-site.xml
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
            <name>dfs.client.use.datanode.hostname</name>
            <value>true</value>
        </property>
        <property>
            <name>dfs.permissions</name>
            <value>false</value>
        </property>
    </configuration>
    ```
6. src > log4j.properites
    ```
    hadoop.root.logger=INFO,console
    hadoop.log.dir=.
    hadoop.log.file=hadoop.log

    # Define the root logger to the system property "hadoop.root.logger".
    log4j.rootLogger=${hadoop.root.logger}, EventCounter

    # Logging Threshold
    log4j.threshold=ALL

    # Null Appender
    log4j.appender.NullAppender=org.apache.log4j.varia.NullAppender

    #
    # Rolling File Appender - cap space usage at 5gb.
    #
    hadoop.log.maxfilesize=256MB
    hadoop.log.maxbackupindex=20
    log4j.appender.RFA=org.apache.log4j.RollingFileAppender
    log4j.appender.RFA.File=${hadoop.log.dir}/${hadoop.log.file}

    log4j.appender.RFA.MaxFileSize=${hadoop.log.maxfilesize}
    log4j.appender.RFA.MaxBackupIndex=${hadoop.log.maxbackupindex}

    log4j.appender.RFA.layout=org.apache.log4j.PatternLayout

    # Pattern format: Date LogLevel LoggerName LogMessage
    log4j.appender.RFA.layout.ConversionPattern=%d{ISO8601} %p %c: %m%n
    # Debugging Pattern format
    #log4j.appender.RFA.layout.ConversionPattern=%d{ISO8601} %-5p %c{2} (%F:%M(%L)) - %m%n

    #
    # Daily Rolling File Appender
    #

    log4j.appender.DRFA=org.apache.log4j.DailyRollingFileAppender
    log4j.appender.DRFA.File=${hadoop.log.dir}/${hadoop.log.file}

    # Rollover at midnight
    log4j.appender.DRFA.DatePattern=.yyyy-MM-dd

    log4j.appender.DRFA.layout=org.apache.log4j.PatternLayout

    # Pattern format: Date LogLevel LoggerName LogMessage
    log4j.appender.DRFA.layout.ConversionPattern=%d{ISO8601} %p %c: %m%n
    # Debugging Pattern format
    #log4j.appender.DRFA.layout.ConversionPattern=%d{ISO8601} %-5p %c{2} (%F:%M(%L)) - %m%n

    #
    # console
    # Add "console" to rootlogger above if you want to use this
    #

    log4j.appender.console=org.apache.log4j.ConsoleAppender
    log4j.appender.console.target=System.err
    log4j.appender.console.layout=org.apache.log4j.PatternLayout
    log4j.appender.console.layout.ConversionPattern=%d{ISO8601} %p %c{2}: %m%n

    #
    # TaskLog Appender
    #
    log4j.appender.TLA=org.apache.hadoop.mapred.TaskLogAppender

    log4j.appender.TLA.layout=org.apache.log4j.PatternLayout
    log4j.appender.TLA.layout.ConversionPattern=%d{ISO8601} %p %c: %m%n

    #
    # HDFS block state change log from block manager
    #
    # Uncomment the following to log normal block state change
    # messages from BlockManager in NameNode.
    #log4j.logger.BlockStateChange=DEBUG

    #
    #Security appender
    #
    hadoop.security.logger=INFO,NullAppender
    hadoop.security.log.maxfilesize=256MB
    hadoop.security.log.maxbackupindex=20
    log4j.category.SecurityLogger=${hadoop.security.logger}
    hadoop.security.log.file=SecurityAuth-${user.name}.audit
    log4j.appender.RFAS=org.apache.log4j.RollingFileAppender
    log4j.appender.RFAS.File=${hadoop.log.dir}/${hadoop.security.log.file}
    log4j.appender.RFAS.layout=org.apache.log4j.PatternLayout
    log4j.appender.RFAS.layout.ConversionPattern=%d{ISO8601} %p %c: %m%n
    log4j.appender.RFAS.MaxFileSize=${hadoop.security.log.maxfilesize}
    log4j.appender.RFAS.MaxBackupIndex=${hadoop.security.log.maxbackupindex}

    #
    # Daily Rolling Security appender
    #
    log4j.appender.DRFAS=org.apache.log4j.DailyRollingFileAppender
    log4j.appender.DRFAS.File=${hadoop.log.dir}/${hadoop.security.log.file}
    log4j.appender.DRFAS.layout=org.apache.log4j.PatternLayout
    log4j.appender.DRFAS.layout.ConversionPattern=%d{ISO8601} %p %c: %m%n
    log4j.appender.DRFAS.DatePattern=.yyyy-MM-dd

    #
    # hadoop configuration logging
    #

    # Uncomment the following line to turn off configuration deprecation warnings.
    # log4j.logger.org.apache.hadoop.conf.Configuration.deprecation=WARN

    #
    # hdfs audit logging
    #
    hdfs.audit.logger=INFO,NullAppender
    hdfs.audit.log.maxfilesize=256MB
    hdfs.audit.log.maxbackupindex=20
    log4j.logger.org.apache.hadoop.hdfs.server.namenode.FSNamesystem.audit=${hdfs.audit.logger}
    log4j.additivity.org.apache.hadoop.hdfs.server.namenode.FSNamesystem.audit=false
    log4j.appender.RFAAUDIT=org.apache.log4j.RollingFileAppender
    log4j.appender.RFAAUDIT.File=${hadoop.log.dir}/hdfs-audit.log
    log4j.appender.RFAAUDIT.layout=org.apache.log4j.PatternLayout
    log4j.appender.RFAAUDIT.layout.ConversionPattern=%d{ISO8601} %p %c{2}: %m%n
    log4j.appender.RFAAUDIT.MaxFileSize=${hdfs.audit.log.maxfilesize}
    log4j.appender.RFAAUDIT.MaxBackupIndex=${hdfs.audit.log.maxbackupindex}

    #
    # NameNode metrics logging.
    # The default is to retain two namenode-metrics.log files up to 64MB each.
    #
    namenode.metrics.logger=INFO,NullAppender
    log4j.logger.NameNodeMetricsLog=${namenode.metrics.logger}
    log4j.additivity.NameNodeMetricsLog=false
    log4j.appender.NNMETRICSRFA=org.apache.log4j.RollingFileAppender
    log4j.appender.NNMETRICSRFA.File=${hadoop.log.dir}/namenode-metrics.log
    log4j.appender.NNMETRICSRFA.layout=org.apache.log4j.PatternLayout
    log4j.appender.NNMETRICSRFA.layout.ConversionPattern=%d{ISO8601} %m%n
    log4j.appender.NNMETRICSRFA.MaxBackupIndex=1
    log4j.appender.NNMETRICSRFA.MaxFileSize=64MB

    #
    # DataNode metrics logging.
    # The default is to retain two datanode-metrics.log files up to 64MB each.
    #
    datanode.metrics.logger=INFO,NullAppender
    log4j.logger.DataNodeMetricsLog=${datanode.metrics.logger}
    log4j.additivity.DataNodeMetricsLog=false
    log4j.appender.DNMETRICSRFA=org.apache.log4j.RollingFileAppender
    log4j.appender.DNMETRICSRFA.File=${hadoop.log.dir}/datanode-metrics.log
    log4j.appender.DNMETRICSRFA.layout=org.apache.log4j.PatternLayout
    log4j.appender.DNMETRICSRFA.layout.ConversionPattern=%d{ISO8601} %m%n
    log4j.appender.DNMETRICSRFA.MaxBackupIndex=1
    log4j.appender.DNMETRICSRFA.MaxFileSize=64MB

    # Custom Logging levels

    #log4j.logger.org.apache.hadoop.mapred.JobTracker=DEBUG
    #log4j.logger.org.apache.hadoop.mapred.TaskTracker=DEBUG
    #log4j.logger.org.apache.hadoop.hdfs.server.namenode.FSNamesystem.audit=DEBUG

    # AWS SDK & S3A FileSystem
    #log4j.logger.com.amazonaws=ERROR
    log4j.logger.com.amazonaws.http.AmazonHttpClient=ERROR
    #log4j.logger.org.apache.hadoop.fs.s3a.S3AFileSystem=WARN

    #
    # Event Counter Appender
    # Sends counts of logging messages at different severity levels to Hadoop Metrics.
    #
    log4j.appender.EventCounter=org.apache.hadoop.log.metrics.EventCounter

    #
    # Job Summary Appender
    #
    # Use following logger to send summary to separate file defined by
    # hadoop.mapreduce.jobsummary.log.file :
    # hadoop.mapreduce.jobsummary.logger=INFO,JSA
    # 
    hadoop.mapreduce.jobsummary.logger=${hadoop.root.logger}
    hadoop.mapreduce.jobsummary.log.file=hadoop-mapreduce.jobsummary.log
    hadoop.mapreduce.jobsummary.log.maxfilesize=256MB
    hadoop.mapreduce.jobsummary.log.maxbackupindex=20
    log4j.appender.JSA=org.apache.log4j.RollingFileAppender
    log4j.appender.JSA.File=${hadoop.log.dir}/${hadoop.mapreduce.jobsummary.log.file}
    log4j.appender.JSA.MaxFileSize=${hadoop.mapreduce.jobsummary.log.maxfilesize}
    log4j.appender.JSA.MaxBackupIndex=${hadoop.mapreduce.jobsummary.log.maxbackupindex}
    log4j.appender.JSA.layout=org.apache.log4j.PatternLayout
    log4j.appender.JSA.layout.ConversionPattern=%d{ISO8601} %p %c{2}: %m%n
    log4j.logger.org.apache.hadoop.mapred.JobInProgress$JobSummary=${hadoop.mapreduce.jobsummary.logger}
    log4j.additivity.org.apache.hadoop.mapred.JobInProgress$JobSummary=false

    #
    # shuffle connection log from shuffleHandler
    # Uncomment the following line to enable logging of shuffle connections
    # log4j.logger.org.apache.hadoop.mapred.ShuffleHandler.audit=DEBUG

    #
    # Yarn ResourceManager Application Summary Log
    #
    # Set the ResourceManager summary log filename
    yarn.server.resourcemanager.appsummary.log.file=rm-appsummary.log
    # Set the ResourceManager summary log level and appender
    yarn.server.resourcemanager.appsummary.logger=${hadoop.root.logger}
    #yarn.server.resourcemanager.appsummary.logger=INFO,RMSUMMARY

    # To enable AppSummaryLogging for the RM,
    # set yarn.server.resourcemanager.appsummary.logger to
    # <LEVEL>,RMSUMMARY in hadoop-env.sh

    # Appender for ResourceManager Application Summary Log
    # Requires the following properties to be set
    #    - hadoop.log.dir (Hadoop Log directory)
    #    - yarn.server.resourcemanager.appsummary.log.file (resource manager app summary log filename)
    #    - yarn.server.resourcemanager.appsummary.logger (resource manager app summary log level and appender)

    log4j.logger.org.apache.hadoop.yarn.server.resourcemanager.RMAppManager$ApplicationSummary=${yarn.server.resourcemanager.appsummary.logger}
    log4j.additivity.org.apache.hadoop.yarn.server.resourcemanager.RMAppManager$ApplicationSummary=false
    log4j.appender.RMSUMMARY=org.apache.log4j.RollingFileAppender
    log4j.appender.RMSUMMARY.File=${hadoop.log.dir}/${yarn.server.resourcemanager.appsummary.log.file}
    log4j.appender.RMSUMMARY.MaxFileSize=256MB
    log4j.appender.RMSUMMARY.MaxBackupIndex=20
    log4j.appender.RMSUMMARY.layout=org.apache.log4j.PatternLayout
    log4j.appender.RMSUMMARY.layout.ConversionPattern=%d{ISO8601} %p %c{2}: %m%n

    # Appender for viewing information for errors and warnings
    yarn.ewma.cleanupInterval=300
    yarn.ewma.messageAgeLimitSeconds=86400
    yarn.ewma.maxUniqueMessages=250
    log4j.appender.EWMA=org.apache.hadoop.yarn.util.Log4jWarningErrorMetricsAppender
    log4j.appender.EWMA.cleanupInterval=${yarn.ewma.cleanupInterval}
    log4j.appender.EWMA.messageAgeLimitSeconds=${yarn.ewma.messageAgeLimitSeconds}
    log4j.appender.EWMA.maxUniqueMessages=${yarn.ewma.maxUniqueMessages}

    # Log levels of third-party libraries
    log4j.logger.org.apache.commons.beanutils=WARN
    ```
6. Project Explorer > temp >src > temp.mr > MaxTemperature.java > 鼠标右键
    - Run As > Run on Hadoop
