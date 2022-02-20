[腾讯安全实验室 c/c++安全指南](https://github.com/Tencent/secguide/blob/main/C,C++%E5%AE%89%E5%85%A8%E6%8C%87%E5%8D%97.md)
[google c++ 代码规范](https://zh-google-styleguide.readthedocs.io/en/latest/google-cpp-styleguide/)

[google c++ 编码规范](https://blog.csdn.net/xiexievv/article/details/50972809)

[C/C++代码规范（一）——文件结构、排版、命名规则](https://blog.csdn.net/changyi9995/article/details/105714712)

[C/C++代码规范（二）——表达式、常量、函数设计](https://blog.csdn.net/changyi9995/article/details/106043662)

[C++effective读书笔记（待更新）](https://blog.csdn.net/vict_wang/article/details/81637048)

[如何写出“颜值高”的代码？](https://zhuanlan.zhihu.com/p/350324541)

@[TOC](文章目录)
<hr style=" border:solid; width:100px; height:1px;" color=#000000 size=1">

# 前言
不用谷歌的 使用微软风格
谷歌偏c风格 下划线很多 很难受

# 1.文件结构
## 1.1 版权和版本的声明
文件头 全使用英文 减少中文编码乱码问题
```
/****************************************************************
* Copyright (c) 2021 by XXX Company
* 
* file description：Export To Be DLL Implement
* version：    1.0.0
* author：     Shiver
* time：       2021 / 05 / 31
****************************************************************/
```

## 1.2 导出头文件命名 XXXAPI.h
项目名+API+.h 作为导出dll 的对应头文件 统一格式方便查找
## 1.3 常见项目结构

```
-ProjectName
--src
--include
--lib
--bin
--res
```

> src        目录 存源码包括（\*.cpp、\*.h,*.cc,\*.hpp)
> include 目录 存引入第三方库的 \*.h文件
> lib         目录 存引入第三方库的\*.lib、\*.a 、\*.so （静态库和动态链接库)
> bin        目录 存引入第三方库的\*.dll  (动态库）
> res       目录 存资源文件 例如\*.jpg、\*.icon

## 1.4 头文件 防止重复引入
```cpp
#ifndef XXX_H
#def XXX_H
// 主要内容
#endif 
```
注：尽量不要使用#pragram once,不利于跨平台 貌似只有windows有这个宏
## 1.5 导出接口命名
格式：
```cpp
返回类型+“ ”+公司简称+“_”+模块简称+“_"+函数名(动+宾结构)+“（”+形参列表+“）”；
```
例如：

```cpp
int ByteDance_Decoder_CreateDecoder(int a, int b);
```

当然导出的接口 自然有一些导出宏之类的 WINAPI 、extern "C"等 记得定义为宏 统一添加

## 1.6 类和虚类命名
类(Class)以C开头，例如CFactory
虚类（接口Interface）以I开头，例如IFactory
# 2.参数命名
## 2.1 局部变量
int: nXXX   iXXX
指针:pXXX
char数组:szXXX
wchar_t数组:wszXXX
## 2.2 静态变量
s:static 静态变量
int:s_iXXX

## 2.3 全局变量
g:glogbal 全局变量
int: g_iXXX;

## 2.4 成员变量
m:member 成员
int:m_iXXX

|变量类型|该类型变量的前缀|类型意义|
|--|--|--|
|局部变量 | 无|例如 int类型 nXXX |
|静态变量|s_ |例如 int类型 g_iXXX |
|全局变量|g_ |例如 int类型 g_iXXX |
|成员变量|m_ |例如 int类型 m_iXXX |

## 2.5 常见变量命名
表一 基本类型及前缀规范
|类型名定义|该类型变量的前缀|类型意义|
|--|--|--|
|int8_t	|n	|有符号的8bit整数|
|uint8_t	|n|	无符号的8bit整数|
|int16_t	|n|	有符号的16bit整数|
|uint16_t	|n|	无符号的16bit整数|
|int32_t	|n|	有符号的32bit整数|
|uint32_t	|n|无符号的32bit整数|
|int64_t	|n|	有符号的64bit整数|
|uint64_t	|n|	无符号的64bit整数|
|void	|v|	void类型|
|float32	|f|	32位浮点数|
|float64|
|double	|f|	64位浮点数|
|FILE*	|pf|	文件指针|
|char*|
|char[]	|sz|	字符指针,或者字符数组|
|char	|ch|	字符|
|wchar	|wch|	宽字符|
|wchar*|
|wchar[]	|wsz|	宽字节数组|
|string	|str|	字符串|
|wstring	|wstr|	宽字符串|
|vector	|vec|	vector容器|
|list	|list|	list容器|
|map	|map|	map容器|
|HANDLE	|h|	句柄|
|thread	|h|	线程句柄|
|DWORD	|dw|	双字|
|WORD	|w|	单字|
|bool/BOOL	|b|	布尔变量|
|函数指针	|pfunc|	函数指针|
|迭代器	|itr|	容器迭代器|

表2 变量属性公共前缀规则
|前缀	|前缀意义|
|--|--|
|arr|	数组类型变量|
|p	|指针类型变量|
|t	|自定义类型变量（自定义类型包括结构、联合、枚举型）|
|ap	|存放指针的数组|
|at	|存放自定义类型变量的数组|
|pa	|指向数组的指针|
|pp	|指向指针的指针变量（两维指针）|
|pt	|指向自定义类型的指针变量|

# 3.函数命名
## 3.1大驼峰命名
void ThisIsFunction();

## 3.2 动词＋名词 结构
全局函数的名字应当使用“动词”或者“动词＋名词”（动宾词组）。类的成员函数应当只使用“动词”，被省略掉的名词就是对象本身。
```bash
例如:
InitModule()
SetHeight()
StartAction()
StopAction()
DestoryModule()
```

## 3.3 单个对象用 is has, 多个对象的集合用复数形态

> 比如
> deleteFile，moveFiles，getChildren，单数复数表达的含义是不同的，file表示操作单个文件，files表示可以接受文件集合，children表示子节点不止一个。

## 3.4 用时态语态可以传达更多信息，增强可读性。
对于正在发生的事情用进行时，doing;
对于一个做完的事情用过去式 did done。比如当状态发生变化的时候，
对于正在改变但是还没彻底变完，xxxChanging，
对于已经变了 xxxChanged 表示真的变了。


# 4.代码规范
## 4.1 【内存申请原则】谁创建谁释放,平级作用域内释放

```cpp
{
	int *pNum = new int();
	{
		int *pNum2 = new int();
		delete pNum2;
	}
	delete pNum;
}
```
## 4.2 【结构体初始化】在创建结构体前/构造函数中初始化值

```cpp
struct test
{
  int a;
  int b;
  test(){
   a = 0;
   b = 0;
  }
}

struct test testa;
memset(testa,0,sizeof(testa));
```
声明初始化以及构造初始化 有利于避免野指针。

# 5.代码格式
## 5.1 一行只申明一个变量,且声明后马上初始化
错误范例：
```cpp
int a,b,c;
```
正确范例:

```cpp
int a = 0;
int b = 0;
int c = 0;

char *buffer = new char[260];
memset(buffer,0,260);
```
## 5.2 代码块之间用 多使用换行 分隔
错误范例：
```cpp
int a;
int b;
int c;
if(b==2){
 ...
}
```

正确范例：
```cpp
int a;
int b;
int c;

if(b == 2)
{
 ...
}
```

## 5.3 操作符与变量之间 多使用 空格 分隔
错误范例：

```cpp
if(b==0){...}
a>b?0:1;
```

正确范例：
```cpp
if(b == 0){
...
}

a > b ? 0 : 1;
```
## 5.4 判断语句和循环语句 内容必须用{}包裹
错误范例:
```cpp
if(a==0) return a;
while(1) return 0;
```
正确范例:

```cpp
if(a==0)
{
 ...   
}

while(1)
{
	return 0;
}
```

## 5.5 {}包裹的内容必须有层次感 通过一层一个tab
错误范例：

```cpp
if(a==0)
{
while(1)
{
return 0;
}
return a;
}

```

正确范例:

```cpp
if(a == 0) //1 层
{
	while(1) // 2层
	{
		return 0;//3 层
	}
	
	return a;//2层
}

```

# 6.常见通俗规定
## 6.1 函数形参顺序  先dst,后src
void *memcpy(void *destin, void *source, unsigned n);

## 6.2 长循环放内部，短循环放外部
在多重循环中，如果有可能，应当将最长的循环放在最内层，最短的循环放在最外层，以减少CPU跨切循环层的次数。例如示例4-4(b)的效率比示例4-4(a)的高。

## 6.3 使用const static 代替 #define 
## 6.4 执行命令时 文件路径 记得用转义字符 \\" \\"圈起来路径
## 6.5 路径中的斜杠 默认使用反斜杠 /
```cpp
windows  \\等于/
linux  /就是/
```

## 6.6 四个空格等于一个tab 但一般用4个空格 一个tab某平台等于8个空格

# 7.常见埋坑操作
## 7.1 文件路径
1.文件路径字符串请用""圈起来，避免有空格情况以及部分系统无法识别相关命令
2.文件路径字符串如果有中文请使用Unicode编码
# 总结


