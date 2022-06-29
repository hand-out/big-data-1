## Hadoop Eclipse Plugin

### Ant

1. 下载 apache-ant-1.10.10-bin.zip 到 D:\students\202121010428\bd1\tools 文件夹下 
2. 解压 apache-ant-1.10.10-bin.zip 到当前文件夹
3. 移动文件夹 apache-ant-1.10.10 到 D:\students\202121010428\bd1\devenv\下
4. 创建 ANT_HOME=D:\students\202121010428\bd1\devenv\apache-ant-1.10.10 系统环境变量
5. 修改系统环境变量 PATH=%PATH%;%ANT_HOME%;%ANT_HOME%\bin
6. 验证ant的安装配置情况
    ```batch
    ant -version
    ```

### eclipse-hadoop3x-master

1. 下载 eclipse-hadoop3x-master.zip 到 D:\students\202121010428\bd1\tools 文件夹下
2. 解压 eclipse-hadoop3x-master.zip 到当前文件夹
3. 移动 eclipse-hadoop3x-master 文件夹到 D:\students\202121010428\bd1\devenv 文件夹下


### 编译过程

1. 进行编译
    ```batch
    cd D:\students\202121010428\bd1\devenv\eclipse-hadoop3x-master\src\contrib\eclipse-plugin
    ant jar -Dversion=3.2.2 -Declipse.home=D:\students\202121010428\bd1\devenv\eclipse -Dhadoop.home=D:\students\202121010428\bd1\devenv\hadoop-3.2.2
    ```
    编译失败
2. 修改eclipse-hadoop3x-master\src\contrib\eclipse-plugin\build.xml
    - 删除`depends="init, ivy-retrieve-common"`
    - 删除`/libexec`
3. 重新编译
    ```batch
    cd D:\students\202121010428\bd1\devenv\eclipse-hadoop3x-master\src\contrib\eclipse-plugin
    ant jar -Dversion=3.2.2 -Declipse.home=D:\students\202121010428\bd1\devenv\eclipse -Dhadoop.home=D:\students\202121010428\bd1\devenv\hadoop-3.2.2
    ```
    编译失败
4. 修改eclipse-hadoop3x-master\ivy\libraries.properties
    - hadoop.version=3.2.2
    - commons-lang.version=3.7
    - netty.version=3.10.6.Final
    - guava.version=27.0-jre
5. 重新编译
    ```batch
    cd D:\students\202121010428\bd1\devenv\eclipse-hadoop3x-master\src\contrib\eclipse-plugin
    ant jar -Dversion=3.2.2 -Declipse.home=D:\students\202121010428\bd1\devenv\eclipse -Dhadoop.home=D:\students\202121010428\bd1\devenv\hadoop-3.2.2
    ```
    编译失败
6. 修改eclipse-hadoop3x-master\src\contrib\eclipse-plugin\build.xml
    - commons-lang- 改为 commons-lang3-
    -commons-lang3-3.4.jar 改为commons-lang3-3.7.jar
7. 重新编译
    ```batch
    cd D:\students\202121010428\bd1\devenv\eclipse-hadoop3x-master\src\contrib\eclipse-plugin
    ant jar -Dversion=3.2.2 -Declipse.home=D:\students\202121010428\bd1\devenv\eclipse -Dhadoop.home=D:\students\202121010428\bd1\devenv\hadoop-3.2.2
    ```
    编译成功

8. 编译成功后
D:\students\202121010428\bd1\devenv\eclipse-hadoop3x-master\build\contrib\eclipse-plugin
生成hadoop-eclipse-plugin-3.2.2.jar
9. 复制hadoop-eclipse-plugin-3.2.2.jar到D:\students\202121010428\bd1\eclipse\plugins 文件夹下
10. 启动eclipse
11. New Hadoop Location... 窗口不能出现
12. 查看D:\students\202121010428\bd1\workspace\.metadata\.log文件
13. 复制D:\students\202121010428\bd1\devenv\hadoop-3.2.2\share\hadoop\common\lib下的所有文件到D:\students\202121010428\bd1\devenv\eclipse-hadoop3x-master\build\contrib\eclipse-plugin\lib下
14. 重新编译
    ```batch
    cd D:\students\202121010428\bd1\devenv\eclipse-hadoop3x-master\src\contrib\eclipse-plugin
    ant jar -Dversion=3.2.2 -Declipse.home=D:\students\202121010428\bd1\devenv\eclipse -Dhadoop.home=D:\students\202121010428\bd1\devenv\hadoop-3.2.2
    ```
    编译成功
15. 复制hadoop-eclipse-plugin-3.2.2.jar到D:\students\202121010428\bd1\eclipse\plugins 文件夹下
16. 启动eclipse
17. New Hadoop Location... 窗口出现
18. hadoop-eclipse-plugin编译成功


### 参考链接
1. ant的官网，https://ant.apache.org/
2. ant下载地址，https://ant.apache.org/bindownload.cgi
5. Apache Hadoop-Eclipse，http://people.apache.org/~srimanth/hadoop-eclipse/
6. hadoop-eclipse-plugin 源代码，https://github.com/Woooosz/eclipse-hadoop3x
7. 在 windows10 下 ant 编译生成 hadoop-eclipse-plugin-3.x 插件
    - https://blog.csdn.net/JJYOLO/article/details/105097582
    - https://www.cnblogs.com/hemomo/p/14441024.html





