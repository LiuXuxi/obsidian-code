# 01编译工具
- [程序环境和预处理](https://blog.csdn.net/weixin_45031801/article/details/135849881?spm=1001.2014.3001.5506))
## 1.1计算机指令概述及C语言如何学
  ### 计算机工作方式简介
  ![[QQ20250930-165400.png]]
## 1.2编译器介绍及系统环境变量
### 1.2.1编译器介绍
#### （图形界面编译器）微软阵营：MSVC
#### （非图形界面编译器）开源组织阵营GNU：gcc
##### Linux：gcc
##### Windows：minGW
### 1.2.2环境变量
#### 可执行文件的名字 告诉系统 找到这个文件 内容读到CPU执行
#### 找到文件名
开始菜单右键—>系统—>高级系统设置—>环境变量—>系统变量PATH—>编辑（有优先级）
## 1.3编译器工作流程介绍
### 1.3.1基本流程
gcc [选项] -o 输出文件 输入文件 
          -v：查看版本信息
          -E-o 文件名.i 文件名.c(预处理器)
### 1.3.2具体流程
cc1 a.c->DNZ4.s(人->编译->汇编语言)
as DNZ4.s->BW16.o(汇编语言->汇编->机器指令集)
collect2 BW16.o \*.o->builid.exe(机器指令集->链接 确定数据的地址->可执行文件)
## 1.4预处理器介绍及条件编译
### 1.4.1预处理(#开头+特定关键字，只有#才作预处理，否则只做普通变量)
1.包含头文件 (#include)
2.宏定义 (替换->在文件编译之前进行一些替换)
(#define)
### 1.4.2条件编译
设置开关
![[920119404cdaf2800df32f55e46063c3.png]]
手动开关
gcc -D定义的变量 -o 输出文件名 输入文件名
## 1.5编译和链接的方法
![[a821bd93afbe06f614ee24c868e687b7.png]]
链接器：汇编时搜集好东西（如函数名），若遇到未定义的则报错
# 02语法基础 
## 2.1数字进制表示法
### 2.1.1十进制 十六进制 二进制 八进制
![[Pasted image 20251001101536.png]]
八进制和十六进制是二进制的简化
- 八进制：三个二进制（如7=111)
- 十六进制：四个二进制（如15=1111）
### 2.1.2进制之间的转换
- 二进制转换为十进制    1011=2^3+2^1+2^0;
- 十进制转换为二进制    1000=512+256+128+64+32+8=2^9+2^8+2^7+2^6+2^5+2^3=0011 1110 1000
- 八进制转换为二进制    15=1 5(101)=1101
- 二进制转换为八进制    1100=1 100=13
- 十六进制转换为二进制    A2=A(1010) 2(0010)=1010 0010
- 二进制转化为十六进制    1000(8) 0000(0)=80
## 2.2C语言进制表示方法
![[Pasted image 20251001104631.png]]
- C语言输入表示（默认十进制）
    - 八进制 0+数字
    - 十六进制 0x+数字
    - 二进制某些编译器不支持
- C语言输出表示
    - 十进制 %d
    - 八进制 %o
    - 十六进制 %x
## 2.3ASC||码表介绍
数字不仅可以表示计算（统计），也可以表示物理事物的映射（状态）
![[Pasted image 20251001112612.png]]
字符数字与数学数字意义不同
（如'9'在ASC||码中为57而不是9）
转换：‘9’-‘0’=57-48=9
## 2.4C语言表示ASC||码
![[Pasted image 20251001115616.png]]
反斜杠+字母：非可视化字符（空格，Tab键等）
反斜杠+0：字符串结束符
![[Pasted image 20251001115829.png]]‘9’和‘\71'和57代表的内容与空间相同
## 2.5基础数据类型
- 内置单词
![[Pasted image 20251001143535.png]]
- 基础数据类型内存大小
![[Pasted image 20251001145720.png]]
- 修饰变量   常量
![[Pasted image 20251001150641.png]]
- unsigned与signed
  - 当存储-1时，最高位为1代表负号，后接补码代表整个内存存储的数据
![[Pasted image 20251001151257.png]]
- 原码 反码 补码
  - 原码：最高位为符号位，最初存储数据的码（负数时最高位为1代表负号不代表数字，0代表正数）
  - 反码：除了符号位（最高位）后后面的数据取反（0变1，1变0）
  - 补码：反码的数值再加一
  - 正数的原码反码补码相同，都为原码，负数按上述进行变换
![[Pasted image 20251001151920.png]]

# 03空间处理
## 3.1如何描述一个空间
- 访问空间的方式
![[Pasted image 20251002104017.png]]
- C语言用地址描述空间的方式
![[Pasted image 20251002104956.png]]
## 3.2代码验证  地址二元素
### 3.2.1代码验证
![[Pasted image 20251002110437.png]]
### 3.2.2地址二元素：存储地址大小的容量与访问地址的单元
- 地址的大小与基本数据类型无关，只与操作系统有关
	- 32位：4B
	- 64位：8B
- 基本数据类型决定访问地址的最小单元
## 3.3如何读C的变量声明
-  读的方式：<mark>先右看再左看</mark>
![[Pasted image 20251002134855.png]]
- 二维空间的存储指针
![[Pasted image 20251002133855.png]]
- 三维空间的存储指针
![[Pasted image 20251002133928.png]]
## 3.4函数地址的保存
- 函数指针
![[Pasted image 20251002140212.png]]
函数指针的变量定义同样遵循<mark>先看右再看左</mark>:向右遇到（），则变量升级为函数，遇到[]则升级为数组
- 定义printf()的函数指针
![[Pasted image 20251002140550.png]]
- <font color=red>模拟计划执行表的案例</font>:一周七天，每天做不同的事
```
#include<stdio.h>

void read()
{
	printf("read\n");
}

void swimming()
{
	printf("swimming\n");
}

void write()
{
	printf("write\n");
}

void goout()
{
	printf("goout\n");
}

void hike()
{
	printf("hike\n");
}

void basketball()
{
	printf("basketball\n");
}

void badmiton()
{
	printf("badmiton\n");
}

int main()
{
	//定义函数指针数组
	void (*event[])(void)= { read, swimming, write, goout, hike, basketball, badmiton };
	//调用函数指针，输出七天的事
	for (int i = 0; i < 7; i++)
	{
		event[i]();
	}
	return 0;
}
```
## 3.5空间的属性概念
- C语言的内存结构
![[Pasted image 20251002174528.png]]![[Pasted image 20251002175125.png]]
- 空间的属性
![[Pasted image 20251002182214.png]]
- static段的特点分析
static变量的初始化<font color=red>只有一次</font>，后面的初始化不会被执行，在函数内的static变量只会被函数调用，不能直接被main函数直接访问
![[Pasted image 20251002182801.png]]
![[Pasted image 20251002182646.png]]
## 3.6空间权限之边界访问
- 定义空间的二要素
	- 定义在哪里
	- 定义多少个有效空间
![[Pasted image 20251002212926.png]]通过越界访问buf数组修改a的值
- 空间访问权限要考虑哪些
![[Pasted image 20251002213702.png]]
## 3.7字符串空间的行为
![[Pasted image 20251002220134.png]]
- <font color=red>strlen与sizeof的区别</font>
	- strlen只测量字符串结束符‘\0’之前的长度
		- 测量数组还是指针名都是字符串的长度
	- sizeof会测量包括结束符的长度
		- 测量数组则是整个字符串的大小
		- 测量指针名，则大小由操作系统决定，与字符串长度无关
# 4.函数设计
## 4.1函数概念
- 函数名
	- 程序员编写代码空间的名称，本质就是一个地
	- 址（常量）
	- `int fun(int a,int b);`声明一个地址常量
	- `fun(10,20);`使用这个地址，访问代码空间
- 本质：<font color=red>一个非常特殊的地址</font>
	- 可以接受消息（几个？每个都是什么类型）
	- 可以返回信息（返回一个信息，什么类型？）
- 定义一个变量来保存不同的常量
	- int(\*p)(int int);
	- 利用typedef便于程序员进行阅读
## 4.2typedef的使用
- typedef的作用
typedef既可以为基本数据类型取别名，也可以为<font color=red>指针甚至函数起别名</font>
`typedef int time_t//基本数据类型别名`
`typedef int* point//指针别名`
`typedef (*fun)(int，int) fun_t//函数别名`
- 给函数起别名
```
#include<stdio.h>

typedef int(*show_t)(char const* const _Format, ...);

int main()
{
	show_t myshow;
	myshow = printf;
	myshow("hello world");
	return 0;
}
```
- <font color=red>配合条件编译</font>
```
#ifdef C64
typedef int u32;
#else
typedef long u32;
#endif
```

## 4.3函数承上启下的作用
- 函数如何获取信息
	- 从调用者处拷贝到函数空间（就这一种）
- 案列：交换两个数
	- 值拷贝
	- 地址拷贝
- <font color=red>传递地址的含义</font>
	- <mark>反向更新</mark>
	- <mark>连续空间的查看</mark>
	- <mark>修改连续空间的值</mark>
## 4.4函数地址传递的唯一性声明

|     | 基础数据类型       | 连续空间  |
| --- | ------------ | ----- |
| 看   | 值拷贝          | const |
| 改   | 地址（需要考虑越界问题） | 地址和大小 |
- 值拷贝`int fun1(int)`
- 地址`int fun2(int*)`
- const`int fun3(const int *)//声明为常量`
- 地址和大小`int fun4(int*,int num)`
## 4.5字符空间声明的注意事项
- 空间

| 字符空间  | 结束有标志0（'\0') | 可以不限制长度（可能导致内存泄露） |
| ----- | ------------ | ----------------- |
| 非字符空间 | 结束没有标志       | 限制长度              |
- strcpy与strncpy
	- `void strcpy(char*,const char*)//前一个可改，后一个不可改`
	- `void strncpy(char*,const char*,size_t_Count)//增加限制长度，防止内存泄漏`
## 4.6任意空间的声明方式
- 非字符空间（数据空间）
	- 对于图片、声音、视频、文档等非字符空间（数据空间），可以一个int一个int的操作，也可以一个B一个B的操作
	- <font color=red>void\*p</font>
		- p不合法，没有明确指定操作行为，但可以作为形参，接受地址用的，使用时再转换
		- 使用案例
			```
			void fun(void*a,int num)//接受地址与大小
			{
				char*p=(char*)a;根据接受需求进行强转
			}
			int main()
			{
				struct abc data[10];//可为任意数据类型
				fun(data,10);
				return 0;
			}
			```
- 连续空间的声明方式
	- 连续的字符空间
	```
	int fun1(const char*);//只读
	int fun2(char*,[int num]);可读可写
	```
	- 连续的数据空间
	```
	int fun3(const void*,int num);只读
	int fun4(void*,int num);可读可写
	```
- 常见内存使用方式
`void*memset(void*,int,size_t_Size);//C语言中任意空间的内存初始化函数`
```
char*p=(char*)malloc(1024);
memset(p,0,1024);//p是初始化的空间，0是初始化的值，1024是初始化空间的大小
```
## 4.7函数返回值的有效性
- 返回值
	- 基础数据类型
	- 结构体
	- 地址：信息量变大
- 返回后，函数里的空间<mark>消失</mark>
- 返回地址：地址哪些是有效的
	- 代码区
	- 常量区
	- 数据区（【全局变量】、static变量）<font color=red>有效</font>
	- 堆区（malloc申请与free释放）<font color=red>有效</font>
	- 栈区（局部变量）<font color=red>无效</font>
## 4.8返回值的地址特点
- 返回值在数据区上
```
char*fun1(int flag)
{
	static char buf[32];//static静态区上的内存
	snprintf(buf,sizeof(buf),"===%d===",flag);//将格式化字符串赋值给buf数组
	return buf;//返回全局地址，有效（若无static定义，则为局部变量，无效）
}
int main()
{
	char*res;
	res=fun1(10);
	printf("%s",res);
	res=fun1(20);
	printf("%s",res);
}
```
- 返回值在堆上
```
char*fun2(int flag)
{
	char*buf;
	buf=(char*)malloc(32);//申请空间
	snprintf(buf,32,"===%d===",flag);
	return buf;//返回堆上的地址
}

void Release_fun(char*p)
{
	free(p);
}
int main()
{
	char*res;
	res=fun2(10);
	Release_fun(res);
	res=fun2(20);
	Release_fun(res);
}
```
- 若函数返回的static的地址，则空间地址在数据区内
- 若有两个函数配对，一个申请一个释放，则返回地址在堆上
	- 如fopen与fclose
# 5.常见面试题
## 5.1指针声明知识点的题目
### 5.1.1`int (*s[10])(int)`表示的是什么意思？
- <font color=red>先右看再左看</font>
- s是数组（右看）
	- 数组中的元素有多少个？10个（看括号）
	- 数组里的元素是什么（向左看）
		- 元素是指针（向左看）
			- 指针的大小（由操作系统决定，4B或8B）
			- 指针移动的方式（指针指向的是什么）（向右看）
				- 是函数
					- 函数的参数，有几个参数（向右看）
						- 是一个int类型的变量参数
					- 函数的返回值是什么（向左看）
						- 是int类型的值
### 5.1.2用变量a给出下面的定义
![[Pasted image 20251004161556.png]]
![[Pasted image 20251004161936.png]]
### 5.1.3`char *const p1;const char *p2;char const *p3;const char* const p4`这上述四个变量有什么区别？
- `char *const p1`
	- p1是只读的地址，这个空间操作方法为：一个char一个char地可读可写（指向的地址不可修改，但地址存储的东西可读可修改
- `const char *p2`
	- p2是可读可写的地址，这个空间操作方法为：一个char一个char地只读不可写（指向的地址可修改，但地址存储的东西只可读不可修改）
- `char const *p3`
	- p3的声明与p2相同
 - `const char* const p4`
	 - p4是一个只读的地址，这个空间操作的方法为：一个char一个char地只读不可写（指向的地址不可修改，且地址存储的东西也只可读不可修改）
- <font color=red>解决的方法还是 <mark>先看右再看左</mark> 右边无修饰，则看左边是先*还是const或char</font>
## 5.2指针概念的题目
### 5.2.1在32bit编译器下，写出运行结果
![[Pasted image 20251004164537.png]]
![[Pasted image 20251004165550.png]]
### 5.2.2已知代码如下，填空：
![[Pasted image 20251004165720.png]]
![[Pasted image 20251004170010.png]]
## 5.3字符空间操作类题目
### 5.3.1如下代码运行后会产生什么结果？为什么？
```
char str[10];
strcpy(str,"0123456789");
```
出现越界问题，运行结果不确定；字符串后隐藏了\0，实际长度为11，而数组长度只有10，会出现越界问题，而运行结果与编译平台有关
### 5.3.2请写出一下str变量的sizeof、strlen的大小
```
char str[]="12345"
char str[10]={'1','2','3','4','5'};
char str[]={'1','2','3','4','5'};
```
- sizeof（<font color=red>空间大小</font>）
	- 6
	- 10
	- 5
- strlen（<font color=red>直到读到\0</font>)
	- 5
	- 数据区：5，栈：直到读到\0
	- 数据区：5，栈：直到读到\0
- <font color=red>双引号的字符串</font>：编译器自动在末尾加\0
### 5.3.3以下代码运行后会出现什么问题？打印结果是什么？
```
void main()
{
	char abc[10];
	printf("%d",strlen(abc));
}
```
- abc定义在主函数内，无static修饰，则空间在栈上，strlen会一直读取，直到读到\0，与10无关，则打印结果不确定
## 5.4结构体对齐类题目
- 对齐
	- 依据：按照成员最大的<font color=red>数据类型</font>来作为对齐标准
- 给定结构体，请问他的sizeof大小？
```
struct data
{
	char t1;
	char t2;
	unsigned short t3;
	unsigned long t4;
};
```
## 5.5指针访问类题目
### 5.5.1下面程序的运行结果是
```
int main()
{
	int a[5]={1,2,3,4,5};
	int *ptr=(int*)(&a+1);
	printf("%d %d\n",*(a+1)，*(ptr-1));
}
```
- 打印结果为2 5
```
  int a[5];
  int*p2=&a//p2五个地址地五个地址地移动
int\*p1=a;//p1一个地址一个地址地移动
```
### 5.5.2下面程序的运行结果是
  ```
  char*s="AAA";
  printf("%s",s);
  s[0]='B';
  printf("%s",s);
  ```
  - 第一个正确打印
  - 第二个不确定，若常量空间被保护，则直接报错，若不被保护，则打印原来的结果，但可能return失败
  - pirntf的作用原理
	  - 将打印内容先存储到系统的<font color=red>缓冲区</font>，遇到\n或其他时再一起将内容冲刷（打印）出来
### 5.5.3下面程序的运行结果是
```
int arr[]={6,7,8,9,10};
int*ptr=arr;
*(ptr++)+=123;
printf("%d %d\n",*ptr,*(++ptr));
```
- 结果为8 8；
- 第一次自增时先用后加，ptr指向7
- 在printf格式化中，变量在栈中，变量先进后出，则格式化时<font color=red>从右往左</font>依次进行
- 则先第一次格式化为先右边第二次自增时先加后用，指向8，第二次格式化是左边，已经自增完毕，所以结果相同
## 5.6函数承上启下功能类题目
### 5.6.1运行后什么结果，为什么？
![[Pasted image 20251005130859.png]]
- 运行失败
- 在调用函数时实参中要用<font color=red>&</font>传递地址，在函数形参中要用<font color=red>*</font>接受地址，这样才能经过函数改变实参的值，否则不改变（无论数据类型是基本的还是指针）
- ```
  //正确代码
  void GetMemory(char**p)
  {
	  *p=(char*)malloc(100);//解引用二级指针p，改变一级指针指向的地址
  }
  void Test(void){
	  char*str=NULL;
	  GetMemory(&str);//用&传递一级指针的地址
	  strcpy(str,"hello world");
	  printf(str);
  }
  ```
### 5.6.2下面的代码有什么问题
![[Pasted image 20251005134748.png]]
- 函数内p在栈中，函数结束后变量出栈变量失效，返回的地址不变，但地址中的内容已经失效
- 若需要返回地址，要么用malloc申请堆空间，要么在变量前用static修饰变量放在全局静态区
### 5.6.3如下代码的结果，为什么？
![[Pasted image 20251005140156.png]]
- 代码逻辑上无问题，但没有free释放申请的堆空间，当数据量过大时，内存空间可能不足导致错误——<font color=red>申请空间后及时释放</font>
![[Pasted image 20251005140442.png]]
- 申请空间时，str指向的是申请的堆空间的<font color=red>首地址</font>，而释放空间时只是空间被释放，而str所指向的<font color=red>地址不变</font>（仍是首地址），所以str不是空指针
- 即使str不是空指针，但指向的首地址空间已经失效，不是系统为它开拓的空间，所以str是<font color=red>野指针</font>
![[Pasted image 20251005141458.png]]
- 当另一个指针申请的空间与首地址重合时，str指向的空间被覆盖，原本的值可能被另一指针修改，所以即使能打印出world，str的使用仍有风险
- 为避免使用str野指针，应当释放空间后让他为空
```
free(str);
str=NULL;
```
## 5.7编程题——游程编码
![[Pasted image 20251005142045.png]]
![[Pasted image 20251005201847.png]]
![[Pasted image 20251005201911.png]]
![[Pasted image 20251005201752.png]]
# 6.知识串讲（海牛直播）
## 6.1代码可移植性
- 工程上避免直接使用int long这样的类型，<font color=red>同样数据类型在不同系统不同编译器内存大小不一样</font>
- ```
  #include<stdint>
  int main()
  {
	  int64_t a=100;
	  printf("%zd",sizeof(a));
  }
  ```
## 6.2自定义数据类型
- 自定义一个容器的大小
	- 用这个容易 把内存 再划分
- 结构体struct 累加组合
	- 累加规则：内存对齐 默认规则
	- 定义预处理宏，告诉编译器，按照什么标准来对齐
		- `#pragma pack(1)//1表示1字节对齐，内存之间无空隙`
 - 共用体union 共享组合
 - 枚举类型enum
	 - C语言中的枚举类似于宏定义，枚举中的值可以修改
## 6.3空间操作
- 有符号与无符号
	- 存储一个数据 无符号类型
	- 数学含义 比较 有符号类型
## 6.4C语言内存空间管理
- <font color=red>sizeof(数组名)=编译器编译期间分配好的空间大小</font>
- <font color=red>sizeof(指针名)=量出容器的大小4/8</font>
## 6.5 多文件编程原理
- <font color=red>把我们不同的接口，分散在不同的.c里维护，编译生成了对应的符号表，连接时，符号表进行汇总，所有符号都有唯一定义</font>
- 工程文件
	- 在物理目录里，有很多的.c源文件
	- 完成一个目标A的构建时，只需要某些.c，完成目标B的构建时，需要另外几个.c
## 6.6cmake的使用
- <font color=red>生成工程管理器的工具 跨平台 统一配置平台</font>
- <font color=greeen>cmake解析同一个的配置文件</font>
