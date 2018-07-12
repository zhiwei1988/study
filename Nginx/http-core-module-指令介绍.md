## listen

设置 IP 的 address 和 port ，或 UNIX 域套接字的 path。可以同时指定 address 和 port，也可以单独指定。address 也可以换成 hostname。指令举例：

> listen 127.0.0.1:8000;
> listen 127.0.0.1;
> listen 8000;
> listen *:8000;
> listen localhost:8000;

IPv6 address 的指定方式：

> listen [::]:8000;
> listen [::1];

UNIX 域套接字的指定方式：

> listen unix:/var/run/nginx.sock;

 