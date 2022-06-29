
## 系统环境准备

1. 系统查新操作
    ```bash
    $ sudo apt-get update   
    $ sudo apt-get upgrade
    ```
2. 安装或更新 ssh 客户端程序。SSH(Secure Shell) 安全外壳协议。
    ```bash
    $ sudo apt-get install ssh
    ```
3. rsync 是 linux 系统下的数据镜像备份工具。Remote Sync 可以远程同步，支持本地复制，或者与其他 SSH、rsync 主机同步。
    ```bash
    $ sudo apt-get install rsync
    ```
4. wget 是一个从网络上自动下载文件的自由工具，支持通过 HTTP、HTTPS、FTP 三个最常见的 TCP/IP 协议下载，并可以使用 HTTP 代理。"wget"这个名称来源于“World Wide Web”与“get”的结合。
所谓自动下载是指 wget 可以在用户退出系统之后在后台继续执行，直到下载任务完成。
    ```bash
    $ sudo apt-get install wget
    ```
5. tree 生成目录树
    ```bash
    $ sudo apt-get install tree
    ```
6. vim 编辑器
    ```bash
    $ sudo apt-get install vim
    ```
vim 的简单使用方法

1. vim 启动后一般会停留在“浏览”状态，此时只能看，不能改
2. 在浏览状态按`i`键进入编辑状态，屏幕下端出现`---INSERT---`提示信息
3. 退出编辑状态按`Esc`键
4. 在浏览状态按`:`键，就是`shift+;`组合键，进入命令状态
5. 在命令状态键入`wq`两个字母表示存盘并退出
6. 在命令状态键入`q!`表示强制退出
