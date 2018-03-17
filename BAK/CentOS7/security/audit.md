
审计系统是深度服务器操作系统安全体系的重要组成部分，安全审计能够对文件、目录、系统资源，系统调用进行监控和记录。管理员通过创建完善的监控和审计规则，使违反规则的行为被审计和记录，以便进行安全追踪和定位。
 
深度服务器操作系统中使用的事件审计工具程序auditd。
 
审计守护进程
在深度服务器操作系统中该守护进程auditd负责把审计信息写入磁盘审计日志。该守护进程有环境配置和功能配置两个配置文件。
 
审计环境配置文件
审计环境配置文件的路径为/etc/default/auditd，在深度服务器操作系统中环境变量AUDITD_STOP_DISABLE的默认配置为no，AUDITD_CLEAN_STOP的默认配置为yes。
 
 
审计功能配置文件
功能配置文件的路径为/etc/audit/auditd.conf，在深度服务器操作系统中该文件的默认配置如下：
log_file = /var/log/audit/audit.log
log_format = RAW
log_group = root
 
priority_boost = 4
flush = INCREMENTAL
freq = 20
num_logs = 5
disp_qos = lossy
dispatcher = /sbin/audispd
name_format = NONE
##name = mydomain
max_log_file = 6 
max_log_file_action = ROTATE
space_left = 75
space_left_action = SYSLOG
action_mail_acct = root
admin_space_left = 50
admin_space_left_action = SUSPEND
disk_full_action = SUSPEND
disk_error_action = SUSPEND
##tcp_listen_port = 
tcp_listen_queue = 5
tcp_max_per_addr = 1
##tcp_client_ports = 1024-65535
tcp_client_max_idle = 0
enable_krb5 = no
krb5_principal = auditd
##krb5_key_file = /etc/audit/audit.key
 
审计规则配置文件
功能配置文件的路径为/etc/audit/audit.conf，用户可根据自己的需求制定的相应规则就写在此配置文件中。
 
审计规则配置及用法举例
在深度服务器操作系统中，审计规则设置程序auditctl用于控制审计系统产生何种审计信息。
如果要添加对/etc/crontab的监控，具体监控写（w）、属性变更（a），并且设置key为CFG_crontab方便对日志进行检索，具体设置和移除命令如下：
设置命令auditctl -w /etc/crontab -p wa -k CFG_crontab
移除命令auditctl -W /etc/crontab -p wa -k CFG_crontab