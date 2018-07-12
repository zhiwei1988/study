## Linux下的库打桩机制

库打桩机制允许你截获对共享库函数的调用，取而代之执行自己的代码。

### 编译时打桩

`gcc -DCOMPILETIME -c mymalloc.c`

`gcc -I. -o intc int.c mymalloc.o`

-I. 参数告诉C预处理器在搜索系统目录之前，现在当前目录中查找malloc.h

### 链接时打桩

> Linux静态链接器支持用--wrap f标志进行链接时打桩。这个标志告诉链接器，把对符号f的引用解析成`__wrap_f`，把对符号`__real_f`的引用解析为f。

`gcc -DLINKTIME -c mymalloc.c`

`gcc -c int.c`

`gcc -Wl,--wrap,malloc -Wl,--wrap,free -o intl int.o mymalloc.o`

-Wl,option 标志把option传递给链接器。

### 运行时打桩

编译时打桩需要能够访问程序的源代码，链接时打桩需要能够访问程序的可重定位目标文件。运行是打桩只需要能够访问可执行目标文件。

如果LD_PRELOAD环境变量被设置为一个共享库路径名的列表，那么当你加载和执行一个程序，需要解析未定义的引用时，动态链接器会先搜索LD_PRELOAD指定的库，在搜索任何其他的库。