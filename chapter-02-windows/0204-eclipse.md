
## Eclipse

官网 [^eclipse_home] 下载 [^eclipse_down] Eclipse IDE for Enterprise Java and Web Developers 发行包 eclipse-jee-2021-12-R-win32-x86_64.zip 到 D:/tudents/20211202/bd1/tool 文件夹下。 

1. 鼠标右键 eclipse-jee-2021-12-R-win32-x86_64.zip 解压到当前文件夹下。 
2. 移动解压好的文件夹 eclipse 到 D:/students/20211202/bd1/idea 下。
3. 进入文件夹 D:/students/20211202/bd1/idea/eclipse，鼠标左键双击 eclipse.exe，等待。..
4. Select a directory as workspace
    - Workspace: D:/students/20211202/bd1/works
    - Launch
5. 关闭 Welcome
6. 关闭 Eclipse

在 Eclipse 下管理 Hadoop 文件和进行 Map/Reduce 项目开发需要安装 Eclipse 插件 Hadoop-eclipse-plugin。 可以从 [^eclipse_hadoop3x_home] 下载该插件的源码后根据 Hadoop 的不同版本动态编译需要的 Hadoop-eclipse-plugin 插件版本。具体的编译过程见附录 [@sec:C1]。

直接从 [^eclipse_hadoop3x_down] 下载编译后的插件 hadoop-eclipse-plugin-2.6.0.jar, 从 [^winutils_home] 下载 [^winutils_down] winutils.exe 和 hadoop.dll 到文件夹 D:/students/20211202/bd1/tool 下。

1. 复制 winutils.exe 和 hadoop.dll 到 D:/students/20211202/bd1/idea/hadoop-3.3.1/bin 下
2. 复制 hadoop.dll 到 C:\Windows\System32
2. 复制 hadoop-eclipse-plugin-2.6.0.jar 到 D:/students/20211202/bd1/idea/eclipse/plugins
3. 双击 eclipse.exe 启动 Eclipse 
4. Project Explorer 出现 DFS Locations
5. Window > Preferences
6. Preferences > Hadoop Map/Reduce
    - Hadoop installation directory: D:/students/20211202/bd1/idea/hadoop-3.3.1
    - Apply and Close
7. Window > Perspective > Open Perspective > Other...
8. Open Perspective > Map/Reduce
    - Open
9. Eclipse 右下方出现 Map/Reduce Locations 视图

[^eclipse_home]: Eclipse 官网，[https://www.eclipse.org/](https://www.eclipse.org/)
[^eclipse_down]: Eclipse 下载，[https://www.eclipse.org/downloads/packages/](https://www.eclipse.org/downloads/packages/)

[^eclipse_hadoop3x_home]: eclipse-hadoop3x 官网，[https://github.com/Woooosz/eclipse-hadoop3x](https://github.com/Woooosz/eclipse-hadoop3x)
[^eclipse_hadoop3x_down]: eclipse-hadoop3x 下载，[https://github.com/Woooosz/eclipse-hadoop3x/tree/master/release](https://github.com/Woooosz/eclipse-hadoop3x/tree/master/release)

[^winutils_home]: winutils 官网，[https://github.com/cdarlint/winutils](https://github.com/cdarlint/winutils)
[^winutils_down]: winutils 下载，[https://github.com/cdarlint/winutils/tree/master/hadoop-3.2.2/bin](https://github.com/cdarlint/winutils/tree/master/hadoop-3.2.2/bin)

### 过滤

1. Project Explorer > View Menu > Filters and Customization...
    - \[ ] .* resources
    -OK
    
### Git 

1. Window > Preferences > Version Control (Team) > Git
    - Default repository folder: D:\students\202222022222\bd1\repos\git
    - \[x] Use SSH agent for SSH connections
    - Default SSH agent: Pageant
    - Apply and Close
