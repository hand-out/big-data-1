
## Temperature

1. 官员身份运行 Eclipse
2. 选择工作空间 D:\students\202222022222\bd1\weido
    - Launch
3. File > New > Other ...
4. Select a wizard > Map/Reduce Project
    - Next
5. MapReduce Project
    - Project name: temp.local
    - Next
6. Java Settings
    - Finish

编写测试代码

1. Project Explorer > temp.local > src > 鼠标右键 > New > Package
2. New Java Package
    - Source folder: temp.local/src
    - Name: temp.local.max
    - Finish
3. Project Explorer > temp.local > src > temp.local.max > 鼠标右键 > New > Class
    - Name: MaxTemperature
    - \[x] public static void main(String[] args)
    - Finish
4. Project Explorer > temp.local > src > temp.local.max > 鼠标右键 > New > Class
    - Name: MaxTemperatureMapper
    - Finish
5. Project Explorer > temp.local > src > temp.local.max > 鼠标右键 > New > Class
    - Name: MaxTemperatureReducer
    - Finish

设置 Java 的编译级别

1. Project Explorer > temp > 鼠标右键 > Properties
2. Properties for temp > Java Compiler 
    - \[x] Enable project specific settings 
    - Compiler compliance level: 11
    - Apply and Close
3. Compiler Settings Changed
    - Yes

编译并打包部署文件

1. Project Explorer > temp > 鼠标右键 > New > Folder
2. New Folder
    - Folder name: dist
1. Project Explorer > temp > Export...
2. Export > Java > Runnable JAR file
    - Next
3. Runnable JAR File Specification
    - Launch configuration: MaxTemperature - temp
    - Export destination: temp/dist/temp.jar
    - \(x) Package required libraries into generated JAR
    - Finish

PowerShell 上传 temp.jar

1. win+x > Windows PowerShell
2. 准备
    ```
    d:
    cd .\students\20211202\bd1\works\temp\dist\
    scp .\temp.jar jack@192.168.1.81:/home/jack/
    cd ../input
    scp .\temp.txt jack@192.168.1.81:/home/jack/
    ```

putty 登录 Ubuntu Server

1. 进入家目录
    ```
    cd ~
    ls
    ```
2. Ubuntu Server Hadoop 本地执行
    ```
    hadoop jar temp.jar temp.txt temp
    cat temp/*
    ```
