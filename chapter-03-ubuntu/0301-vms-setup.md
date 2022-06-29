## 安装 VMware WorkStation

官网 [^vmwp_home] 下载 [^vmwp_down] VMware Workstation Pro 试用版 VMware-workstation-full-16.2.1-18811642.exe

鼠标双击 VMware-workstation-full-16.2.1-18811642.exe 安装开始安装。

1. 你要允许此应用对你的设备进行更改吗？
    - 是
2. 欢迎使用 VMware Workstation Pro 安装向导
    - 下一步
3. 最终用户许可协议
    - \[x] 我接受许可协议中的条款
    - 下一步
4. 自定义安装
    - 安装位置： C:/Program Files (x86)/VMware/VMware Workstation/
    - \[x] 增强型键盘驱动程序
    - \[x] 将 VMware Workstation 控制台工具添加到系统 PATH
    - 下一步
5. 用户体验设置
    - \[x] 启动时检查产品更新
    - \[ ] 加入 VMware 客户体验提升计划
    - 下一步
6. 快捷方式
    - \[x] 桌面
    - \[x] 开始菜单程序文件夹
    - 下一步
7. 已准备好安装 VMware Workstation Pro
    - 安装
8. VMware Workstation Pro 安装向导已完成
    - 许可证
9. 输入许可证秘钥
    - ZF3R0-FHED2-M80TY-8QYGC-NPKYF
    - 输入
10. VMware Workstation Pro 安装向导已完成
    - 完成
11. 您必须重新启动系统，对 VMware Workstation 进行的配置更改才能生效。
    - 是

[^vmwp_home]: VMware Workstation Pro 官网，[https://www.vmware.com/cn/products/workstation-pro.html](https://www.vmware.com/cn/products/workstation-pro.html)
[^vmwp_down]: VMware Workstation Pro 下载，[https://www.vmware.com/cn/products/workstation-pro/workstation-pro-evaluation.html](https://www.vmware.com/cn/products/workstation-pro/workstation-pro-evaluation.html)

### 支持嵌套虚拟化

此平台不支持虚拟化的 intel vt-x/ept 问题的解决。

1. 取消 Hyper-V 服务
2. 打开服务管理，禁止 HV 主机服务 (HvHost)
3. 以管理员身份启动 PowerShell
    - bcdedit /set hypervisorlaunchtype off
4. 重新启动电脑

Esxi 服务器虚拟化嵌套（？待实验）
1. esxi 启动 ssh server
2. ssh 链接 esxi
3. vi /etc/vmware/config
    - vhv.enable = "TRUE"
    - vhv.allow = "TRUE"
4. 重启 Esxi
