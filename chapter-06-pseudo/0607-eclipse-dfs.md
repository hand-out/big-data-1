
## Eclipse 浏览 Hadoop 文件系统 DFS

### 启动 Hadoop 文件系统

```
start-dfs.sh
jps
```

### 修改 hosts

1. 修改 C:\Windows\System32\drivers\etc\hosts，添加域名
    - 210.47.218.170  namenode

### 启动 Eclipse

1. Window > Show View > Other...
2. Show View > MapReduce Tools > Map/Reduce Locations
    - Open
3. Map/Reduce Locations
    - 点击 大象 图标
4. Define Hadoop location > General
    - Location name: willow
    - Map/Reduce(V2) Master
        - Host: namenode
        - Port: 9001
    - DFS Master
        - \[x] Use M/R Master host
        - Host: namenode
        - Port: 9000
    - User name: jack
    - Finish
5. Project Explorer
    - DFS Locations > willow > (1) > user > jack 
6. Project Explorer > DFS Locations > willow > (1) > user > jack > 鼠标右键
    - Download from DFS...
    - Create new directory...
    - Upload files to DFS...
    - Upload directory to DFS...
    - Refresh
    - Delete
