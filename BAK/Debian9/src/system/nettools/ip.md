
深度服务器操作系统中管理员用户可使用ip、dhclient、route三个工具程序对ip进行管理。
 
ip工具程序
ip命令用来显示或操纵Linux主机的路由、网络设备、策略路由和隧道，是Linux下较新的功能强大的网络配置工具。特别的，不赞成使用的linux网络命令有 arp, ifconfig, iptunnel,nameif, netstat, route。这些程序包含在net-tools软件包，但该软件包已经多年不被维护了。他们中的许多基本功能能够用iproute2软件包中一些套件替代，其中最著名的就是新的ip命令。下面我们先介绍ip的语法，再介绍ip与上述命令的对比。

ip的一般用法
ip [OPTIONS] OBJECT [COMMAND | help] 
 
其中，OPTIONS是一些修改ip行为或者改变其输出的选项，其常用参数请参见表1.4。
 
表1.4 ip命令OPTION选项参数说明
短参数
长参数
参数说明
-V
-version
显示指令版本信息
-s
-stats,-statistics
输出更详细的信息
-f
-family
强制使用指定的协议族
-4
 
指定使用的网络层协议是IPv4协议
-6
 
指定使用的网络层协议是IPv6协议
-0
 
输出信息每条记录输出一行，即使内容较多也不换行显示
-r
-resolve
显示主机时，不使用IP地址，而使用主机的域名。
 
 
而OBJECT是要管理或者获取信息的对象，其常用对象请参见表1.5。
 
 
 
表1.5 ip命令认识的对象
短参数
长参数
参数说明
address
 
一个设备的协议（IP或IPv6）地址
link
 
网络设备
route
 
路由表条目
rule
 
路由策略数据库中的规则
neighbour
 
ARP或者NDISC缓冲区条目
 
 
网络命令对比
表1.6 网络管理的其他命令与ip命令对比
其他网络命令
等效的ip命令
arp
ip n (ip neighbor)
ifconfig
ip a (ip addr)
iptunnel
ip tunnel
nameif
ip link
netstat
ss, ip route (for netstat-r), ip -s link (for netstat -i), ip maddr (for netstat -g)
 
route
ip r (ip route)
 
 
表1.7 arp vs ip
arp命令
等效的ip命令
arp -a [host] or --all [host]
显示指定主机或指定ip地址的条目
ip n (or ip neighbor), or ip n show
arp -d [ip_addr] or --delete [ip_addr]
移除指定主机的arp缓存条目
ip n del [ip_addr] (this “invalidates” neighbor entries)

.ip n f [ip_addr] (or ip n flush [ip_addr])
arp -i [int] or --device [int]
e.g.
arp -i eth0 -s 10.21.31.41 A321.ABCF.321A creates a static ARP entry associating IP address 10.21.31.41 with MAC address A321.ABCF.321A on eth0.
ip n [add | chg | del | repl] dev [name]
arp -s [ip_addr] [hw_addr] or --set [ip_addr]
创建一个静态的arp地址对指定的ip主机
ip n add [ip_addr] lladdr [mac_address] dev [device] nud [nud_state] (见下面实例)
arp -v
使用verbose模式显示更多细节
ip -s n (or ip -stats n)
 
e.g.
# ip n del 10.1.2.3 dev eth0
Invalidates the ARP cache entry for host 10.1.2.3 on device eth0.
# ip neighbor show dev eth0
Shows the ARP cache for interface eth0.
# ip n add 10.1.2.3 lladdr 1:2:3:4:5:6 dev eth0 nud perm
Adds a “permanent” ARP cache entry for host 10.1.2.3 device eth0. 
 
表1.8 ifconfig vs ip
ifconfig命令
等效的ip命令
ifconfig
ip a (or ip addr)
ifconfig [interface]
ip a show dev [interface]
ifconfig [address_family]
ip -f [family] a
Ifconfig [interface] add [address/prefixlength
 
Adds an IPv6 address to the [interface].
ip a add [ip_addr/mask] dev [interface]
ifconfig [interface] address [address]
ip a add [ip_addr/mask] dev [interface]
ifconfig [interface] allmulti or -allmulti
ip mr iif [name] or ip mroute iif [name]
ifconfig [interface] arp or -arp
ip link set arp on or arp off
ifconfig [interface] broadcast [address]
ip a add broadcast [ip_address]
.
ip link set dev [interface] broadcast [mac_address]
ifconfig [interface] del [address/prefixlength]
ip a del [ipv6_addr or ipv4_addr] dev [interface]
ifconfig [interface] down
ip link set dev [interface] address [mac_addr]
ifconfig [interface] mtu [n]
ip link set dev [interface] mtu [n]
ifconfig [interface] multicast
ip link set dev [interface] multicast on or off
ifconfig [interface] promisc or -promisc
ip link set dev [interface] promisc on or off
ifconfig [interface] txquelen [n]
.
Sets the transmit queue length on the [interface]. Smaller values are recommended for connections with high latency (i.e., dial-up modems, ISDN, etc).
ip link set dev [interface] txqueuelen [n] or txqlen [n]
ifconfig [interface] tunnel [address]
ip tunnel mode sit 
ifconfig [interface] up
ip link set [interface] up
ip命令用法实例如下：
# ip link show dev eth0
# ip a add 10.11.12.13/8 dev eth0
# ip link set dev eth0 up
# ip link set dev eth0 mtu 1500
# ip link set dev eth0 address 00:70:b7:d6:cd:ef
 
 
表1.9 iptunnel vs ip tunnel
iptunnel命令
等效的ip命令
iptunnel [add | change | del | show]
ip tunnel a or add
ip tunnel chg or change
ip tunnel d or del
ip tunnel ls or show
iptunnel add [name] [mode {ipip | gre | sit} ] 
remote [remote_addr] local [local_addr]
ip tunnel add [name] [mode {ipip | gre | sit | isatap | ip6in6 | ipip6 | any }]
 remote [remote_addr] local [local_addr]
Iptunnel和ip tunnel用法实例如下
# [iptunnel | ip tunnel] add ipip-tunl1 mode ipip remote 83.240.67.86 (ipip-tunl1 is the name of the tunnel, 83.240.67.86 is the IP address of the remote endpoint).

# [iptunnel | ip tunnel] add ipi-tunl2 mode ipip remote 104.137.4.160 local 104.137.4.150 ttl 1

# [iptunnel | ip tunnel] add gre-tunl1 mode gre remote 192.168.22.17 local 192.168.10.21 ttl 255
 
 
表1.10 nameif vs ip
Nameif命令
等效的ip命令
nameif [name] [mac_address]
ip link set dev [interface] name [name].
ifrename -i [interface] -n [newname]
 
表1.11 netstat vs ss/ip
netstat命令
等效的ss命令
netstat -a or --all
ss -a or --all
netstat -A [family] or --protocol=[family]
ss -f [family] or –family=[family]
netstat -C
ip route list cache
netstat -e or --extend
ss -e or --extended
netstat -g or --groups
ip maddr, ip maddr show [interface]
netstat -i or --interface=[name]
ip -s link
netstat -l or --listening
ss -l or --listening
netstat -n or --numeric
ss -n or --numeric
netstat -N or --symbolic
ss -r or --resolve
netstat -o or --timers
ss -o or --options
netstat -p or --program
ss -p
netstat -r or --route
ip route, ip route show all
netstat -s or --statistics
ss -s
netstat -t or --tcp
ss -t or --tcp
netstat -u or --udp
ss -u or --udp
netstat -w or --raw
ss -w or --raw
 
表1.12 route vs ip
route命令
等效的ip命令
route
ip route
route -A [family] [add] or route --[family] [add]
ip -f [family] route
route -e or -ee
ip route show
route -h or --help
ip route help
route -v or --verbose
ip -s route
route -V or --version
ip -V
route add or del
ip route [add | chg | repl | del] [ip_addr] via [ip_addr]
route [add or del] dev [interface]
ip route [add | chg | repl | del] dev [interface]
route [add or del] [default] gw [gw]
ip route add default via [gw]
route [add or del] metric [n]
ip route [add | chg | repl | del] metric [number] or preference [number]
route [add or del] mss [bytes]
ip route [add | chg | repl | del] advmss [number]
route [add or del] reject
ip route add prohibit [network_addr]
route [add or del] window [n]
ip route [add | chg | repl | del] window [W]
Ip route命令语法实例如下：
# ip route add 10.23.30.0/24 via 192.168.8.50
# ip route del 10.28.0.0/16 via 192.168.10.50 dev eth0
# ip route chg default via 192.168.25.110 dev eth1
# ip route get [ip_address] 
 
ip应用举例
1. 显示网络设备及配置
ifconfig
ip addr showip link show
ip addr show dev eth0
2. 开启和关闭一个网络接口
ifconfig eth0 up
ip link set eth0 up
ifconfig eth0 down
ip link set eth0 down
3. 设置ip地址
ifconfig eth0 192.168.0.77
ip address add 192.168.0.77 dev eth0
ifconfig eth0 192.168.0.77 netmask 255.255.255.0 broadcast 192.168.0.255
ip addr add 192.168.0.77/24 broadcast 192.168.0.255 dev eth0
4. 删除一个ip地址
ip addr del 192.168.0.77/24 dev eth0
5. 给网络接口添加一个别名
ifconfig eth0:1 10.0.0.1/8
ip addr add 10.0.0.1/8 dev eth0 label eth0:1
6. Arp协议
在arp表中添加一条
arp -i eth0 -s 192.168.0.1 00:11:22:33:44:55
ip neigh add 192.168.0.1 lladdr 00:11:22:33:44:55 nud permanent
dev eth0
在一个设备上关掉arp方案
ifconfig -arp eth0
ip link set dev eth0 arp off
7. 显示路由信息
ip ro
8. 添加和删除路由
ip ro add 10.0.0.0/16 via 192.0.2.253
ip ro del 10.0.0.0/16 via 192.0.2.253
9. 获取arp表
ip neigh
10. 获取ip neighbor的帮助
ip neighbor help
 
ip命令的其他参数及其意义，用户可以直接运行man ip即可查看。
