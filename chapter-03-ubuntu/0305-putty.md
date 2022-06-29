## Putty

[^putty_home]: PuTTY 官网，https://www.chiark.greenend.org.uk/~sgtatham/putty/
[^putty_down]: PuTTY 下载，https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html

官网 [^putty_home] 下载 [^putty_down]putty-64bit-0.76-installer.msi，双击安装：

1. Welcome to the PuTTY
    - Next
2. Destination Folder
    - C:/Program Files/PuTTY/
    - Next
3. Product Features
    - Add shortcut to PuTTY on the Desktop
        - Entire feature will be installed on local hard drive
    - Install
4. 你要允许此应用对你的设备进行更改吗？
    - 是
5. Completed the PuTTY
    - \[ ] View README file
    - Finish

开启 Ubuntu Server 虚拟机 node，然后运行 PuTTY

1. PuTTY Configuration
    - Host Name (or IP address): 192.168.1.81
    - Port: 22
    - Open
2. PuTTY Security Alert
    - Accept
3. 192.168.1.81 - PuTTY
    - login as: jack
    - jack@192.168.1.83's password: 123456
4. jack@node:~

选择粘贴方法

1. 鼠标选中文字即为选择并复制到剪贴板了
2. 光标处鼠标右键即为粘贴

使用 putty 上传文件的方法

1. 进入到 PuTTY 的安装目录 C:\Program Files\PuTTY
2. 地址栏输入 cmd 后按回车，打开 Windows 的终端窗口
3. 通过 pscp.exe 上传文件
    ```batch
    C:\Program Files\PuTTY>pscp readme.txt jack@192.168.1.81:/home/jack
    jack@192.168.1.81's password:
    readme.txt                | 1 kB |   1.5 kB/s | ETA: 00:00:00 | 100%
    ```

免密码链接

1. 复制 SSH 服务器私钥 id_rsa 的内容到 C:\Users\Dawei\.ssh\81.rsa
2. 添加 SSH 服务器公钥 id_rsa.pub 的内容到 authorized_keys
3. 打开 C:\Program Files\PuTTY>puttygen.exe
    - load : C:\Users\Dawei\.ssh\81.rsa 
4. Save private key
    - Are you sure you want to save this key without a passphrase to protect it? > yes
    - C:\Users\Dawei\.ssh\81.ppk
5. 彻底删除 C:\Users\Dawei\.ssh\81.rsa
6. 启动 putty > Session
    - Host Name: 192.168.1.81
    - Port: 22
    - Connection type: SSH
    - Saved sessions: 81
7. Connection > SSH > Auth  
    - Private key file for authertication: C:\Users\Dawei\.ssh\81.ppk
8. Session > save
9. open
