
nload概述
Nload是一个实时监控网络流量和带宽使用的控制台应用程序，它能在在命令行界面监控网络吞吐量，它使用两个图表可视化地展示接收和发送的流量，并提供诸如数据交换总量、最小/最大网络带宽使用量等附加信息。nload 网卡流量显示工具功能单一，但是一目了然，使用简单。
 
nload安装
深度服务器操作系统默认已经集成了nload工具。
 
nload用法
nload命令语法
nload [options] [devices]
 
其中，devices表示自定义监控的网卡，默认是全部监控的，使用左右键切换
 
nload常用的option及其含义如表5.10所示。
 
表5.10 nload常用的option及其含义
短参数
长参数
含义
-a
 
全部数据的刷新时间周期，单位是秒，默认是300
-i
 
进入网卡的流量图的显示比例最大值设置，默认10240 kBit/s
-m
 
不显示流量图，只显示统计数据
-O
 
出去网卡的流量图的显示比例最大值设置
-t
 
显示数据的刷新时间间隔，单位是毫秒，默认500
-u
(h|H|b|B|k|K|m|M|g|G)
 
设置右边Curr、Avg、Min、Max的数据单位，默认是自动变的.注意大小写单位不同
(h|b|k|m|g   h: auto, b: Bit/s, k: kBit/s, m: MBit/s etc)
-U
(h|H|b|B|k|K|m|M|g|G)
 
设置右边Ttl的数据单位，默认是自动变的.注意大小写单位不同（与-u相同）
(H|B|K|M|G  H: auto, B: Byte/s, K: kByte/s, M: MByte/s etc)
-h
--help
显示帮助信息
 
nload命令的其他更多选项参数及其含义，用户可以直接运行man nload即可查看。
 
nload快捷键的使用
nload 命令一旦执行就会开始监控网络设备，可以使用下列快捷键操控 nload 应用程序。
Ø 按键盘上的 ← → 或者 Enter/Tab 键在设备间切换。
Ø 按 F2 显示选项窗口。
Ø 按 F5 将当前设置保存到用户配置文件。
Ø 按 F6 从配置文件重新加载设置。
Ø 按 q 或者 Ctrl+C 退出 nload。
 
nload应用举例
1. root登录深度服务器操作系统，在tty1执行命令nload，打开nload界面，监控网卡的实时流量，如下图
 
 
默认第一行是网卡的名称及IP信息，使用键盘上的左右键可以切换网卡;
默认上边Incoming是进入网卡的流量;
默认下边Outgoing是网卡出去的流量;
默认右边（Curr当前流量）、（Avg平均流量）、（Min最小流量）、（Max最大流量）、（Ttl流量统计）。
2. 在远端pc机（10.1.11.186），执行如下命令开始向测试机(ip是10.1.11.146)发送文件，	可以看到nload界面实时监控流入eth2网卡的流量（测试机使用的网卡为eth2）。
默认情况，数据传输过程中统计数据的左边会使用显示流量图，用#号拼出来的，根据	实时流量变化显示。
scp bigfile2 test@10.1.11.146:/tmp
3. 在测试机，执行如下命令开始向远程pc机发送文件，可以看到nload界面实时监控流出eth2网卡的流量（测试机使用的网卡为eth2）。默认情况，数据传输过程中统计数据的左边会使用显示流量图，用#号拼出来的，根据实时流量变化显示。
scp /tmp/bigfile2 wfsong@10.1.11.186:/tmp