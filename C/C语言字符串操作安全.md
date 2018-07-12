# C语言字符串操作安全

## 确保有足够的空间存储字符串的字符数据和’\0’结束符

**根据源字符串长度为目标字符串分配空间**

```c
int main(int argc, char *argv[])
{
    char *dst = NULL;
    size_t length = strnlen(argv[1], MAX_LEN);
	if (argc > 1)
	{
		dst = (char *)malloc(length + 1);
		if(dst != NULL)
		{
            int ret = strncpy(dst, argv[1], length + 1); 
            // 校验ret，确保安全函数执行成功
        } 
	}
	
	// 使用完后释放内存
	
	return 0;
}
```

**在赋值循环语句中考虑结束符的添加**

```c
enum { ARRAY_SIZE = 32 };
void func(void) 
{
    char dst[ARRAY_SIZE + 1] = {0x00};
    char src[ARRAY_SIZE + 1] = {0x00};
    size_t i = 0;
    // 考虑结束符的写入位置，不会越界
    for (i = 0; src[i] != ‘\0’ && (i < ARRAY_SIZE); ++i)
    {
        dest[i] = src[i];
    }
    dst[i] = '\0';
}
```

## 字符串操作过程中确保字符串有’\0’结束符


