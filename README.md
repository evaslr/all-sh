# all-sh 2020-09-01
## 秋水四合一 
wget --no-check-certificate -O shadowsocks-all.sh https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks-all.sh

chmod +x shadowsocks-all.sh

./shadowsocks-all.sh 2>&1 | tee shadowsocks-all.log

卸载：./shadowsocks-all.sh uninstall

启动脚本
启动脚本后面的参数含义，从左至右依次为：启动，停止，重启，查看状态。

Shadowsocks-Python 版：
/etc/init.d/shadowsocks-python start | stop | restart | status

ShadowsocksR 版：
/etc/init.d/shadowsocks-r start | stop | restart | status

Shadowsocks-Go 版：
/etc/init.d/shadowsocks-go start | stop | restart | status

Shadowsocks-libev 版：
/etc/init.d/shadowsocks-libev start | stop | restart | status

各版本默认配置文件
Shadowsocks-Python 版：
/etc/shadowsocks-python/config.json

ShadowsocksR 版：
/etc/shadowsocks-r/config.json

Shadowsocks-Go 版：
/etc/shadowsocks-go/config.json

Shadowsocks-libev 版：
/etc/shadowsocks-libev/config.json

## bbr加速
不卸载内核版本
wget -N "https://github.000060000.xyz/tcpx.sh" && chmod +x tcpx.sh && ./tcpx.sh

卸载内核版本
wget -N "https://github.000060000.xyz/tcp.sh" && chmod +x tcp.sh && ./tcp.sh

支持 Focal Ubuntu 20.04 的一键重装脚本
from https://www.hostloc.com/thread-696865-1-1.html

wget https://github.000060000.xyz/InstallNET.sh && chmod a+x InstallNET.sh && bash InstallNET.sh -u focal -v 64 -a

5.5内核及BBR2内核支持cake队列

双持bbr+锐速
bbr 添加
echo "net.core.default_qdisc=fq" >> /etc/sysctl.conf
echo "net.ipv4.tcp_congestion_control=bbr" >> /etc/sysctl.conf
sysctl -p

编辑锐速文件
nano /appex/etc/config

检测代码有BUG，如果锐速正常 运行查看
bash /appex/bin/lotServer.sh status | grep "LotServer"

检查bbr 内核默认bbr算法不会有输出
lsmod | grep bbr

检查centos安装内核
grubby --info=ALL|awk -F= '$1=="kernel" {print i++ " : " $2}'

查看当前支持TCP算法
cat /proc/sys/net/ipv4/tcp_allowed_congestion_control
查看当前运行的算法
cat /proc/sys/net/ipv4/tcp_congestion_control
查看当前队列算法
sysctl net.core.default_qdisc

命令： uname -a
作用： 查看系统内核版本号及系统名称

命令： cat /proc/version
作用： 查看目录"/proc"下version的信息，也可以得到当前系统的内核版本号及系统名称

真实队列查看？ 更改队列算法可能需要重启生效
tc -s qdisc show

ylx2016与chiakge、cx9208无任何关系
bbsplus算法原作者
https://blog.csdn.net/dog250/article/details/80629551
bbrplus首用名 ？
https://github.com/cx9208/bbrplus
xanmod官网
https://xanmod.org
Zen官网
https://liquorix.net/
锐速
https://moeclub.org/2017/03/09/14/
官方编译好的内核
https://sourceforge.net/projects/xanmod/files/releases/current
https://elrepo.org/linux/kernel/el7/x86_64/RPMS/
https://elrepo.org/linux/kernel/el8/x86_64/RPMS/
https://kernel.ubuntu.com/~kernel-ppa/mainline/
高科技
https://github.com/phlinhng/v2ray-tcp-tls-web
https://github.com/johnrosen1/trojan-gfw-script


## Socat一键安装脚本，可转发TCP和UDP流量
使用root运行以下命令：

wget https://www.moerats.com/usr/shell/socat.sh && bash socat.sh
按要求输入以下信息：

#如果你要用本地服务器的3333端口转发IP为1.1.1.1服务器的6666端口，那就依次填入指定参数。
请输入本地端口:3333
请输入远程端口:6666
请输入远程IP:1.1.1.1
输入后直到配置完成。

删除/etc/rc.local重启即可停止中转


## unlock.sh流媒体解锁
dnsmasq分流详解
一、dnsmasq是什么?
Dnsmasq为小型网络提供网络基础设施：DNS，DHCP，路由器通告和网络引导。它被设计为轻量级且占用空间小，适用于资源受限的路由器和防火墙。它还被广泛用于智能手机和便携式热点的共享，并支持虚拟化框架中的虚拟网络。支持的平台包括Linux（带有glibc和uclibc），Android，* BSD和Mac OS X. Dnsmasq包含在大多数Linux发行版以及FreeBSD，OpenBSD和NetBSD的端口系统中。Dnsmasq提供完整的IPv6支持

本站dnsmasq分流脚本有什么作用？
1.根据系统安装dnsmasq。

2.默认写入netflix相关的规则并指定DNS。

3.修改系统DNS为127.0.0.1，作用是使网络域名解析在dnsmasq上进行。

注意
1.解锁成功后系统DNS应该为127.0.0.1，部分系统会自行重置系统DNS，或重启VPS系统、重启网络相关功能导致系统DNS被重置使DNS解锁失效。

2.可使用chattr -i /etc/resolv.conf && echo "nameserver 127.0.0.1" > /etc/resolv.conf && chattr +i /etc/resolv.conf进行文件加锁，解锁chattr -i /etc/resolv.conf，C7以外的系统加锁会提示错误等信息，自行百度谷歌

3.dnsmasq分流只适用于科学服务端使用系统的DNS。

二、脚本用法。
编号:A2

1.最后DNS为变量,就是需要你自行修改成想用的DNS,格式必须为。

wget https://raw.githubusercontent.com/evaslr/all-sh/master/unlock.sh && chmod +x unlock.sh && ./unlock.sh 8.8.8.8

									
2.已测试过阿里云系统C7、D9、u6。推荐C7，其它两个或多或少有点小问题


									
3.如安装错误，请手动安装，注意报错（百度搜索找寻答案）


								
三、自定义dnsmasq的配置。

									
1.打开vi /etc/dnsmasq.d/unlock.conf。


									
2.按照里面的格式自行添加删除修改。


									
3.修改完成重启dnsmasq。（重启命令systemctl restart dnsmasq）


									
4.最后重启科学服务端


																
四、不再使用dnsmasq。

									
1.只需修改系统DNS为默认即可。


									
2.一般默认为8.8.8.8 8.8.4.4。


									
3.修改完成重启科学服务端

## vps安装系统（甲骨文dd Debian系统）
DD系统
萌咖大佬已经成功测试DD脚本！这样我们比较方便的使用debian系统了！

原系统请选择 ubuntu16 （18系统兼容有一些问题！）

安装debian9脚本 (-firmware 额外驱动支持)

1
bash <(wget --no-check-certificate -qO- 'https://moeclub.org/attachment/LinuxShell/InstallNET.sh') -d 9 -v 64 -p 'RUYO' -a -firmware

DD成功后，请使用root登录！

账号: root

密码:RUYO
