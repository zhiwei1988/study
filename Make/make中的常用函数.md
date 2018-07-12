# GNU make 中的常用函数

函数调用语法：

```
$(function arguments)
${function arguments}
```

参数与函数名之前通过空格或tab分隔，如果有多个参数则用`,`分隔。

用`{}`还是`()`是根据你的参数来的，如果参数中有变量引用或函数调用，最好保持分隔符的一致性。

```
$(subst a,b,$(x)) // 推荐
$(subst a,b,${x}) // 不推荐
```

**$(wildcard pattern)**

pattern 通常是包含通配符的文件名模式，返回值是与模式匹配的用空格分隔的文件名列表。

**$(realpath names…)**

对于names中的每个文件名，返回规范的绝对名称。规范名称不包含任何`.`或`..`，也没有任何重复的路径分隔符`/`或符号链接。

**$(filter-out pattern…,text)**

返回text中以空格分隔的，不与patrern...中的一个或多个匹配的字段。

```
objects=main1.o foo.o main2.o bar.o
mains=main1.o main2.o
$(filter-out $(mains),$(objects)) // 返回 foo.o bar.o
```


