# Linux 常用命令及使用方法

## 系统信息

1. 显示机器的处理器架构 (1)
    ```bash
    $ arch
    ```
2. 显示机器的处理器架构 (2)
    ```bash
    $ uname -m
    ```
3. 显示正在使用的内核版本
    ```bash
    $ uname -r
    ```
4. 显示硬件系统部件 - (SMBIOS / DMI)
    ```bash
    $ dmidecode -q
    ```
5. 罗列一个磁盘的架构特性
    ```bash
    $ hdparm -i /dev/hda
    ```
6. 在磁盘上执行测试性读取操作
    ```bash
    $ hdparm -tT /dev/sda
    ```
7. 显示 CPU info 的信息
    ```bash
    $ cat /proc/cpuinfo
    ```
8. 显示中断
    ```bash
    $ cat /proc/interrupts
    ```
9. 校验内存使用
    ```bash
    $ cat /proc/meminfo
    ```
10. 显示哪些 swap 被使用
    ```bash
    $ cat /proc/swaps
    ```
11. 显示内核的版本
    ```bash
    $ cat /proc/version
    ```
12. 显示网络适配器及统计
    ```bash
    $ cat /proc/net/dev
    ```
13. 显示已加载的文件系统
    ```bash
    $ cat /proc/mounts
    ```
14. 罗列 PCI 设备
    ```bash
    $ lspci -tv
    ```
15. 显示 USB 设备
    ```bash
    $ lsusb -tv
    ```
16. 显示系统日期
    ```bash
    $ date
    ```
17. 显示 2007 年的日历表
    ```bash
    $ cal 2007
    ```
18. 设置日期和时间 - 月日时分年。秒
    ```bash
    $ date 041217002007.00
    ```
19. 将时间修改保存到 BIOS
    ```bash
    $ clock -w
    ```

## 系统的关机、重启、登出

1. 关闭系统 (1)
    ```bash
    $ shutdown -h now
    ```
2. 关闭系统 (2)
    ```bash
    $ init 0
    ```
3. 关闭系统 (3)
    ```bash
    $ telinit 0
    ```
4. 按预定时间关闭系统
    ```bash
    $ shutdown -h hours:minutes &
    ```
5. 取消按预定时间关闭系统
    ```bash
    $ shutdown -c
    ```
6. 重启 (1)
    ```bash
    $ shutdown -r now
    ```
7. 重启 (2)
    ```bash
    $ reboot
    ```
8. 注销
    ```bash
    $ logout
    ```

## 文件和目录

1. 进入 '/ home' 目录'
    ```bash
    $ cd /home
    ```
2. 返回上一级目录
    ```bash
    $ cd ..
    ```
3. 返回上两级目录
    ```bash
    $ cd ../..
    ```
4. 进入个人的主目录
    ```bash
    $ cd
    ```
5. 进入个人的主目录
    ```bash
    $ cd ~user1
    ```
6. 返回上次所在的目录
    ```bash
    $ cd -
    ```
7. 显示工作路径
    ```bash
    $ pwd
    ```
8. 查看目录中的文件
    ```bash
    $ ls
    ```
9. 查看目录中的文件
    ```bash
    $ ls -F
    ```
10. 显示文件和目录的详细资料
    ```bash
    $ ls -l
    ```
11. 显示隐藏文件
    ```bash
    $ ls -a
    ```
12. 显示包含数字的文件名和目录名
    ```bash
    $ ls *[0-9]*
    ```
13. 显示文件和目录由根目录开始的树形结构 (1)
    ```bash
    $ tree
    ```
14. 显示文件和目录由根目录开始的树形结构 (2)
    ```bash
    $ lstree
    ```
15. 创建一个叫做 'dir1' 的目录'
    ```bash
    $ mkdir dir1
    ```
16. 同时创建两个目录
    ```bash
    $ mkdir dir1 dir2
    ```
17. 创建一个目录树
    ```bash
    $ mkdir -p /tmp/dir1/dir2
    ```
18. 删除一个叫做 'file1' 的文件'
    ```bash
    $ rm -f file1
    ```
19. 删除一个叫做 'dir1' 的目录'
    ```bash
    $ rmdir dir1
    ```
20. 删除一个叫做 'dir1' 的目录并同时删除其内容
    ```bash
    $ rm -rf dir1
    ```
21. 同时删除两个目录及它们的内容
    ```bash
    $ rm -rf dir1 dir2
    ```
22. 重命名/移动 一个目录
    ```bash
    $ mv dir1 new_dir
    ```
23. 复制一个文件
    ```bash
    $ cp file1 file2
    ```
24. 复制一个目录下的所有文件到当前工作目录
    ```bash
    $ cp dir/* .
    ```
25. 复制一个目录到当前工作目录
    ```bash
    $ cp -a /tmp/dir1 .
    ```
26. 复制一个目录
    ```bash
    $ cp -a dir1 dir2
    ```
27. 创建一个指向文件或目录的软链接
    ```bash
    $ ln -s file1 lnk1
    ```
28. 创建一个指向文件或目录的物理链接
    ```bash
    $ ln file1 lnk1
    ```
29. 修改一个文件或目录的时间戳 - (YYMMDDhhmm)
    ```bash
    $ touch -t 0712250000 file1
    ```
30. outputs the mime type of the file as text
    ```bash
    $ file file1
    ```
31. 列出已知的编码
    ```bash
    $ iconv -l
    ```
32. creates a new from the given input file by assuming it is encoded in fromEncoding and converting it to toEncoding.
    ```bash
    $ iconv -f fromEncoding -t toEncoding inputFile > outputFile
    ```
33. batch resize files in the current directory and send them to a thumbnails directory (requires convert from Imagemagick)
    ```bash
    $ find . -maxdepth 1 -name *.jpg -print -exec convert "{}" -resize 80x60 "thumbs/{}" \;
    ```

## 文件搜索

1. 从 '/' 开始进入根文件系统搜索文件和目录
    ```bash
    $ find / -name file1
    ```
2. 搜索属于用户 'user1' 的文件和目录
    ```bash
    $ find / -user user1
    ```
3. 在目录 '/ home/user1' 中搜索带有'.bin' 结尾的文件
    ```bash
    $ find /home/user1 -name \*.bin
    ```
4. 搜索在过去 100 天内未被使用过的执行文件
    ```bash
    $ find /usr/bin -type f -atime +100
    ```
5. 搜索在 10 天内被创建或者修改过的文件
    ```bash
    $ find /usr/bin -type f -mtime -10
    ```
6. 搜索以 '.rpm' 结尾的文件并定义其权限
    ```bash
    $ find / -name \*.rpm -exec chmod 755 '{}' \;
    ```
7. 搜索以 '.rpm' 结尾的文件，忽略光驱、捷盘等可移动设备
    ```bash
    $ find / -xdev -name \*.rpm
    ```
8. 寻找以 '.ps' 结尾的文件 - 先运行 'updatedb' 命令
    ```bash
    $ locate \*.ps
    ```
9. 显示一个二进制文件、源码或 man 的位置
    ```bash
    $ whereis halt
    ```
10. 显示一个二进制文件或可执行文件的完整路径
    ```bash
    $ which halt
    ```

## 挂载一个文件系统

1. 挂载一个叫做 hda2 的盘 - 确定目录 '/ mnt/hda2' 已经存在
    ```bash
    $ mount /dev/hda2 /mnt/hda2
    ```
2. 卸载一个叫做 hda2 的盘 - 先从挂载点 '/ mnt/hda2' 退出
    ```bash
    $ umount /dev/hda2
    ```
3. 当设备繁忙时强制卸载
    ```bash
    $ fuser -km /mnt/hda2
    ```
4. 运行卸载操作而不写入 /etc/mtab 文件- 当文件为只读或当磁盘写满时非常有用
    ```bash
    $ umount -n /mnt/hda2
    ```
5. 挂载一个软盘
    ```bash
    $ mount /dev/fd0 /mnt/floppy
    ```
6. 挂载一个 cdrom 或 dvdrom
    ```bash
    $ mount /dev/cdrom /mnt/cdrom
    ```
7. 挂载一个 cdrw 或 dvdrom
    ```bash
    $ mount /dev/hdc /mnt/cdrecorder
    ```
8. 挂载一个 cdrw 或 dvdrom
    ```bash
    $ mount /dev/hdb /mnt/cdrecorder
    ```
9. 挂载一个文件或 ISO 镜像文件
    ```bash
    $ mount -o loop file.iso /mnt/cdrom
    ```
10. 挂载一个 Windows FAT32 文件系统
    ```bash
    $ mount -t vfat /dev/hda5 /mnt/hda5
    ```
11. 挂载一个 usb 捷盘或闪存设备
    ```bash
    $ mount /dev/sda1 /mnt/usbdisk
    ```
12. 挂载一个 windows 网络共享
    ```bash
    $ mount -t smbfs -o username=user,password=pass //WinClient/share /mnt/share
    ```

## 磁盘空间

1. 显示已经挂载的分区列表
    ```bash
    $ df -h
    ```
2. 以尺寸大小排列文件和目录
    ```bash
    $ ls -lSr | more
    ```
3. 估算目录'dir1'已经使用的磁盘空间
    ```bash
    $ du -sh dir1
    ```
4. 以容量大小为依据依次显示文件和目录的大小
    ```bash
    $ du -sk * | sort -rn
    ```
5. 以大小为依据依次显示已安装的 rpm 包所使用的空间 (fedora, redhat 类系统）
    ```bash
    $ rpm -q -a --qf '%10{SIZE}t%{NAME}n' | sort -k1,1n
    ```
6. 以大小为依据显示已安装的 deb 包所使用的空间 (ubuntu, debian 类系统）
    ```bash
    $ dpkg-query -W -f='${Installed-Size;10}t${Package}n' | sort -k1,1n
    ```

## 用户和群组

1. 创建一个新用户组
    ```bash
    $ groupadd group_name
    ```
2. 删除一个用户组
    ```bash
    $ groupdel group_name
    ```
3. 重命名一个用户组
    ```bash
    $ groupmod -n new_group_name old_group_name
    ```
4. 创建一个属于 "admin" 用户组的用户
    ```bash
    $ useradd -c "Name Surname " -g admin -d /home/user1 -s /bin/bash user1
    ```
5. 创建一个新用户
    ```bash
    $ useradd user1
    ```
6. 删除一个用户 ( '-r' 排除主目录）
    ```bash
    $ userdel -r user1
    ```
7. 修改用户属性
    ```bash
    $ usermod -c "User FTP" -g system -d /ftp/user1 -s /bin/nologin user1
    ```
8. 修改口令
    ```bash
    $ passwd
    ```
9. 修改一个用户的口令 （只允许 root 执行）
    ```bash
    $ passwd user1
    ```
10. 设置用户口令的失效期限
    ```bash
    $ chage -E 2005-12-31 user1
    ```
11. 检查 '/etc/passwd' 的文件格式和语法修正以及存在的用户
    ```bash
    $ pwck
    ```
12. 检查 '/etc/passwd' 的文件格式和语法修正以及存在的群组
    ```bash
    $ grpck
    ```
13. 登陆进一个新的群组以改变新创建文件的预设群组
    ```bash
    $ newgrp group_name
    ```

## 文件的权限

1. 显示权限	
    ```bash
    $ ls -lh
    ```
2. 将终端划分成 5 栏显示
    ```bash
    $ ls /tmp | pr -T5 -W$COLUMNS
    ```
3. 设置目录的所有人 (u)、群组 (g) 以及其他人 (o) 以读（r ）、写 (w) 和执行 (x) 的权限
    ```bash
    $ chmod ugo+rwx directory1
    ```
4. 删除群组 (g) 与其他人 (o) 对目录的读写执行权限
    ```bash
    $ chmod go-rwx directory1
    ```
5. 改变一个文件的所有人属性
    ```bash
    $ chown user1 file1
    ```
6. 改变一个目录的所有人属性并同时改变改目录下所有文件的属性
    ```bash
    $ chown -R user1 directory1
    ```
7. 改变文件的群组
    ```bash
    $ chgrp group1 file1
    ```
8. 改变一个文件的所有人和群组属性
    ```bash
    $ chown user1:group1 file1
    ```
9. 罗列一个系统中所有使用了 SUID 控制的文件
    ```bash
    $ find / -perm -u+s
    ```
10. 设置一个二进制文件的 SUID 位 - 运行该文件的用户也被赋予和所有者同样的权限
    ```bash
    $ chmod u+s /bin/file1
    ```
11. 禁用一个二进制文件的 SUID 位
    ```bash
    $ chmod u-s /bin/file1
    ```
12. 设置一个目录的 SGID 位 - 类似 SUID ，不过这是针对目录的
    ```bash
    $ chmod g+s /home/public
    ```
13. 禁用一个目录的 SGID 位
    ```bash
    $ chmod g-s /home/public
    ```
14. 设置一个文件的 STIKY 位 - 只允许合法所有人删除文件
    ```bash
    $ chmod o+t /home/public
    ```
15. 禁用一个目录的 STIKY 位
    ```bash
    $ chmod o-t /home/public
    ```

## 文件的特殊属性

1. ``，只允许以追加方式读写文件
    ```bash
    $ chattr +a file1
    ```
2. ``，允许这个文件能被内核自动压缩/解压
    ```bash
    $ chattr +c file1
    ```
3. ``，在进行文件系统备份时，dump 程序将忽略这个文件
    ```bash
    $ chattr +d file1
    ```
4. ``，设置成不可变的文件，不能被删除、修改、重命名或者链接
    ```bash
    $ chattr +i file1
    ```
5. ``，允许一个文件被安全地删除
    ```bash
    $ chattr +s file1
    ```
6. ``，一旦应用程序对这个文件执行了写操作，使系统立刻把修改的结果写到磁盘
    ```bash
    $ chattr +S file1
    ```
7. ``，若文件被删除，系统会允许你在以后恢复这个被删除的文件
    ```bash
    $ chattr +u file1
    ```
8. ``，显示特殊的属性
    ```bash
    $ lsattr
    ```

## 打包和压缩文件

1. 解压一个叫做 'file1.bz2'的文件
    ```bash
    $ bunzip2 file1.bz2
    ```
2. 压缩一个叫做 'file1' 的文件
    ```bash
    $ bzip2 file1
    ```
3. 解压一个叫做 'file1.gz'的文件
    ```bash
    $ gunzip file1.gz
    ```
4. 压缩一个叫做 'file1'的文件
    ```bash
    $ gzip file1
    ```
5. 最大程度压缩
    ```bash
    $ gzip -9 file1
    ```
6. 创建一个叫做 'file1.rar' 的包
    ```bash
    $ rar a file1.rar test_file
    ```
7. 同时压缩 'file1', 'file2' 以及目录 'dir1'
    ```bash
    $ rar a file1.rar file1 file2 dir1
    ```
8. 解压 rar 包
    ```bash
    $ rar x file1.rar
    ```
9. 解压 rar 包
    ```bash
    $ unrar x file1.rar
    ```
10. 创建一个非压缩的 tarball
    ```bash
    $ tar -cvf archive.tar file1
    ```
11. 创建一个包含了 'file1', 'file2' 以及 'dir1'的档案文件
    ```bash
    $ tar -cvf archive.tar file1 file2 dir1
    ```
12. 显示一个包中的内容
    ```bash
    $ tar -tf archive.tar
    ```
13. 释放一个包
    ```bash
    $ tar -xvf archive.tar
    ```
14. 将压缩包释放到 /tmp 目录下
    ```bash
    $ tar -xvf archive.tar -C /tmp
    ```
15. 创建一个 bzip2 格式的压缩包
    ```bash
    $ tar -cvfj archive.tar.bz2 dir1
    ```
16. 解压一个 bzip2 格式的压缩包
    ```bash
    $ tar -xvfj archive.tar.bz2
    ```
17. 创建一个 gzip 格式的压缩包
    ```bash
    $ tar -cvfz archive.tar.gz dir1
    ```
18. 解压一个 gzip 格式的压缩包
    ```bash
    $ tar -xvfz archive.tar.gz
    ```
19. 创建一个 zip 格式的压缩包
    ```bash
    $ zip file1.zip file1
    ```
20. 将几个文件和目录同时压缩成一个 zip 格式的压缩包
    ```bash
    $ zip -r file1.zip file1 file2 dir1
    ```
21. 解压一个 zip 格式压缩包
    ```bash
    $ unzip file1.zip
    ```

### RPM 包 - （Fedora, Redhat 及类似系统）	
1. 安装一个 rpm 包
    ```bash
    $ rpm -ivh package.rpm
    ```
2. 安装一个 rpm 包而忽略依赖关系警告
    ```bash
    $ rpm -ivh --nodeeps package.rpm
    ```
3. 更新一个 rpm 包但不改变其配置文件
    ```bash
    $ rpm -U package.rpm
    ```
4. 更新一个确定已经安装的 rpm 包
    ```bash
    $ rpm -F package.rpm
    ```
5. 删除一个 rpm 包
    ```bash
    $ rpm -e package_name.rpm
    ```
6. 显示系统中所有已经安装的 rpm 包
    ```bash
    $ rpm -qa
    ```
7. 显示所有名称中包含 "httpd" 字样的 rpm 包
    ```bash
    $ rpm -qa | grep httpd
    ```
8. 获取一个已安装包的特殊信息
    ```bash
    $ rpm -qi package_name
    ```
9. 显示一个组件的 rpm 包
    ```bash
    $ rpm -qg "System Environment/Daemons"
    ```
10. 显示一个已经安装的 rpm 包提供的文件列表
    ```bash
    $ rpm -ql package_name
    ```
11. 显示一个已经安装的 rpm 包提供的配置文件列表
    ```bash
    $ rpm -qc package_name
    ```
12. 显示与一个 rpm 包存在依赖关系的列表
    ```bash
    $ rpm -q package_name --whatrequires
    ```
13. 显示一个 rpm 包所占的体积
    ```bash
    $ rpm -q package_name --whatprovides
    ```
14. 显示在安装/删除期间所执行的脚本 l
    ```bash
    $ rpm -q package_name --scripts
    ```
15. 显示一个 rpm 包的修改历史
    ```bash
    $ rpm -q package_name --changelog
    ```
16. 确认所给的文件由哪个 rpm 包所提供
    ```bash
    $ rpm -qf /etc/httpd/conf/httpd.conf
    ```
17. 显示由一个尚未安装的 rpm 包提供的文件列表
    ```bash
    $ rpm -qp package.rpm -l
    ```
18. 导入公钥数字证书
    ```bash
    $ rpm --import /media/cdrom/RPM-GPG-KEY
    ```
19. 确认一个 rpm 包的完整性
    ```bash
    $ rpm --checksig package.rpm
    ```
20. 确认已安装的所有 rpm 包的完整性
    ```bash
    $ rpm -qa gpg-pubkey
    ```
21. 检查文件尺寸、 许可、类型、所有者、群组、MD5 检查以及最后修改时间
    ```bash
    $ rpm -V package_name
    ```
22. 检查系统中所有已安装的 rpm 包- 小心使用
    ```bash
    $ rpm -Va
    ```
23. 确认一个 rpm 包还未安装
    ```bash
    $ rpm -Vp package.rpm
    ```
24. 从一个 rpm 包运行可执行文件
    ```bash
    $ rpm2cpio package.rpm | cpio --extract --make-directories *bin*
    ```
25. 从一个 rpm 源码安装一个构建好的包
    ```bash
    $ rpm -ivh /usr/src/redhat/RPMS/`arch`/package.rpm
    ```
26. 从一个 rpm 源码构建一个 rpm 包
    ```bash
    $ rpmbuild --rebuild package_name.src.rpm
    ```

###  YUM 软件包升级器 - （Fedora, RedHat 及类似系统）	

1. 下载并安装一个 rpm 包
    ```bash
    $ yum install package_name
    ```
2. 将安装一个 rpm 包，使用你自己的软件仓库为你解决所有依赖关系
    ```bash
    $ yum localinstall package_name.rpm
    ```
3. 更新当前系统中所有安装的 rpm 包
    ```bash
    $ yum update package_name.rpm
    ```
4. 更新一个 rpm 包
    ```bash
    $ yum update package_name
    ```
5. 删除一个 rpm 包
    ```bash
    $ yum remove package_name
    ```
6. 列出当前系统中安装的所有包
    ```bash
    $ yum list
    ```
7. 在 rpm 仓库中搜寻软件包
    ```bash
    $ yum search package_name
    ```
8. 清理 rpm 缓存删除下载的包
    ```bash
    $ yum clean packages
    ```
9. 删除所有头文件
    ```bash
    $ yum clean headers
    ```
10. 删除所有缓存的包和头文件
    ```bash
    $ yum clean all
    ```
### DEB 包 (Debian, Ubuntu 以及类似系统）	

1. 安装/更新一个 deb 包
    ```bash
    $ dpkg -i package.deb
    ```
2. 从系统删除一个 deb 包
    ```bash
    $ dpkg -r package_name
    ```
3. 显示系统中所有已经安装的 deb 包
    ```bash
    $ dpkg -l
    ```
4. 显示所有名称中包含 "httpd" 字样的 deb 包
    ```bash
    $ dpkg -l | grep httpd
    ```
5. 获得已经安装在系统中一个特殊包的信息
    ```bash
    $ dpkg -s package_name
    ```
6. 显示系统中已经安装的一个 deb 包所提供的文件列表
    ```bash
    $ dpkg -L package_name
    ```
7. 显示尚未安装的一个包所提供的文件列表
    ```bash
    $ dpkg --contents package.deb
    ```
8. 确认所给的文件由哪个 deb 包提供
    ```bash
    $ dpkg -S /bin/ping
    ```

### APT 软件工具 (Debian, Ubuntu 以及类似系统）	
1. 安装/更新一个 deb 包
    ```bash
    $ apt-get install package_name
    ```
2. 从光盘安装/更新一个 deb 包
    ```bash
    $ apt-cdrom install package_name
    ```
3. 升级列表中的软件包
    ```bash
    $ apt-get update
    ```
4. 升级所有已安装的软件
    ```bash
    $ apt-get upgrade
    ```
5. 从系统删除一个 deb 包
    ```bash
    $ apt-get remove package_name
    ```
6. 确认依赖的软件仓库正确
    ```bash
    $ apt-get check
    ```
7. 从下载的软件包中清理缓存
    ```bash
    $ apt-get clean
    ```
8. 返回包含所要搜索字符串的软件包名称
    ```bash
    $ apt-cache search searched-package
    ```

## 查看文件内容

1. 从第一个字节开始正向查看文件的内容
    ```bash
    $ cat file1
    ```
2. 从最后一行开始反向查看一个文件的内容
    ```bash
    $ tac file1
    ```
3. 查看一个长文件的内容
    ```bash
    $ more file1
    ```
4. 类似于 'more' 命令，但是它允许在文件中和正向操作一样的反向操作
    ```bash
    $ less file1
    ```
5. 查看一个文件的前两行
    ```bash
    $ head -2 file1
    ```
6. 查看一个文件的最后两行
    ```bash
    $ tail -2 file1
    ```
7. 实时查看被添加到一个文件中的内容
    ```bash
    $ tail -f /var/log/messages
    ```

## 文本处理

1. general syntax for text manipulation using PIPE, STDIN and STDOUT
    ```bash
    $ cat file1 file2 ... | command <> file1_in.txt_or_file1_out.txt
    ```
2. 合并一个文件的详细说明文本，并将简介写入一个新文件中
    ```bash
    $ cat file1 | command( sed, grep, awk, grep, etc...) > result.txt
    ```
3. 合并一个文件的详细说明文本，并将简介写入一个已有的文件中
    ```bash
    $ cat file1 | command( sed, grep, awk, grep, etc...) >> result.txt
    ```
4. 在文件 '/var/log/messages'中查找关键词"Aug"
    ```bash
    $ grep Aug /var/log/messages
    ```
5. 在文件 '/var/log/messages'中查找以"Aug"开始的词汇
    ```bash
    $ grep ^Aug /var/log/messages
    ```
6. 选择 '/var/log/messages' 文件中所有包含数字的行
    ```bash
    $ grep [0-9] /var/log/messages
    ```
7. 在目录 '/var/log' 及随后的目录中搜索字符串"Aug"
    ```bash
    $ grep Aug -R /var/log/*
    ```
8. 将 example.txt 文件中的 "string1" 替换成 "string2"
    ```bash
    $ sed 's/stringa1/stringa2/g' example.txt
    ```
9. 从 example.txt 文件中删除所有空白行
    ```bash
    $ sed '/^$/d' example.txt
    ```
10. 从 example.txt 文件中删除所有注释和空白行
    ```bash
    $ sed '/ *#/d; /^$/d' example.txt
    ```
11. 合并上下单元格内容
    ```bash
    $ echo 'esempio' | tr '[&#58;lower&#58;]' '[&#58;upper&#58;]'
    ```
12. 从文件 example.txt 中排除第一行
    ```bash
    $ sed -e '1d' result.txt
    ```
13. 查看只包含词汇 "string1"的行
    ```bash
    $ sed -n '/stringa1/p'
    ```
14. 删除每一行最后的空白字符
    ```bash
    $ sed -e 's/ *$//' example.txt
    ```
15. 从文档中只删除词汇 "string1" 并保留剩余全部
    ```bash
    $ sed -e 's/stringa1//g' example.txt
    ```
16. 查看从第一行到第 5 行内容
    ```bash
    $ sed -n '1,5p;5q' example.txt
    ```
17. 查看第 5 行
    ```bash
    $ sed -n '5p;5q' example.txt
    ```
18. 用单个零替换多个零
    ```bash
    $ sed -e 's/00*/0/g' example.txt
    ```
19. 标示文件的行数
    ```bash
    $ cat -n file1
    ```
20. 删除 example.txt 文件中的所有偶数行
    ```bash
    $ cat example.txt | awk 'NR%2==1'
    ```
21. 查看一行第一栏
    ```bash
    $ echo a b c | awk '{print $1}'
    ```
22. 查看一行的第一和第三栏
    ```bash
    $ echo a b c | awk '{print $1,$3}'
    ```
23. 合并两个文件或两栏的内容
    ```bash
    $ paste file1 file2
    ```
24. 合并两个文件或两栏的内容，中间用"+"区分
    ```bash
    $ paste -d '+' file1 file2
    ```
25. 排序两个文件的内容
    ```bash
    $ sort file1 file2
    ```
26. 取出两个文件的并集（重复的行只保留一份）
    ```bash
    $ sort file1 file2 | uniq
    ```
27. 删除交集，留下其他的行
    ```bash
    $ sort file1 file2 | uniq -u
    ```
28. 取出两个文件的交集（只留下同时存在于两个文件中的文件）
    ```bash
    $ sort file1 file2 | uniq -d
    ```
29. 比较两个文件的内容只删除 'file1' 所包含的内容
    ```bash
    $ comm -1 file1 file2
    ```
30. 比较两个文件的内容只删除 'file2' 所包含的内容
    ```bash
    $ comm -2 file1 file2
    ```
31. 比较两个文件的内容只删除两个文件共有的部分
    ```bash
    $ comm -3 file1 file2
    ```

## 字符设置和文件格式转换

1. 将一个文本文件的格式从 MSDOS 转换成 UNIX
    ```bash
    $ dos2unix filedos.txt fileunix.txt
    ```
2. 将一个文本文件的格式从 UNIX 转换成 MSDOS
    ```bash
    $ unix2dos fileunix.txt filedos.txt
    ```
3. 将一个文本文件转换成 html
    ```bash
    $ recode ..HTML < page.txt > page.html
    ```
4. 显示所有允许的转换格式
    ```bash
    $ recode -l | more
    ```

## 文件系统分析

1. 检查磁盘 hda1 上的坏磁块
    ```bash
    $ badblocks -v /dev/hda1
    ```
2. 修复/检查 hda1 磁盘上 linux 文件系统的完整性
    ```bash
    $ fsck /dev/hda1
    ```
3. 修复/检查 hda1 磁盘上 ext2 文件系统的完整性
    ```bash
    $ fsck.ext2 /dev/hda1
    ```
4. 修复/检查 hda1 磁盘上 ext2 文件系统的完整性
    ```bash
    $ e2fsck /dev/hda1
    ```
5. 修复/检查 hda1 磁盘上 ext3 文件系统的完整性
    ```bash
    $ e2fsck -j /dev/hda1
    ```
6. 修复/检查 hda1 磁盘上 ext3 文件系统的完整性
    ```bash
    $ fsck.ext3 /dev/hda1
    ```
7. 修复/检查 hda1 磁盘上 fat 文件系统的完整性
    ```bash
    $ fsck.vfat /dev/hda1
    ```
8. 修复/检查 hda1 磁盘上 dos 文件系统的完整性
    ```bash
    $ fsck.msdos /dev/hda1
    ```
9. 修复/检查 hda1 磁盘上 dos 文件系统的完整性
    ```bash
    $ dosfsck /dev/hda1
    ```

## 初始化一个文件系统

1. 在 hda1 分区创建一个文件系统
    ```bash
    $ mkfs /dev/hda1
    ```
2. 在 hda1 分区创建一个 linux ext2 的文件系统
    ```bash
    $ mke2fs /dev/hda1
    ```
3. 在 hda1 分区创建一个 linux ext3（日志型）的文件系统
    ```bash
    $ mke2fs -j /dev/hda1
    ```
4. 创建一个 FAT32 文件系统
    ```bash
    $ mkfs -t vfat 32 -F /dev/hda1
    ```
5. 格式化一个软盘
    ```bash
    $ fdformat -n /dev/fd0
    ```
6. 创建一个 swap 文件系统
    ```bash
    $ mkswap /dev/hda3
    ```

## SWAP 文件系统

1. 创建一个 swap 文件系统
    ```bash
    $ mkswap /dev/hda3
    ```
2. 启用一个新的 swap 文件系统
    ```bash
    $ swapon /dev/hda3
    ```
3. 启用两个 swap 分区
    ```bash
    $ swapon /dev/hda2 /dev/hdb3
    ```

## 备份

1. 制作一个 '/home' 目录的完整备份
    ```bash
    $ dump -0aj -f /tmp/home0.bak /home
    ```
2. 制作一个 '/home' 目录的交互式备份
    ```bash
    $ dump -1aj -f /tmp/home0.bak /home
    ```
3. 还原一个交互式备份
    ```bash
    $ restore -if /tmp/home0.bak
    ```
4. 同步两边的目录
    ```bash
    $ rsync -rogpav --delete /home /tmp
    ```
5. 通过 SSH 通道 rsync
    ```bash
    $ rsync -rogpav -e ssh --delete /home ip_address:/tmp
    ```
6. 通过 ssh 和压缩将一个远程目录同步到本地目录
    ```bash
    $ rsync -az -e ssh --delete ip_addr:/home/public /home/local
    ```
7. 通过 ssh 和压缩将本地目录同步到远程目录
    ```bash
    $ rsync -az -e ssh --delete /home/local ip_addr:/home/public
    ```
8. 通过 ssh 在远程主机上执行一次备份本地磁盘的操作
    ```bash
    $ dd bs=1M if=/dev/hda | gzip | ssh user@ip_addr 'dd of=hda.gz'
    ```
9. 备份磁盘内容到一个文件
    ```bash
    $ dd if=/dev/sda of=/tmp/file1
    ```
10. 执行一次对 '/home/user' 目录的交互式备份操作
    ```bash
    $ tar -Puf backup.tar /home/user 
    ```
11. 通过 ssh 在远程目录中复制一个目录内容
    ```bash
    $ ( cd /tmp/local/ && tar c . ) | ssh -C user@ip_addr 'cd /home/share/ && tar x -p'
    ```
12. 通过 ssh 在远程目录中复制一个本地目录
    ```bash
    $ ( tar c /home ) | ssh -C user@ip_addr 'cd /home/backup-home && tar x -p'
    ```
13. 本地将一个目录复制到另一个地方，保留原有权限及链接
    ```bash
    $ tar cf - . | (cd /tmp/backup ; tar xf - )
    ```
14. 从一个目录查找并复制所有以 '.txt' 结尾的文件到另一个目录
    ```bash
    $ find /home/user1 -name '*.txt' | xargs cp -av --target-directory=/home/backup/ --parents
    ```
15. 查找所有以 '.log' 结尾的文件并做成一个 bzip 包
    ```bash
    $ find /var/log -name '*.log' | tar cv --files-from=- | bzip2 > log.tar.bz2
    ```
16. 做一个将 MBR (Master Boot Record) 内容复制到软盘的动作
    ```bash
    $ dd if=/dev/hda of=/dev/fd0 bs=512 count=1
    ```
17. 从已经保存到软盘的备份中恢复 MBR 内容
    ```bash
    $ dd if=/dev/fd0 of=/dev/hda bs=512 count=1
    ```

## 光盘

1. 清空一个可复写的光盘内容
    ```bash
    $ cdrecord -v gracetime=2 dev=/dev/cdrom -eject blank=fast -force
    ```
2. 在磁盘上创建一个光盘的 iso 镜像文件
    ```bash
    $ mkisofs /dev/cdrom > cd.iso
    ```
3. 在磁盘上创建一个压缩了的光盘 iso 镜像文件
    ```bash
    $ mkisofs /dev/cdrom | gzip > cd_iso.gz
    ```
4. 创建一个目录的 iso 镜像文件
    ```bash
    $ mkisofs -J -allow-leading-dots -R -V "Label CD" -iso-level 4 -o ./cd.iso data_cd
    ```
5. 刻录一个 ISO 镜像文件
    ```bash
    $ cdrecord -v dev=/dev/cdrom cd.iso
    ```
6. 刻录一个压缩了的 ISO 镜像文件
    ```bash
    $ gzip -dc cd_iso.gz | cdrecord dev=/dev/cdrom -
    ```
7. 挂载一个 ISO 镜像文件
    ```bash
    $ mount -o loop cd.iso /mnt/iso
    ```
8. 从一个 CD 光盘转录音轨到 wav 文件中
    ```bash
    $ cd-paranoia -B
    ```
9. 从一个 CD 光盘转录音轨到 wav 文件中（参数-3）
    ```bash
    $ cd-paranoia -- "-3"
    ```
10. 扫描总线以识别 scsi 通道
    ```bash
    $ cdrecord --scanbus
    ```
11. 校验一个设备的 md5sum 编码，例如一张 CD
    ```bash
    $ dd if=/dev/hdc | md5sum
    ```

## 网络

1. 显示一个以太网卡的配置
    ```bash
    $ ifconfig eth0
    ```
2. 启用一个 'eth0' 网络设备
    ```bash
    $ ifup eth0
    ```
3. 禁用一个 'eth0' 网络设备
    ```bash
    $ ifdown eth0
    ```
4. 控制 IP 地址
    ```bash
    $ ifconfig eth0 192.168.1.1 netmask 255.255.255.0
    ```
5. 设置 'eth0' 成混杂模式以嗅探数据包 (sniffing)
    ```bash
    $ ifconfig eth0 promisc
    ```
6. 以 dhcp 模式启用 'eth0'
    ```bash
    $ dhclient eth0
    ```
7. show routing table
    ```bash
    $ route -n
    ```
8. configura default gateway
    ```bash
    $ route add -net 0/0 gw IP_Gateway
    ```
9. configure static route to reach network '192.168.0.0/16'
    ```bash
    $ route add -net 192.168.0.0 netmask 255.255.0.0 gw 192.168.1.1
    ```
10. remove static route
    ```bash
    $ route del 0/0 gw IP_gateway
    ```
11. activate ip routing
    ```bash
    $ echo "1" > /proc/sys/net/ipv4/ip_forward
    ```
12. show hostname of system
    ```bash
    $ hostname
    ```
13. lookup hostname to resolve name to ip address and viceversa(1)
    ```bash
    $ host www.example.com
    ```
14. lookup hostname to resolve name to ip address and viceversa(2)
    ```bash
    $ nslookup www.example.com
    ```
15. show link status of all interfaces
    ```bash
    $ ip link show
    ```
16. show link status of 'eth0'
    ```bash
    $ mii-tool eth0
    ```
17. show statistics of network card 'eth0'
    ```bash
    $ ethtool eth0
    ```
18. show all active network connections and their PID
    ```bash
    $ netstat -tup
    ```
19. show all network services listening on the system and their PID
    ```bash
    $ netstat -tupl
    ```
20. show all HTTP traffic
    ```bash
    $ tcpdump tcp port 80
    ```
21. scan show wireless networks
    ```bash
    $ iwlist
    ```
22. show configuration of a wireless network card
    ```bash
    $ iwconfig eth1
    ```
23. show hostname
    ```bash
    $ hostname
    ```
24. lookup hostname to resolve name to ip address and viceversa
    ```bash
    $ host www.example.com
    ```
25. lookup hostname to resolve name to ip address and viceversa
    ```bash
    $ nslookup www.example.com
    ```
26. lookup on Whois database
    ```bash
    $ whois www.example.com
    ```
27. Microsoft Windows networks (SAMBA)
28. netbios name resolution
    ```bash
    $ nbtscan ip_addr
    ```
29. netbios name resolution
    ```bash
    $ nmblookup -A ip_addr
    ```
30. show remote shares of a windows host
    ```bash
    $ smbclient -L ip_addr/hostname
    ```
31. ike wget can download files from a host windows via smb
    ```bash
    $ smbget -Rr smb://ip_addr/share l
    ```
32. mount a windows network share
    ```bash
    $ mount -t smbfs -o username=user,password=pass //WinClient/share /mnt/share
    ```
