
## 网络配置

1. 对每个节点复查或配置 cloud.cfg
    ```bash
    $ sudo vim /etc/cloud/cloud.cfg
    ```
    ```bash {.line-numbers}
    preserve_hostname: true
    ```
2. 分别修改每个节点的主机名 name,node1,node2,node3,...
	```bash
	$ sudo vim /etc/hostname
	```
3. 查看每个节点的网卡信息
    ```bash
	$ ifconfig
	```
4. 配置每个节点的 IP 地址 192.168.1.81,91,92,93,...
    ```bash
	$ sudo vim /etc/netplan/00-installer-config.yaml
	```
    ```yaml {.line-numbers}
    # This is the network config written by 'subiquity'
    network:
      ethernets:
        ens33:
          addresses: [192.168.1.9x/24]
          gateway4: 192.168.1.254
          dhcp4: true
          optional: true
      version: 2
    ```
5. 应用每个节点的网卡配置
    ```bash
	$ sudo netplan apply
	```
6. 查看每个节点的网络配置是否生效
    ```bash
	$ ifconfig
	```
7. 为每个节点配置本地域名
    ```bash
    $ sudo vim /etc/hosts
    ```
    ```bash {.line-numbers}
    127.0.0.1 localhost
    #127.0.1.1  node0

    192.168.1.81 name
    192.168.1.91 node1
    192.168.1.92 node2
    192.168.1.93 node3

    # The following lines are desirable for IPv6 capable hosts
    ::1     ip6-localhost ip6-loopback
    fe00::0 ip6-localnet
    ff00::0 ip6-mcastprefix
    ff02::1 ip6-allnodes
    ff02::2 ip6-allrouters
    ```
8. 为每个节点配置 DNS 解析
    ```bash
    $ sudo vim /etc/systemd/resolved.conf
    ```
    ```bash {.line-numbers}
    [Resolve]
    DNS=210.47.208.8 210.47.208.6 114.114.114.114
    #FallbackDNS=
    #Domains=
    #LLMNR=no
    #MulticastDNS=no
    #DNSSEC=no
    #Cache=yes
    #DNSStubListener=yes
    ```
9. 检查域名解析
    ```bash
    $ ping www.baidu.com
    ```
    按 Ctrl+c 结束
10. 重新启动系统
    ```bash
    $ sudo reboot
    ```