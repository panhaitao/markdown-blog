
网络连通性诊断工具ping也属于一个通信协议，是TCP/IP协议的一部分。利用“ping”命令可以检查网络是否连通，可以很好地帮助我们分析和判定网络故障。
 
ping令的一般用法：
ping [参数] [主机名或IP地址]
 
ping命令常用的参数包括-b、-d、-f、-n、-q、-r、-R、-v、-c、-i、-I、-l、-p、-s、-t它们的具体意义请参见表1.15。
 
表1.15 ping命令参数说明
短参数
长参数
参数说明
-d
 
使用Socket的SO_DEBUG功能
-f
 
极限检测。大量且快速地送网络封包给一台机器，看它的回应
-n
 
只输出数值
-q
 
不显示任何传送封包的信息，只显示最后的结果
-r
 
忽略普通的Routing Table，直接将数据包送到远端主机上。通常是查看本机的网络接口是否有问题
-R
 
记录路由过程
-v
 
详细显示指令的执行过程
<p>-c
 
数目：在发送指定数目的包后停止
-i
 
秒数：设定间隔几秒送一个网络封包给一台机器，预设值是一秒送一次
-I
 
网络界面：使用指定的网络界面送出数据包
-l
 
前置载入：设置在送出要求信息之前，先行发出的数据包
-p
 
 范本样式：设置填满数据包的范本样式
-s
 
字节数：指定发送的数据字节数，预设值是56，加上8字节的ICMP头，一共是64ICMP数据字节
-t
 
存活数值：设置存活数值TTL的大小
-b
 
允许ping命令ping广播地址
 
例如ping的通的情况：
# ping 10.1.11.186
PING 10.1.11.186 (10.1.11.186) 56(84) bytes of data.
64 bytes from 10.1.11.186: icmp_seq=1 ttl=64 time=0.436 ms
64 bytes from 10.1.11.186: icmp_seq=2 ttl=64 time=0.247 ms
64 bytes from 10.1.11.186: icmp_seq=3 ttl=64 time=0.248 ms
64 bytes from 10.1.11.186: icmp_seq=4 ttl=64 time=0.249 ms
64 bytes from 10.1.11.186: icmp_seq=5 ttl=64 time=0.248 ms
64 bytes from 10.1.11.186: icmp_seq=6 ttl=64 time=0.251 ms
^C
--- 10.1.11.186 ping statistics ---
 
例如运行下面命令，ping广播地址：
# ping -b 10.1.11.255
PING 10.1.11.1 (10.1.11.1) 56(84) bytes of data.
64 bytes from 10.1.11.1: icmp_seq=1 ttl=64 time=0.326 ms
64 bytes from 10.1.11.1: icmp_seq=2 ttl=64 time=0.345 ms
64 bytes from 10.1.11.1: icmp_seq=3 ttl=64 time=0.249 ms
64 bytes from 10.1.11.1: icmp_seq=4 ttl=64 time=0.448 ms
64 bytes from 10.1.11.1: icmp_seq=5 ttl=64 time=0.434 ms
64 bytes from 10.1.11.1: icmp_seq=6 ttl=64 time=0.415 ms
^C
--- 10.1.11.255 ping statistics ---
 
例如运行如下命令，每0.5秒发送一次网络封装包，并且限制10次停止发送：
# ping -i 0.5 -c 10 10.1.11.186
PING 10.1.11.186 (10.1.11.186) 56(84) bytes of data.
64 bytes from 10.1.11.186: icmp_seq=1 ttl=64 time=0.249 ms
64 bytes from 10.1.11.186: icmp_seq=2 ttl=64 time=0.252 ms
64 bytes from 10.1.11.186: icmp_seq=3 ttl=64 time=0.245 ms
64 bytes from 10.1.11.186: icmp_seq=4 ttl=64 time=0.246 ms
64 bytes from 10.1.11.186: icmp_seq=5 ttl=64 time=0.246 ms
64 bytes from 10.1.11.186: icmp_seq=6 ttl=64 time=0.242 ms
64 bytes from 10.1.11.186: icmp_seq=7 ttl=64 time=0.261 ms
64 bytes from 10.1.11.186: icmp_seq=8 ttl=64 time=0.242 ms
64 bytes from 10.1.11.186: icmp_seq=9 ttl=64 time=0.253 ms
64 bytes from 10.1.11.186: icmp_seq=10 ttl=64 time=0.247 ms
 
--- 10.1.11.186 ping statistics ---
 
ping命令的其他参数及其意义，用户可以直接运行man ping即可查看。