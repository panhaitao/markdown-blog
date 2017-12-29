
afick概述
文件完整性检查工具afick设计的目标就是监视你主机上文件的变化（包括新建、删除、修改文件），因此，我们通过它具有的文件完整性检查功能用作入侵检测系统。它也被设计为便携式克隆助手。为了安全起见，我们应该定期的运行这个程序（如作为批处理任务）。
 
afick的安装
在深度服务器操作系统afick工具的安装方式有两种：
Tasksel安装方式
 
1. 配置好软件源，配置软件源请参考本手册的2.3节。
2. 在命令行执行tasksel命令，在打开的tasksel软件选择界面，选中“afick”，	光标移动到“ok/确定”按钮，敲击回车键，系统就开始安装。
 
命令行安装方式
1. 配置好软件源，配置软件源请参考本手册的2.3节。
2. 在命令行执行命令apt-get install afick或aptitude 	install afick，系统就开始安装。
 
afick配置文件
深度服务器操作系统中afick的配置文件为/etc/afick.conf。在此配置文件中可配置文件完整性校验的依据，配置的校验类型有MD5、sha-1、sha-256、sha-512。
 
afick的语法
afick的一般用法
afick [action] [options]
其中action为要afick执行的动作，options为可选项参数。
 
 
afick常用action及它们的意义如表4.7所示，
注：这些强制性动作必须有一个且仅能有一个
 
表4.7 afick命令的action参数说明
短参数
长参数
参数说明
-i
--init
初始化hash.dbm数据库
-C
--check_config
仅检查配置文件语法并退出
-G
--clean_config
检查并清理配置文件，然后退出
-U
--check_update
如果一个软件更新是有效的则进行检查
-k
--compare
比较hash.dbm数据库
-l
--list
检查参数给定的文件（通过逗号分隔）
-u
--update
比较并更新那个hash.dbm数据库
 
--csv
以csv格式导出数据库
-p
--print
打印数据库内容
 
 
afick命令的其他action及其意义，用户可以直接运行man afick即可查看。
 
afick常用option及它们的意义如表4.8所示。
 
表4.8 afick命令的option参数说明
短参数
长参数
参数说明
-A
--archive
写报告到指定目录
-c
--config_file
读指定的配置文件
-D
--database
采用指定的数据库
 
 
 
-h
--help
输出简要的帮助信息并退出
 
--man
输出详细的帮助信息并退出
-V
--version
输出版本信息并退出
 
 
afick命令的其他option及其意义，用户可以直接运行man afick即可查看。
 
afick的用法举例
1. 配置文件采取默认状态。
2. 在测试机tty1,以root用户身份执行如下命令，进行hash.dbm数据库初始化。
afick -c afick.conf --init
3. root用户分别执行如下命令，创建一个测试文件。
echo “This is a integrity testing of file”>testfile;
4. 执行如下命令，查看监测结果，这时就能显示出文件系统的变化，显示结果如下：
afick -c afick.conf -k
 
# summary changes
new file : /root/testfile
 
# detailed changes
new file : /root/testfile
inode_date	 : Wed Sep  2 14:09:15 2015
 
# Hash database : 17810 files scanned, 1 changed (new : 1; delete : 0; changed : 0; dangling : 6; exclude_suffix : 295; exclude_prefix : 0; exclude_re : 0; degraded : 17)
# #################################################################
# MD5 hash of /var/lib/afick/afick => ZedOeD8rpyJ5PwqqiEa2aA
# user time : 7.42; system time : 0.6; real time : 8
 
5. 重复执行步骤2, 初始化数据库。
6. 执行如下命令，更改测试文件testfile的属性。
chmod 777 testfile
7. 执行命令afick -c afick.conf -k, 查看监测结果，结果对文件属性的修改也被监测到，显示如下：
# summary changes
changed file : /root/testfile
 
# detailed changes
changed file : /root/testfile
filemode 	 : 100775	100777
ctime     	 : Wed Sep  2 14:13:19 2015	Wed Sep  2 14:21:15 2015
 
# Hash database : 17811 files scanned, 1 changed (new : 0; delete : 	0; changed : 1; dangling : 6; exclude_suffix : 295; exclude_prefix : 	0; exclude_re : 0; degraded : 18)
# 	##############################################################	###
# MD5 hash of /var/lib/afick/afick => GewYFj78XDNdCBivj6tAZQ
# user time : 7.45; system time : 0.83; real time : 8
 
8. 分别执行如下命令，创建一用户tester并修改其口令。
useradd -m tester;
passwd  tester;
 
9. 再执行命令afick -c afick.conf -k, 查看监测结果，系统文件的变化显示如下：
# summary changes
changed file : /etc/group
changed file : /etc/group-
changed file : /etc/gshadow
changed file : /etc/gshadow-
changed file : /etc/passwd
changed file : /etc/passwd-
changed file : /etc/shadow
changed file : /etc/shadow-
changed file : /etc/subgid
changed file : /etc/subgid-
changed file : /etc/subuid
changed file : /etc/subuid-
changed file : /root/testfile
 
# detailed changes
changed file : /etc/group
md5       	 : 9f2e11207b063bc5eed1b15bde46eed0	8f8e61e6b9c4e95e25c52a5422bca906
inode     	 : 2099595	2099563
filesize  	 : 938	953
atime     	 : Wed Sep  2 10:25:01 2015	Wed Sep  2 14:31:52 	2015
mtime     	 : Wed Sep  2 10:21:50 2015	Wed Sep  2 14:31:52 	2015
ctime     	 : Wed Sep  2 10:21:50 2015	Wed Sep  2 14:31:52 	2015
......
 
# Hash database : 17811 files scanned, 13 changed (new : 0; delete : 	0; changed : 13; dangling : 6; exclude_suffix : 295; 	exclude_prefix : 0; exclude_re : 0; degraded : 18)
# #################################################################
# MD5 hash of /var/lib/afick/afick => GewYFj78XDNdCBivj6tAZQ
# user time : 7.52; system time : 0.69; real time : 8