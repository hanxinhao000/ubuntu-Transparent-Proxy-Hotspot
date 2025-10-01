
# ubuntu-Transparent-Proxy-Hotspot
## 此仓库只是展示在ubuntu上怎么使用自己的ap 网卡创建一个热点的透明代理

## 1.购买AP WIFI设备
使用兼容linux的 WIFI AP设备 最好是免驱的
我购买的是 Dual Band USB Adapter 无线网卡
## 2.安装ubuntu Server
此过程不再赘述，自行下载安装即可
## 3.安装驱动
首先 使用lsusb
我的是：
Bus 001 Device 005: ID 0bda:c811 Realtek Semiconductor Corp. 802.11ac NIC

然后 使用此命令

 lsmod | grep rtl

我的驱动是这个
https://github.com/brektrou/rtl8821CU
使用这个安装完成即可
## 4.下载clash 和 create_ap

create_ap:
https://github.com/lakinduakash/linux-wifi-hotspot?tab=readme-ov-file#vpn-hotspot
https://github.com/garywill/linux-router
clash:
https://github.com/nelvko/clash-for-linux-install

然后clash按照提示 开启tun模式，他会有一个网卡信息

比如(可能台机器不一致，开启和关闭之后 然后ifconfig 查看新增的网卡接口)：
Meta: flags=4305<UP,POINTOPOINT,RUNNING,NOARP,MULTICAST>  mtu 9000
        inet 28.0.0.1  netmask 255.255.255.252  destination 28.0.0.1
        inet6 fe80::bc3c:acbc:cb95:ae01  prefixlen 64  scopeid 0x20<link>
        unspec 00-00-00-00-00-00-00-00-00-00-00-00-00-00-00-00  txqueuelen 500  (UNSPEC)
        RX packets 362  bytes 30394 (30.3 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 589  bytes 69032 (69.0 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
然后使用 create_ap创建以下命令

# create_ap wlx90de80f76d82 Meta TEST_AP 123456789 --dhcp-dns 8.8.8.8

wlx90de80f76d82: 是你购买的网卡AP硬件ID，或者是你的机器自带的 WIFI id，这个是变动的，如果不知道，就拔了WIFI USB网卡，然后ifconfig，然后插上，ifconfig,来回看看变动的那个就是了

Meta 是 clash 开的tun模式的虚拟网卡，这个一般也会和机器变动，打开之后不出意外的话，创建的这个热点 就能直接联到科学网了



 
