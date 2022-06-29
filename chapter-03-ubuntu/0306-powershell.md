## PowerShell

1. win+x > Windows PowerShell （管理员）
3. ssh 链接
    ```shell
    ssh jack@192.168.1.81 -p 22
    ```
3. Are you sure you want to continue connecting (yes/no[fingerprint])?
    - yes
4. jack@192.168.1.81's passsword: 123456

退出 PowerShell 的 ssh 链接状态

1. 从 Windows 到 Linux
    ```shell
    PS C:/Windows/system32> scp D:/students/20211202/bd1/works/temp/input/temp.txt jack@192.168.1.81:/home/jack
    jack@192.168.1.81's password:
    temp.txt                                                                      100%  535   190.9KB/s   00:00
    PS C:/Windows/system32>
    ```
2. 从 Linux 到 Windows
    ```shell
    PS D:/tmp> scp jack@192.168.1.81:/home/jack/temp.txt D:/students/20211202/bd1/works/temp/input/data.txt
    jack@192.168.1.81's password:
    temp.txt                                                                   100%  535   263.1KB/s   00:00
    ```

选择粘贴方法

1. 鼠标左键选中，鼠标右键复制
2. 光标处鼠标右键即为粘贴
