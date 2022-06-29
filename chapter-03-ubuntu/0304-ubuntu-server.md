## Ubuntu Server

官网 [^ubuntu_server_home] 下载 [^ubuntu_server_down] ubuntu-20.04.3-live-server-amd64.iso 到 D:/students/20211202/bd1/tool 

启动 VMware Workstation 应用程序

1. 库 > 我的计算机 > node
2. node > 编辑虚拟机设置
3. 虚拟机设置 >  硬件 > CD/DVD (SATA)
    - \[x] 启动时连接
    - (x) 使用 ISO 映像文件：D:/students/20211202/bd1/tool/ubuntu-20.04.3-live-server-amd64.iso
4. 虚拟机设置 > 硬件 > 网络适配器
    - \[x] 启动时连接
    - (x) 桥接模式 (B): 直接连接到物理网络
5. 确定
6. node > 开启此虚拟机

安装 Ubuntu Server 的过程如下：上下箭头移动选项，空格选择，回车确定

1. select your language
    - English
2. Installer update available
    - Update to the new installer
4. Keyboard configuration
    - Done
5. Network connections
    - Done
6. Configure proxy
    - Done
7. Configure Ubuntu archive mirror
    - Done
8. Guided storage configuration
    - (x) Use an entire disk
    - \[ ] Set up this disk as an LVM group
    - Done
9. Storage configuration
    - Done
10. Confirm destructive action
    - Continue
11. Profile setup
    - Your name: Jack Ma
    - Your server's name: node
    - Pick a username: jack
    - Choose a password: 123456
    - Done
12. SSH Setup
    - \[x] Install OpenSSH server
    - Done
13. Featured Server Snaps
    - Done
14. Installing system
15. Install complete
    - Reboot Now
16. Please remove the installation medium, then press ENTER:
17. 登录 Ubuntu
    - node login: jack
    - Password: 123456

首次登录后的基本操作：

1. 安装网络工具
    ```bash
    $ sudo apt install net-tools
    ```
2. 查看网卡信息
    ```bash
    $ ifconfig
    ```
3. 修改 IP 地址
    ```bash
    $ sudo vim /etc/netplan/00-installer-config.yaml
    ```
    按 i 键，进入编辑模式
    ``` bash {.line-numbers}
    network:
      ethernets:
        ens33:
          addresses: [192.168.1.81/24]
          gateway4: 192.168.1.254
          dhcp4: true
          optional: true
      version: 2
    ```
    按 Esc 键退出编辑模式
    按：键等待输入命令
    输入 wq 命令存盘退出
4. 使修改后的 IP 地址生效
    ```bash
    $ sudo netplan apply
    $ ifconfig
    ```
5. 关闭 Ubuntu
    ```bash
    $ sudo shutdown -h now
    ```

[^ubuntu_server_home]: Ubuntu 官网，[https://ubuntu.com/](https://ubuntu.com/)
[^ubuntu_server_down]: Ubuntu 下载，[https://ubuntu.com/download/server](https://ubuntu.com/download/server)
