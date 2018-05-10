`find . -name filename`

通过文件名搜索当前位置，默认会搜索所有子目录，除非你指定了搜索深度

`find . -user root`

搜索指定用户拥有的文件

`find . ! -user root`

搜索除指定用户以外用户拥有的文件

`find . -type l`

搜索指定类型的文件

c = 字符设备文件

d = 目录

p = 命名管道 

f = 常规文件 

l = 符号连接

s = 套接字

`find . -maxdepth 2`

限定搜索子文件夹的层级