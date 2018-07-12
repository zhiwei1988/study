# C语言中的字符串操作

`char *strncpy(char *dest, const char *src, size_t n)`

从 src 中拷贝 n（dest 所占内存空间） 个字节到 dest中，如果src的有效字符长度小于n，则dest中剩余空间会被null字符填充；**如果src中的有效字符长度大于n，则dest将没有null结束字符**。

`int snprintf(char *str, size_t size, const char *format, ...)`

snprintf 最多向str中写入size个字节（包括结束字符`\0`）,如果待输出的字符串长度大于size那么它将会被截断，返回值是写入的实际字节数（不包括`\0`）。如果返回值等于size或更大，说明字符串被截断了。
