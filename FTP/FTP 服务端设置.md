# FTP 服务端设置

## 安装

以 ubuntu16.04 LTS 为例。

`apt-get install vsftpd` 安装服务端软件

## 配置

vsftpd 的大多数配置都可以通过编辑 /etc/vsftpd.conf 文件实现。该文件本身自带大量注释说明，所以这里仅就一些重要的配置予以说明。

- write_enable=YES # 允许用户进行上传
- local_enable=YES # 允许 /etc/passwd 中的用户登录
- anonymous_enable=YES # 允许匿名用户登录，默认情况下，匿名登录只能从 /srv/ftp 下载
-  anon_upload_enable=YES # 允许匿名用户上传文件，需本地文件夹权限支持
- anon_mkdir_write_enable=YES # 允许匿名用户创建新的目录
- no_anon_password=YES # 匿名登录不需要密码
- anon_max_rate=30000 # 匿名客户端的最大传输速率（以 Bytes/秒 为单位）
- anon_root=/example/directory # 用于匿名登录的目录
- chroot_list_enable=YES # 阻止用户离开家目录
- chroot_list_file=/etc/vsftpd.chroot_list # chroot_list_file 定义了被 chroot 限制的用户列表
- chroot_local_user=YES # 默认为所有用户启用 chroot 环境。 在这种情况下，chroot_list_file 定义了不受 chroot 限制的用户列表。
- userlist_enable=YES # 限制指定用户登录
- userlist_file=/etc/vsftpd.user_list # userlist_file 文件列出不允许登录的用户
- userlist_deny=NO # 只允许指定用户登录，此时 userlist_file 文件指定允许登录的用户
- local_max_rate=1000000 # 最大数据传输速率（单位: Bytes/秒）
- max_clients=50 # 可以同时连接的最大客户端数
- max_per_ip=2 # 每个 IP 允许的最大连接数

## 创建用户

- mkdir /home/username
- sudo useradd username -g ftp -d /home/username -m username
- sudo passwd username
- mkdir /home/username/pub
- chmod 777 -R /home/username/pub # 新建一个pub目录用于存放文件，并且赋予全部访问权限
- usermod -s /sbin/nologin username # 限制用户 username 只能通过 ftp 登陆，而不能直接登陆服务器

## 记录日志

- xferlog_enable=YES # 记录FTP服务器记录上传下载的情况
- xferlog_std_format=YES # 将记录的上传下载情况写在xferlog_file所指定的文件中
- xferlog_file=/var/log/xferlog
- dual_log_enable=YES # 启用了双份日志。在用xferlog文件记录服务器上传下载情况的同时，vsftpd_log_file所指定的文件也将用来记录服务器的传输情况
- vsftpd_log_file=/var/log/vsftpd.log

## 启动或重启 FTP

- `systemctl start vsftpd` # 启动
- `systemctl restart vsftpd` # 重启

## 常见错误

### 530 Login incorrect

默认情况下，配置文件中 pam_service_name=vsftpd，将其改成 pam_service_name=ftp 就可以解决该问题（具体原因未知）

### 独立模式运行

如果将vsftpd守护程序设置为以独立模式运行，而不是启动 vsftpd 守护程序和 enable xinetd.service，请在 /etc/vsftpd.conf 中进行以下更改：listen=NO

**这个配置文档中的描述貌似相反，具体原因未知，难道是我英语太差？**

## 参考链接

- [config manual](https://security.appspot.com/vsftpd/vsftpd_conf.html)
- [Ubuntu Server 16.04.1 LTS 64位使用vsftpd搭建ftp服务器](http://blog.csdn.net/qq_33279781/article/details/73607466)
- [Very Secure FTP Daemon](https://wiki.archlinux.org/index.php/Very_Secure_FTP_Daemon)
- [ubuntu vsftpd 530 Login incorrect](http://www.jianshu.com/p/1f6a4f2de7b6)