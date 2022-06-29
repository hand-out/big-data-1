
## 制作启动脚本

1. 查看系统 start-all.sh 脚本
    ```bash
	$ vim /usr/bd/hadoop-3.3.1/sbin/start-all.sh
    ```
2. 查看系统 stop-all.sh
    ```bash
	$ sudo vim /usr/bd/hadoop-3.3.1/sbin/stop-all.sh
    ```
3. 创建自己的脚本 startall.sh
    ```bash
    $ sudo vim /usr/bd/hadoop-3.3.1/sbin/startall.sh
	```
    ```bash {.line-numbers}
    #!/usr/bin/env bash

    # Start all hadoop daemons.  Run this on master node.

    echo "This script is Deprecated. Instead use start-dfs.sh and start-yarn.sh"

    echo "Starting yarn..."
    start-yarn.sh

    echo "Starting dfs..."
    start-dfs.sh

    echo "Starting historyserver..."
    mr-jobhistory-daemon.sh start historyserver

    jps
    ```
4. 修改权限
    ```bash
	$ sudo chmod 755 /usr/bd/hadoop-3.3.1/sbin/startall.sh
    ``` 
5. 修改所属
    ```bash
	  $ sudo chown 1001:1002 /usr/bd/hadoop-3.3.1/sbin/startall.sh
    ```
6. 执行脚本
    ```bash
	$ startall.sh
    ```
8. 创建自己的脚本 stopall.sh
    ```bash
    $ sudo vim /usr/bd/hadoop-3.2.2/sbin/stopall.sh
	  ```
      ```bash {.line-numbers}
    #!/usr/bin/env bash

    # Stop all hadoop daemons.  Run this on master node.

    echo "This script is Deprecated. Instead use stop-dfs.sh and stop-yarn.sh"

    echo "Stoping historyserver..."
    mr-jobhistory-daemon.sh stop historyserver

    echo "Stoping dfs..."
    stop-dfs.sh

    echo "Stoping yarn..."
    stop-yarn.sh
    ```
9. 修改权限
    ```bash
	$ sudo chmod 755 /usr/bd/hadoop-3.2.2/sbin/stopall.sh
    ``` 
10. 修改所属权
    ```bash
	$ sudo chown 1001:1002 /usr/bd/hadoop-3.2.2/sbin/stopall.sh
    ```
11. 执行脚本
    ```bash
	$ stopall.sh
    ``` 
