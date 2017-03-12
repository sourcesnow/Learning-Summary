# 2017-3-2
* #include<stdio.h>与#include"stdio.h"之间的区别是，使用后者的查找头文件的步骤更多，相对花费的时间更长 详情见 [MSDN](https://msdn.microsoft.com/zh-cn/library/hh875057.aspx)

# 2017-3-11
 * char* s="abcd"，其中sizeof(s)是4表示的是指针变量的大小,sizeof(*s)是1,表示的是*第一个字符的大小*,strlen(s)表示的是4,是字符串的长度,这个系统自带的函数，是以'\0'作为结束标志的，所以没有考虑‘\0’，如果使用sizeof(s)/sizeof(*s)则，长度是5。
