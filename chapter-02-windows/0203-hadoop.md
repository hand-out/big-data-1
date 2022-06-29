
## Hadoop

官网 [^hadoop_home] 下载 [^hadoop_down] Hadoop 发行包 hadoop-3.3.1.tar.gz 到 D:/students/20211202/bd1/tool 文件夹下。

以 **管理员身份** 运行 WinRAR 解压软件，将 hadoop-3.3.1.tar.gz 解压到 D:/students/20211202/bd1/idea 下。

1. Win+d 返回桌面：此电脑 > 鼠标右键 > 属性
2. 设置：关于 > 高级系统设置
3. 系统属性：高级 > 环境变量
4. 环境变量：系统变量 > 新建
5. 新建系统变量：
    - 变量名：HADOOP_HOME
    - 浏览目录
    - 变量值： D:/students/20211202/bd1/idea/hadoop-3.3.1
    - 确定
6. 环境变量：系统变量 > Path
    - 编辑
7. 编辑环境变量：新建
    - %HADOOP_HOME%
    - %HADOOP_HOME%/bin
    - 确定
8. 环境变量：确定
9. 系统属性：确定
10. 设置：关闭

6. 修改 D:/students/20211202/bd1/idea/hadoop-3.3.1/etc/hadoop/hadoop-env.cmd
    ```batch
    set JAVA_HOME=C:/Progra~1/Java/jdk-11.0.13
    ```
1. Win+x > 运行
2. 运行： 
    - 打开： cmd
    - 确定
3. 查看 path 环境变量命令：`path`
4. 查看全部环境变量命令：`set`
5. 检查 Hadoop 安装配置是否正确命令：
    ```
    hadoop
    hadoop -version
    ```

[^hadoop_home]: Hadoop 官网，[https://hadoop.apache.org/](https://hadoop.apache.org/)
[^hadoop_down]: Hadoop 下载，[https://hadoop.apache.org/releases.html](https://hadoop.apache.org/releases.html)
