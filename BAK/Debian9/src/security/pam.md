# PAM模块

## 概述

PAM（Pluggable Authentication Modules ）是由Sun提出的一种认证机制。它通过提供一些动态链接库和一套统一的API，将系统提供的服务 和该服务的认证方式分开，使得系统管理员可以灵活地根据需要给不同的服务配置不同的认证方式而无需更改服务程序，同时也便于向系统中添加新的认证手段.
 
### PAM的核心文件和配置文件位置：

* /lib64/libpam.so.* PAM核心库
* /lib64/security/pam_*.so 可动态加载的PAM service module
* /etc/pam.conf 或 /etc/pam.d/  PAM配置文件位置

### PAM的配置实例

PAM的配置是可以通过`/etc/pam.conf`或`/etc/pam.d/`目录下配置文件来管理PAM，推荐使用`/etc/pam.d/`目录下的配置文件，以下是部分参考配置实例

* 实例一： 配置用户密码强度：

限定用户密码最小是长度为8位，且密码字符串中至少包含一个大写字母、一个小写字母和一个数字，修改配置文件`/etc/pam.d/system-auth`，将包含`pam_cracklib.so`的一句改为：
```
password    requisite     pam_cracklib.so enforce_for_root retry=3 minlen=8 ucredit=-1 lcredit=-1 dcredit=-1 difok=3
```

* 实例二：限制密码失败尝试次数：

即连续三次登录口令输入错误，将锁定该用户账户3分钟，锁定期间，拒绝用户登陆，编辑配置文件`/etc/pam.d/sshd`，在行首添加：

```
auth        required      pam_tally2.so    deny=3    unlock_time=180    even_deny_root root_unlock_time=30
```

可以使用`pam_tally2`来查询用户登陆失败的时间和次数，以及命令`pam_tally2 -u 用户名 --reset=0` 立即清楚限制
 
## PAM的配置语法 

 
如果`/etc/pam.conf`配置文件，PAM配置文件的语法如下：
```
service-name module-type control-flag module-path arguments
```
使用配置目录/etc/pam.d/ 目录下的配置件名则默认对应的service-name，PAM配置文件的语法如下：

```
module-type control-flag module-path arguments
```

参考上节实例二的配置，各个配置解释如下：
* service-name 服务的名字对的是`sshd`
* module-type（实例二为`auth`）：模块类型有四种：`auth、account、session、password`即对应PAM所支持的四种管理方式。同一个服务可以调用多个PAM模块进行认证，这些模块构成一个stack。
   * auth 是指认证管理（authentication management）主要是接受用户名和密码，进而对该用户的密码进行认证，并负责设置用户的一些秘密
信息。
   * account 是指帐户管理（account management）主要是检查帐户是否被允许登录系统，帐号是否已经过期，帐号的登录是否有时间段的
限制等等。
   * 密码管理（password management） 主要是用来修改用户的密码。
   * 会话管理（session management） 主要是提供对会话的管理和记账（accounting）。
* control-flag 实例二为`required`，用来告诉PAM库该如何处理与该服务相关的PAM模块的成功或失败情况。它有四种可能的 值：required，requisite，sufficient，optional。
   * required 表示本模块必须返回成功才能通过认证，但是如果该模块返回失败的话，失败结果也不会立即通知用户，而是要等到同一stack 中的所有模块全部执行完毕再将失败结果返回给应用程序。可以认为是一个必要条件。
   * requisite 与required类似，该模块必须返回成功才能通过认证，但是一旦该模块返回失败，将不再执行同一stack内的任何模块，而是直 接将控制权返回给应用程序。是一个必要条件。注：这种只有RedHat支持，Solaris不支持。
   * sufficient 表明本模块返回成功已经足以通过身份认证的要求，不必再执行同一stack内的其它模块，但是如果本模块返回失败的话可以 忽略。可以认为是一个充分条件。
   * optional表明本模块是可选的，它的成功与否一般不会对身份认证起关键作用，其返回值一般被忽略。
* module-path （实例二为`pam_tally2.so`）是指用来指明本模块对应的程序文件的路径名，一般采用绝对路径，如果没有给出绝对路径，默认该文件在目录`/lib64/security`下面。
* arguments （实例二为`deny=3    unlock_time=180    even_deny_root root_unlock_time=30`）：是指用来传递给该模块的参数。一般来说每个模块的参数都不相同，可以由该模块的开发者自己定义，但是也有以下几个共同 的参数：
  * debug 该模块应当用syslog( )将调试信息写入到系统日志文件中。
  * no_warn 表明该模块不应把警告信息发送给应用程序。
  * use_first_pass 表明该模块不能提示用户输入密码，而应使用前一个模块从用户那里得到的密码。
  * try_first_pass 表明该模块首先应当使用前一个模块从用户那里得到的密码，如果该密码验证不通过，再提示用户输入新的密码。
  * use_mapped_pass 该模块不能提示用户输入密码，而是使用映射过的密码。
  * expose_account 允许该模块显示用户的帐号名等信息，一般只能在安全的环境下使用，因为泄漏用户名会对安全造成一定程度的威 胁。



