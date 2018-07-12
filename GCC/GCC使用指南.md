# GCC 使用指南

gcc -static -o prog2c main.o ./libvector.a
gcc -static -o prog2c main.o -L. -lvector

上面的两条指令等效，-lvector 是 libvector.a 的缩写，-L.告诉链接器在当前目录下查找libvector.a

gcc -shared -fpic -o libvector.so addvec.c multvec.c

生成动态链接库

选项：

- c：只生成可重定位目标文件，不链接
- static： 告诉链接器应该构建一个完全链接的可执行文件，它可以加载到内存中并运行，在加载时无需进一步的链接。
- fpic：指示编译器生成与位置无关的代码
- shared：指示链接器创建一个共享的目标文件

