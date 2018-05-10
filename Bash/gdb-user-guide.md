`set scheduler-locking on`

step 或 continue 时只让当前被调试的线程执行。

off 不锁定任何线程

on 只有当前被调试线程执行

step 在单步的时候，除了 next 过一个函数的情况以外，只在当前线程执行。

`thread tid`

 切换调试线程

`info thread`

查看当前进程的线程

`x/nfx addr` 

- n 多少个单位 
- f 以什么格式打印
  - x 十六进制显示
  - d 十进制显示
  - u 无符号十进制
  - o 八进制
  - t 二进制
  - I 指令地址格式
  - c 一字符格式
  - f 全浮点格式
- x 一个地址单位的长度
  - b 1字节 h 2字节 w 4字节

`set sysroot`

设置动态库路径

`set solib-search-path`

设置动态库查找路径前缀