`gcc -O1 -S code.c`

"-S" 选项使gcc仅生成汇编代码，而不做其他处理

`gcc -O1 -c code.c`

"-c" 选项使gcc生成目标代码。

目标代码是二进制格式的，无法直接查看。但是可通过**反汇编器**将目标代码转化成一种类似于汇编的格式。

`objdump -d code.o`

带 "-d" 选项的的 objdump 命令可充当这个角色。

`gcc -O1 -o prog code.o main.c`

"-o" 选项使gcc生成可执行文件。