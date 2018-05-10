`strace -f -e trace=file -p 845 -o 845.file.trace.log app-name`

-f 跟踪由 fork 创建的所有子进程

-e trace=file 跟踪文件操作相关的系统调用

-o 输出到指定文件 

-p 指定要跟踪的进程号