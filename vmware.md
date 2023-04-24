# VMWare配置虚拟机

一、VMWare安装
...

二、centOS虚拟机安装
- 下载centos系统
- 安装

三、配置centOS
- 固定ip配置
  - 确认vmware网络模式，网络适配器选择NAT模式
  - 确认宿主机网络适配器开启
  - 配置网卡
    - vim /etc/sysconfig/network-scripts/ifcfg-ens33
    - 新增
    ```bash
    IPADDR=192.168.204.141  # ipv4地址
    NETMASK=255.255.255.0  # 子网掩码
    GATEWAY=192.168.204.2  # 网关
    DNS1=192.168.204.2  # dns服务器
    # 参考宿主机vmware-vmnet8配置，保证子网掩码一致
    ```
    - 修改
    ```
    BOOTPROTO="static"  # 固定ip模式
    ```
    - 重启网络服务
    ```
    systemctl restart network
    ```
    - 验证网络
    - 若不确定掩码、网关等信息，在虚拟机创建完毕后没执行下列命令，获取当前自动分配的网络配置进行配置
    ```
    nmcli device show <interface>  # nmcli device show ens33
    
    # 如下
    GENERAL.DEVICE:                         ens33
    GENERAL.TYPE:                           ethernet
    GENERAL.HWADDR:                         00:0C:29:AF:DD:63
    GENERAL.MTU:                            1500
    GENERAL.STATE:                          100 (connected)
    GENERAL.CONNECTION:                     ens33
    GENERAL.CON-PATH:                       /org/freedesktop/NetworkManager/ActiveConnectio
    WIRED-PROPERTIES.CARRIER:               on
    IP4.ADDRESS[1]:                         192.168.204.135/24
    IP4.GATEWAY:                            192.168.204.2
    IP4.ROUTE[1]:                           dst = 192.168.204.0/24, nh = 0.0.0.0, mt = 100
    IP4.ROUTE[2]:                           dst = 0.0.0.0/0, nh = 192.168.204.2, mt = 100
    IP4.DNS[1]:                             192.168.204.2
    IP6.ADDRESS[1]:                         fe80::290:e7dc:ebce:8709/64
    IP6.ADDRESS[2]:                         fe80::1931:56ac:cd5b:36ce/64
    IP6.ADDRESS[3]:                         fe80::d04c:423c:a0e1:65f7/64
    IP6.GATEWAY:                            --
    IP6.ROUTE[1]:                           dst = fe80::/64, nh = ::, mt = 100
    IP6.ROUTE[2]:                           dst = ff00::/8, nh = ::, mt = 256, table=255
    ```
