
## 关机过程

1. 关闭集群
    ```bash
    $ stopall.sh
    ```
2. 查看集群状态
    - http://192.168.1.81:9870
    - http://192.168.1.81:8088
    - http://192.168.1.81:19888
3. 关闭虚拟机
    ```bash
    $ ssh -t node1 "sudo shutdown -h now"
    $ ssh -t node2 "sudo shutdown -h now"
    $ ssh -t node3 "sudo shutdown -h now"
    ```
4. 关闭 WMware
5. 关闭计算机
