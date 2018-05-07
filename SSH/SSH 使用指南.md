# SSH 使用指南

SSH之所以能够保证安全，原因在于它采用了公钥加密。整个过程是这样的：

1. 远程主机收到用户的登录请求，把自己的公钥发给用户。
2. 用户使用这个公钥，将登录密码加密后，发送回来。
3. 远程主机用自己的私钥，解密登录密码，如果密码正确，就同意用户登录。

## 公钥登录

使用密码登录，每次都必须输入密码，非常麻烦。好在SSH还提供了公钥登录，可以省去输入密码的步骤。

所谓"公钥登录"，原理很简单，就是用户将自己的公钥储存在远程主机上。登录的时候，远程主机会向用户发送一段随机字符串，用户用自己的私钥加密后，再发回来。远程主机用事先储存的公钥进行解密，如果成功，就证明用户是可信的，直接允许登录shell，不再要求密码。

这种方法要求用户必须提供自己的公钥。如果没有现成的，可以直接用ssh-keygen生成一个：

`$ ssh-keygen -t rsa -b 4096 -C "$(whoami)@$(hostname)-$(date -I)"`

- `-t` 指定加密类型
- `-b` 制定密钥对长度
- `-C` 注释

运行上面的命令以后，系统会出现一系列提示，可以一路回车。其中有一个问题是，要不要对私钥设置口令（passphrase），如果担心私钥的安全，这里可以设置一个。

运行结束以后，在$HOME/.ssh/目录下，会新生成两个文件：id_rsa.pub和id_rsa。前者是你的公钥，后者是你的私钥。

### 将 SSH Key 添加到 ssh-agent

如果您的私钥使用密码短语来加密了的话，每一次使用 SSH 密钥对进行登录的时候，您都必须输入正确的密码短语。

而 SSH agent 程序能够将您的已解密的私钥缓存起来，在需要的时候提供给您的 SSH 客户端。这样子，您就只需要将私钥加入 SSH agent 缓存的时候输入一次密码短语就可以了。这为您经常使用 SSH 连接提供了不少便利。

`eval $(ssh-agent -s)` 确保 ssh-agent 已运行。

`ssh-add ~/.ssh/id_rsa`

### 将公钥复制到远程服务器上

这时再输入下面的命令，将公钥传送到远程主机host上面

`$ ssh-copy-id user@host`

好了，从此你再登录，就不需要输入密码了。

如果还是不行，就打开远程主机的/etc/ssh/sshd_config这个文件，检查下面几行前面"#"注释是否取掉。

> RSAAuthentication yes
PubkeyAuthentication yes
AuthorizedKeysFile .ssh/authorized_keys

然后，重启远程主机的ssh服务。

`service ssh restart`

## 参考链接

- [SSH原理与运用（一）：远程登录](http://www.ruanyifeng.com/blog/2011/12/ssh_remote_login.html)
- [SSH keys](https://wiki.archlinux.org/index.php/SSH_keys)
