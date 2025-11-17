# 1.一维数组
## 1.1交换两个值
- 临时变量法
- 加减法
```
int a=1,b=2;
a=a+b;
b=a-b;
b=a-b;
```  
- 使用系统函数swap
## 1.2字符数组
1. cout在遇到char数组时，会输出整个字符串，直到遇到‘\0'，所以就算是普通的char单个字符地址，我么也需要<font color=red>（void*）来强转他的类型</font>
2. 字符数组的输入与输出
	- gets（输入）与puts（输出）
	- cin与cout不能接受空格，遇到\n与空格就结束，而gets与puts只遇到\n结束，可以输入和输出空格
3. 字符数组操作
	- <font color=red>strcmp(const char*,const char*);</font>以ASC||码比较字符串大小
	- <font color=red>strncmp(const char*,const char*,int);</font><font color=green>整型变量代表两个字符串的前n个字符进行比较</font>
	- <font color=red>stricmp(const char*,const char*);</font><font color=green>不区分大小写比较字符串的大小，比较的结果由函数返回值带回</font>（stricmp_windows,strcasecmp_macos/linux）
	- <font color=red>strnicmp(const char*,const char*,int);</font><font color=green>不区分大小比较字符串的前n个字符，比较的结果由函数返回值带回</font>
		- 字符串1大于字符串2，返回1
		- 字符串1等于字符串2，返回0
		- 字符串1小于字符串2，返回-1
		- 有些可能返回差值
	- <font color=red>strcat(char*,const char*);</font><font color=green>把字符串2拼接到字符串1后（返回字符串1的值）</font>
	-  <font color=red>strncat(char*,const char*,int);</font><font color=green>把字符串2前n个拼接到字符串1后（返回字符串1的值）</font>
	- <font color=red>strchr(const char*,char);</font><font color=green>在字符串中查找指定字符</font>
	- <font color=red>strrchr(const char*,char);</font><font color=green>在字符串中反向查找指定字符</font>
		- 返回一个指向该字符串中第一次出现的字符的指针，如果字符串中不包含该字符则返回NULL空指针
	- <font color=red>strlwr(char*);</font><font color=green>将字符串中大写字母换成小写字母</font>
	- <font color=red>strupr(char*);</font><font color=green>将字符串中小写字母换成大写字母</font>
	- <font color=red>memset(char*,int(初始化值),int(初始化字节数));</font><font color=green>默认一个一个字节字节的查看</font>
	- `#include<cstdlib>`
	- <font color=red>atoi(p)</font><font color=green>字符串转到int整型</font>
	- <font color=red>atof(p)</font><font color=green>字符串转到double浮点数</font>
	- <font color=red>atol(p)</font><font color=green>字符串转换到long整型</font>
	- `#include<cctype>`
	- <font color=red>isalpha();</font><font color=green>检查是否为字母字符</font>
	- <font color=red>isupper();</font><font color=green>检查是否为大写字母字符</font>
	- <font color=red>islower();</font><font color=green>检查是否为小写字母字符</font>
	- <font color=red>isdigit();</font><font color=green>检查是否为数字</font>
![[Pasted image 20251012185612.png]]
## 1.3字符串string
1. 构造函数
	- `string(const char*s)`;<font color=green>将string对象初始化为s指向的字符串</font>`string str("hello");`
	- `string(size_type n,char c);`<font color=green>创建一个包含n个元素的string对象，其中每个元素都被初始化为字符</font>c`string str(10,'a');`
	- `string(const string,&str);`<font color=green>将一个string对象初始化为string对象str（复制构造函数）</font>`string str1("hello");string str2(str1);`
	- `string();`<font color=green>创建一个默认的string对象，长度为0（默认构造函数）</font>`string str;//创建一个空的string对象`
	- <font color=red>string类的设计程序自动处理string的大小</font>因此，上述代码创建了一个长度为0的string对象，但是str中写入数据时，程序会自动调整str的长度。因此，与使用数组相比，使用string对象更方便，也更安全。
2. 获取string对象的长度
	- <font color=red>string.size()</font>
	- <font color=red>string.lenth()</font>
	- ```
	  string str("hello,world");
	  int strlen1=str.length();
	  int strlen2=str.size();
	  ```
	- 两个方法完全一样的，没有区别。length()是C语言习惯保留下来的，size()是为了兼容STL容易而引入的。
3. 复制string对象
	- <font color=red>直接将一个string对象赋值给另一个string对象</font>
	- ```
	  string str1("hello,world");
	  string str2;
	  str2=str1;
	  ```
	- 由于string类会自动调整对象的大小，因此不需要担心目标数组不够大的问题
4. string对象的拼接和附加
	- <font color=red>使用+操作符拼接两个字符串</font>
	- ```
	  string str1("hello");
	  string str2("world");
	  string str3=str1+str2;
	  ```
	- <font color=red>使用+=操作符在字符串后面附加内容</font>
	- ```
	  string str1("hello");
	  string str2("world"\n);
	  str+=str2;
	  str1+="nice job\n";
	  str1+='a';
	  ```
	- <font color=red>使用string.append();</font><font color=green>在一个string对象后面附加一个string对象或c风格的字符串</font>
	- ```
	  string str1="hello,world";
	  string str2="HELLO,WORLD";
	  str1.append(str2);
	  str1.append("C string");
	  ```
	- <font color=red>使用string.push_back();</font><font color=green>在string对象后面附加一个字符</font>
	- ```
	  string str("HELLO");
	  str.push_back('a');
	  ```
5. string对象的比较
	- <font color=red>在c++中s由于将tring对象声明为了简单变量，故而对字符串的比较操作十分简单了，直接使用关系运算符即可</font>
	- ```
	  string str1("hello");
	  string str2("hello");
	  if(str1==str2)
	  {
		  cout<<"str1=str2"<<endl;
	  }
	  else if(str1<str2)
	  {
		  cout<<"str1<str2"<<endl;
	  }
	  else
	  {
		  cout<<"str1>str2"<<endl;
	  }
	  ```
	- <font color=red>使用类似strcmp的函数来进行string对象的比较，string类提供的是string.compare()方法，函数原型如下：</font>
![[Pasted image 20251013121025.png]]
![[Pasted image 20251013121214.png]]
6. 访问string字符串
	 - <font color=red>使用string.substr()函数来获取子串</font>
	 - ![[Pasted image 20251013121707.png]]
	 - 访问string字符串的元素
	 - ![[Pasted image 20251013122342.png]]
7. string对象的查找操作
	- 正向查找
	- ![[Pasted image 20251013214708.png]]
	- 反向查找
	- ![[Pasted image 20251014122625.png]]
	- 查找任一字符
	- ![[Pasted image 20251014122835.png]]
	- ![[Pasted image 20251014123130.png]]
8. string对象的插入操作
	- <font color=red>使用stirng.insert()进行插入操作</font>
	- ![[Pasted image 20251014123249.png]]
9. string对象的删除操作
	- <font clolor=red>使用string.erase()进行元素删除</font>
	- ![[Pasted image 20251014124224.png]]
	- 常用删除
	- ![[Pasted image 20251014130046.png]]
10. 判断字符串是否为空（是否含有有效元素）
	- <font color=red>使用empty()函数</font>
	- <font color=greeen>若字符串为""即仅有一个\0结束符，则认为无有效元素，即字符串为空</font>
	- ![[Pasted image 20251014130306.png]]
11. string的交换
	- <font color=red>使用swap()函数交换两个字符串</font>
	- <font color=greeen>函数会交换两个字符串的内容，同时改变两个字符串的值</font>
	- ![[Pasted image 20251014130933.png]]
12. 输入输出
	- 分割符
		- 传统分割符：<font color=red>空格回车</font>——<font color=greeen>cin</font>
		- <font color=red>输入所有内容都原封不动地存入容器中，直到用户敲入回车</font><font color=greeen>getline</font>
	- ![[Pasted image 20251014131429.png]]
13. string对象的替换
	- <font color=red>string.replace();</font>
	- ![[Pasted image 20251014132412.png]]
14. 字符串反转
	 - <font color=red>使用algorithm头文件里面的reverse函数</font>
	 - ![[Pasted image 20251014132958.png]]
# 2.函数
## 2.1函数声明与定义、函数参数、引用简介
- 引用概念
	- <font color=red>引用即为某个已存在的变量取名，引用变量与被引用变量公用一块内存空间，通过在数据类型后、变量名前添加“&”符号来定义引用类型。</font>
	- <font color=greeen>type &name=data</font>
	- ```
	  int num=11;
	  int &num2=num;//num就是num的别名，就是num的引用
	  ```
- 引用特性
	1. <font color=red>引用只是别名，不占内存；和它引用的变量共用同一块内存空间</font>
	2. <font color=red>引用仅在定义时带&，使用时和普通变量一样使用，不含&</font>
	3. <font color=red>引用必须在创建的时候初始化，一旦引用初始化后，就不能改变引用所指向的变量，类似于指针常量</font>
	4. <font color=red>引用必须与一个确定的合法内存单元相关联，不存在NULL引用且不可以使用</font>
	- <font color=greeen>一个变量可以有多个引用</font>
## 2.2引用参数、可变参数、默认参数、函数返回值、函数嵌套
- 引用使用场景
	1. 做参数
		- <font color=red>void change(int &v1,int &v2){}</font><font color=greeen>在函数被调用时，就相当于传递实参</font>
	2. 做返回值
		- <font color=red>type&funcName(){}</font>
		- 当函数返回一个引用时，则返回一个指向返回值的<font color=greeen>隐式指针</font>，当返回一个引用时，要注意引用的对象<font color=greeen>不能超出作用域</font>。所以返回一个对局部变量的引用是不合法的，但是，可以返回一个对静态变量的引用。
- 可变参数
	- 即函数参数的个数是任意的，最典型的可变参数就是系统内置的scanf函数和printf函数
	- ![[Pasted image 20251016125538.png]]
	- ![[Pasted image 20251016125648.png]]
	- ![[Pasted image 20251016125827.png]]
- 函数默认参数
	- ![[Pasted image 20251016130318.png]]
	- ![[Pasted image 20251016130446.png]]
## 2.3函数递归
- 即在函数内调用自身函数
- 递归条件
	- ![[Pasted image 20251016135110.png]]
- 递归案例
	- ```
	  //1到n的求和
	  int sum(int n)
	  {
		  if(n==1)
		  {
			  return 1;
		  }
		  return sum(n-1)+n;
	  }
	  ```
	- ```
	  //斐波拉契数列
	  int fibo(int n)
	  {
		  if(n<=2)
		  {
			  return 1
		  }
		  else
		  {
			  return fibo(n-1)+fibo(n-2);
		  }
	  }
	  ```
	- ![[Pasted image 20251016140152.png]]
	- ![[Pasted image 20251016140732.png]]
## 2.4内联函数、函数重载
- 内联函数
	- ![[Pasted image 20251016210449.png]]
- 函数重载
	- ![[Pasted image 20251016210616.png]]
	- <font color=red>重载规则</font>
		- ![[Pasted image 20251016210656.png]]
	- 函数重载的原理
		- ![[Pasted image 20251016210849.png]]
	- 函数重载案例
		- ```
		  //两数之和
		  int sum(int a,int b)
		  {
			  return a+b;
		  }
		  float sum(float a,float b)
		  {
			  return a+b;
		  }
		  double sum(double a,double b)
		  {
			  return a+b;
		  }
		  ```
# 3.变量作用域与命名空间
## 3.1变量作用域
- 存储类
- ![[Pasted image 20251019205503.png]]
- ![[Pasted image 20251019205701.png]]
	- <font color=red>auto</font>
		- ![[Pasted image 20251019205747.png]]
	- <font color=red>register注册存储类</font>
		- ![[Pasted image 20251019230000.png]]
	- <font color=red>extern外部存储类</font>
		- ![[Pasted image 20251019230137.png]]
## 3.2命名空间的概念
![[Pasted image 20251019231618.png]]

# 4指针
- <font color=red>nullptr</font>
	- 在某些场景（例如，函数重载）的使用会遇到麻烦，C++引入关键字nullptr来避免二义性，nullptr是一个“指针空值常量”，仅可以被隐式转换为指针类型。
	- <font color=greeen>所以以后指针初始化赋值就使用nullptr.</font>
	- <font color=green>在C++中NULL退化为数字0，而nullptr严格为空</font>
- <font color=red>void指针</font>
	- void指针为<font color=green>无类型指针</font>,void指针可以指向任何类型的数据。所以void指针一般被称为<font color=green>通用指针或者泛指针，也可以叫做万能指针</font>
	- <font color=blown>void指针使用</font>
		1. 在C++中在任何时候都可以用void类型的指针来代替其他类型的指针，void指针可以指向任何数据类型的变量。
		2. 如果要通过void指针去获取它所指向的变量值时候，需要先将void指针强制类型转换成和变量名类型相匹配的数据类型指针后再进行操作。
		3. 任何类型的指针都可以赋值给void指针，无需进行强制类型转换。
- <font color=red>指针与引用的区别</font>
	- ![[Pasted image 20251022194332.png]]
- <font color=red>指针常量与常量指针</font>
	- [[C语言进阶笔记#5.1.3`char *const p1;const char *p2;char const *p3;const char* const p4`这上述四个变量有什么区别？]]
# 5.预处理命令
- 常用预处理指令
	- <font color=red>文件包含类</font>
		- <font color=red>#include包含一个源文件、头文件</font>
	- <font color=greeen>宏定义类</font>
		- <font color=greeen>#define 定义宏 #undef 取消已定义的宏</font>
		- <font color=greeen>带参数宏定义</font>
			- `#define identify(paramlist) expression`在使用宏参数时，建议将所有的参数都是要（）括起来
		- <font color=greeen>宏函数</font>
			- 就是带参数的宏
			- 跟普通函数类似，只是宏函数参数没有类型
			- ```
			  
			  ```
	- <font color=green>条件编译类</font>
		- <font color=green>#if 如果给定条件为真，则编译下面代码</font>
		- <font color=green>#ifdef 如果宏已经定义，则编译下面代码 </font>
		- <font color=green>#ifndef 如果宏没有定义，则编译一下代码 </font>
		- <font color=green>#elif 如果#if条件部位真，当前条件为真，则编译一下代码 </font>
		- <font color=green>#endif 结束#if...到#else条件编译代码块</font>
		- <font color=green>#error</font>
			- 用于编译期间给出一个错误信息，并终止程序的编译。同时后面的错误信息不需要使用双引号
			- `#error error message`
# 6.位运算
## 6.1按位运算符
- ![[Pasted image 20251025105145.png]]
- <font color=red>取反运算符~</font>
	- 定义：参加运算的一个数据，按二进制进行“取反”运算
	- 运算规则：对一个运算量取反操作，即1->0，0->1
	- ```
	  a:01111010
	  ~a:10000101
	  ```
	- 主要用途
		- ![[Pasted image 20251025110545.png]]
- <font color=red>按位与&</font>
	- 定义：参加运算的两个数据，按二进制位进行“与”运算
	- 运算规则：同时是1才为1，否则就是0
	- ```
	  a:01111010
	  b:10011000
	  a&b:00011000
	  ```
	- 主要用途
		- ![[Pasted image 20251025111047.png]]
- <font color=red>按位或 |</font>
	- 定义：参加运算的两个对象，按二进制位进行“或”运算。
	- 运算规则：同时是0才为0，否则就是1
	- ```
	  a:01111010
	  b:10011000
	  a|b:11111010
	  ```
	- 主要用途
		- ![[Pasted image 20251025113609.png]]
- <font color=red>按位异或 ^</font>
	- 定义：参加运算的两个数据，按二进制位进行“异或”运算
	- 运算规则：相同则为0，不同则为1
	- ```
	  a:01111010
	  b:10011000
	  a^b:11100010
	  ```
	- 主要用途
		- ![[Pasted image 20251025114026.png]]
- <font color=red>左移<<</font>
	- 定义：将一个运算对象的各二进制位全部左移若干位（左边的二进制位丢弃，右边补0）
	- ```
	  a=1010 1110
	  a=a<<2;
	  a=1011 1000
	  ```
	- 若左移时舍弃的高位不包含1，则每左移一位，相当于概述乘以2
	- <font color=greeen>m*2^n可以写成</font>m<<n;
- <font color=red>右移>></font>
	- 定义：将一个运算对象的各二进制位全部右移若干位,正数左补0，负数左补1，右边丢弃
	- ```
	  /*
	  00001011>>1
	  00000101=5
	  */
	  11>>1=5;
	  ```
	- 操作数每右移一位，相当于该数除以2(右移就是N/2，不用担心一处，但是要注意是整除，产生的小数部分直接丢弃)
- <font color=red>位运算赋值运算符</font>
	- ![[Pasted image 20251025120751.png]]
- 案例
	- ![[Pasted image 20251025121947.png]]
```
#include <iostream>
using namespace std;

int main() {
    int num = 612;
    // 假设用16位表示，从最高位(15)到最低位(0)
    for (int i = 15; i >= 0; i--) {
        int mask = 1 << i;    // 构造掩码
        if (num & mask) {
            cout << "1";
        } else {
            cout << "0";
        }
    }
    cout << endl;
    return 0;
}
```
# 7.面向对象编程
## 7.1类与对象
- 面向过程与面向对象
	- ![[Pasted image 20251026155725.png]]
- 类与对象的基本概念
	- ![[Pasted image 20251026160122.png]]
- <font color=red>类class</font>的定义(类名首字母一般大写)
	- 类里面的属性列表和函数列表需要用{}包围，同时，类的最后一定不能忘记<font color=greeen>分号</font>
	- ```
	  class ClassName{
		propertyModifier:  //属性修饰符，有public、protected、private
			propertoys  //属性列表
			functions  //函数列表（方法列表）
	  };
	  ```
	  
## 7.2构造函数
- 类对象
	- 使用类创建对象的过程，又称为类的实例化
	- ```
	  //类名    类对象（参数）；
	  ClassName classVar(param);
	  ```
- 构造函数与析构函数
	- 构造函数
		- ![[Pasted image 20251026162525.png]]
	- 构造函数参数
		- ![[Pasted image 20251026162839.png]]
	- 拷贝构造函数
		- ![[Pasted image 20251026165112.png]]
	- 析构函数
		- ![[Pasted image 20251026165137.png]]
		- ```
		  ~Destructor(){
		  //析构函数前面一定要加加~，并且是系统自动调用的
		  }
		  ```
	- [const成员函数](https://blog.csdn.net/weixin_45031801/article/details/134161230?spm=1001.2014.3001.5506))
## 7.3动态创建对象
- 当创建一个C++对象时，会发生两件事情
	- ![[Pasted image 20251026165744.png]]
- <font color=red>new操作符</font>
	- ![[Pasted image 20251026170126.png]]
	- ```
	  //new操作能确定在调用构造函数初始化之前内存分配是成功的，所以不用显示确定调用是否成功
	  ClassName*p=new ClassName();
	  ```
- <font color=red>delete操作符</font>
	- ![[Pasted image 20251026171042.png]]
## 7.4动态创建对象数组与普通数组
- 聚合初始化
	- ```
	  //栈上可以聚合初始化,但堆上必须提供一个默认的构造函数
	  Class Student{
	  public:
		  Student(){
			  cout<<111<<endl;
		  }
		  Student(string name,int age){
			  cout<<name<<endl;
			  cout<<age<<endl;
		  }
	  };
	  
	  int main(){
		  //栈聚合初始化
		  Student stu[]={{"zs",20},{"ww",21}};
		  //创建堆上对象数组必须提供构造函数
		  Student*pstr=new Student[20];
		  //删除
		  deletr[]pstu;
		  return 0;
	  }
	  ```
	- new/delete用于普通数组
		- ```
		  //创建字符数组
		  char*p1=new char[50];
		  
		  //创建整型数组
		  int*p2=new int[100];
		  //创建整型数组并初始化
		  int*p3=new int[10]{1,2,3,4,5,6,7,8,9,10};
		  //释放数组内存
		  delete[]p1;
		  delete[]p2;
		  delete[]p3;
		  ```
## 7.5静态成员变量与静态成员函数
- 静态成员变量
	- ![[Pasted image 20251028082747.png]]
- ```
  class ClassName{
  public:
	  static type paramter;
  };
  //静态成员在定义后必须初始化
  Type ClassName::paramter=value;
  //静态成员的引用可以使用类名或者对象名引用
  ClassName::paramter;
  ```
- 静态成员函数
	- ![[Pasted image 20251028084120.png]]
	- ```
	  class ClassName{
	  public:
		  static type funcName(paramtertype paramter){
		  
		  }
	  };
	  ```
	- [[C++其他使用细节#11.类中静态成员函数与类中普通函数的区别]]
	- 可以通过类名和对象名调用 
- const修饰类的成员函数
	- ![[Pasted image 20251028084621.png]]
	- ```
	  class ClassName{
	  public:
		  type func()const{
		  
		  }
	  };
	  ```
## 7.6this指针
- ![[Pasted image 20251028085053.png]]
- ![[Pasted image 20251028085123.png]]
- [[C++其他使用细节#10.this指针使用场景]] 
## 7.7访问限定符 友元函数
- 访问限定符
- [[C++其他使用细节#14private,public,protected的不同点与相同点]]
	- ![[Pasted image 20251029093237.png]]
- 友元函数
	- ![[Pasted image 20251029093301.png]]
	- 用<font color=red>friend</font>修饰的函数
	- ```
	  class Name{
	  public:
		  friend void func();
		};
		void func(){
		
		}
	  ```
## 7.8友元类
- 如果一个类是另一个类的友元类，<font color=red>友元类可以访问类的所有私有成员</font>
- 用friend修饰的类
- [[C++其他使用细节#12.友元的理解（友元函数与友元类）]]
## 7.9运算符重载
- ![[Pasted image 20251030131101.png]]
- ![[Pasted image 20251030131331.png]]
- 不能重载的运算符
	- ![[Pasted image 20251030131441.png]]
- 重载的两种形式
	- ![[Pasted image 20251030131527.png]]
- [[C++其他使用细节#13.学生成绩管理系统（友元与成员函数，私有公有函数的运用）]]
## 7.10继承和多态
- 继承和派生概念
	- ![[Pasted image 20251031071203.png]]
- 继承使用场景
	- ![[Pasted image 20251031071148.png]]
	- ```
	  class derived-class: access-specifier base-class
	  //derived-class 派生类，即继承自base-class创建的新类
	  //access-specifier继承访问修饰符（如果不写，默认为private)
	  //base-class基类，即要被继承的类
	  ```
	- 不同的继承方式会影响基类成员在派生类中的访问权限
		- ![[Pasted image 20251031072007.png]]
	- 继承中的构造和析构
		- ![[Pasted image 20251031075326.png]]
		- ![[Pasted image 20251031075503.png]]
	- 通过using来继承基类构造函数
		- ![[Pasted image 20251031075625.png]]
	- 构造和析构的调用顺序
		- 构造函数：先调用基类的构造函数，在调用子类的，基类没有默认构造函数，则编译错误
		- 析构函数：先调用子类析构，再调用基类析构
- 多继承
	- 一个派生类有多个基类
	- ```
	  class D:public A,protected B,private C;//类D新增加的成员
	  ```
	- 多继承构造函数
		- ![[Pasted image 20251031090841.png]]
	- 多继承命名冲突
		- ![[Pasted image 20251031093102.png]]
- 菱形继承
	- ![[Pasted image 20251101084054.png]]
	- 类D使用类A中的变量时会发生命名冲突，变量不明确。<font color=red>所以使用时要显式类的作用域</font>
- 虚继承
	- ![[Pasted image 20251101084841.png]]
	- 虚继承构造函数
		- ![[Pasted image 20251101090417.png]]
- 类的多态
	- ![[Pasted image 20251101093536.png]]
	- 基本概念
		- ![[Pasted image 20251101093732.png]]
	- 构成条件
		1. 必须存在继承关系
		2. 继承关系中必须有同名的虚函数，并且他们是覆盖关系（函数原型相同）
		3. 存在基类的指针，通过该指针调用虚函数
		4. ![[Pasted image 20251101094357.png]]
	- 通过基类指针只能访问派生类的成员变量，但是不能访问派生类成员函数。为了能让基类指针访问派生类的成员函数，cpp增加了虚函数`virtual void info()...`
	- 引用实现多态
		- <font color=red>指针可以随时改变方向，而引用只能指代固定的对象，在多态性方面缺乏表现力</font>
		- ![[Pasted image 20251101095220.png]]
	- 虚函数
		- ![[Pasted image 20251101095349.png]]
	- 虚析构函数
		- ![[Pasted image 20251101100802.png]]
		- ![[Pasted image 20251101100540.png]]
	- 虚函数表
		- ![[Pasted image 20251101104620.png]]
	- C++如何实现动态绑定
		- ![[Pasted image 20251101105119.png]]
		- ![[Pasted image 20251101105231.png]]
	- 抽象基类和纯虚函数
		-  ![[Pasted image 20251101105518.png]]
		- 纯虚函数
			- ![[Pasted image 20251101105853.png]]
## 7.11嵌套类和局部类
- 嵌套类
	- ![[Pasted image 20251104085150.png]]
	- 特点
		1. 嵌套类不可以访问外围类的任何成员
		2. 外围类可以通过对象访问嵌套类的公有成员，但不能访问保护和私有成员
		3. 嵌套类只能由外围类使用
- 局部类
	- 类可以定义在函数体内，这样的类称为局部类。局部类只在定义它的局部域内可见
	- 局部类的成员函数必须被定义在类体中
	- 局部类中不能有静态成员函数
	- 在实践中，局部类很少使用
# 8.STL
- STL基本组成
	- ![[Pasted image 20251102100317.png]]
## 8.1vector(向量/顺序表)
- 概念
	- <font color=red>时一个能够存放任意类型的动态数组</font>
	- <font color=red>是同一种类型的对象的集合，每一个对象都有一个对应的整数索引值</font>
	- <font color=red>被称为</font><font color=greeen></font><font color=greeen>容器</font><font color=red>可以包含其他对象，一个容器中的所有对象都必须是同一种类型的</font>
- 使用
	- <font color=red>必须包含头文件</font>`#include<vector>`
	- <font color=red>声明与初始化</font>
		- ```
		  //整形数组
		  vector<int>vec1={1,2,3};
		  //char型数组
		  vector<char>vec2={'h','e','l'};
		  //double
		  vector<double>vec3={1.1,2.2,3.3};
		  ```
		- 利用构造函数初始化
		- ![[Pasted image 20251024194335.png]]
	- <font color red>遍历函数</font>
		- ![[Pasted image 20251024195113.png]]
	- 增加函数
		- ![[Pasted image 20251025085317.png]]
	- 删除函数
		- ![[Pasted image 20251025085843.png]]
	 - 判断函数
		 - ![[Pasted image 20251025090401.png]]
	- 大小函数
		- ![[Pasted image 20251025090518.png]]
	- 其他函数
		- ![[Pasted image 20251025090747.png]]
	- [[C++其他使用细节#2.vecor如何申请多个动态数组]]
## 8.2queue(队列)
- 定义
	- 是一种先进先出的数据结构，它有两个出口
	- queue模板类的定义在`#include<queue>`中
	- ```
	  queue<int>q1;
	  queue<double>q2;
	  ```
- 逻辑
	- ![[Pasted image 20251027093124.png]]
	- 队列容器允许从一端新增元素，从另一端移除元素
	- 队列中只有队头和队尾可以被外界使用，因此队列不允许有遍历的行为
	- 队列中进数据成为-入队 push
	- 队列中出数据称为-出队pop
- 构造函数
	- ```
	  queue<T>que T;//queue采用模板类实现，queue对象的默认构造形式
	  queue(const queue&que);//拷贝构造函数
	  
	  //声明
	  queue<int>q1;
	  queue<int>q2(q1);
	  queue<int>q3=q1;
	  ```
- 操作
	- ```
	  push(elem);//往队尾添加元素
	  pop();//从队头一处第一个元素
	  back();//返回最后一个元素
	  front();//返回第一个元素
	  empty();//判断队列是否为空
	  size();//返回队列的大小
	  ```
- <font color=red>deque容器</font>
	- `#include<deque>`
	- deque双端队列，可以对头端和尾端进行插入删除操作
	- deque队列为一个给定类型的元素进行线性处理，像向量一样，它
		能够快速地随机访问任一个元素，并且能够高效地插入和删除容器
		的尾部元素。但它又与vector不同，deque支持高效插入和删除容
		器的头部元素。
	- ![[Pasted image 20251027102118.png]]
	- 构造函数
		- ```
		  deque<T>deqT;//默认构造形式
		  deque<T>deqT(int size);//默认构造，初始化大小
		  deque(beg,end);//构造函数将[beg,end)区间的元素拷贝给本身
		  deque(n,elem);//构造函数将n个elem拷贝给本身
		  deque(const deque&deq);//拷贝构造函数
		  ```
	- 添加函数
		- ```
		  d.push_front(const T&x);//头部添加元素
		  d.push_back(const T&x);//尾部添加元素
		  d.insert(iterator it,const T&x);//任意位置插入一个元素
		  d.insert(iterator it,int n,const T& x);//任意位置插入n个相同元素
		  d.insert(iterator it,iterator first,iterator last);//插入另一个向量的[first,lase)间的数据
		  ```
	- 删除函数
		- ```
		  //头部删除函数
		  d1.pop_front();
		  //末尾删除函数
		  d1.pop_back(); 
		  //任意位置删除一个元素
		  d1.erase(iterator it);
		  //删除[first,lase)之间的元素
		  d1.erase(iterator first,iterator,lase);
		  //清空所有元素
		  d1.clear();
		  ```
	- 访问函数
		- ```
		  //下标访问，并不会检查是否越界
		  deq[1];
		  //at方法访问，会检查是否越界,越界啧抛出out of range异常
		  deq.at[1];
		  //访问第一个元素
		  deq.front();
		  //访问最后一个元素
		  deq.back();
		  ```
	- 容量函数
		- ```
		  //容器大小
		  d.size();
		  //容器最大容量
		  d.max_size();
		  //更改容器大小
		  d.resize();
		  //容器判空
		  deq.empty();
		  //减少容器大小到满足元素所占存储空间的大小
		  deq.shrink_to_fit();
		  ```
	- 其他函数
		- ```
		  //多个元素赋值，该函数同样可以用 *数量+值* *迭代器范围（可跨容器赋值）* *初始化列表* 赋值，
		  //先清空再赋值，不会保留原有元素（直接用=赋值可能会遗留原有元素）
		  deq.assign(int nSize,const T&x);
		  //交换两个同类型容器的元素
		  swap(deque&);
		  ```
	- [[C++其他使用细节#7.deque与vector的区别]]
## 8.3list(双向链表)
- 初始化
	- ![[Pasted image 20251102110610.png]]
- 头部插入和头部删除
	- ![[Pasted image 20251102111009.png]]
- 尾部插入和尾部删除
	- ![[Pasted image 20251102111059.png]]
- 指定位置插入
	- ![[Pasted image 20251102111135.png]]
- 指定位置删除
	- ![[Pasted image 20251102111740.png]]
- <font color=red>在指定位置进行操作时，使用迭代器不能进行+n的操作，若要实现区间操作，可以先定义iterator it=begin/end，在按需进行++或--</font>
- list中的排序sort()
	- ![[Pasted image 20251102112458.png]]
	- 若要降序排序，可实现一个辅助函数进行自定义排序状态
- list中的反转reverse()
	- ![[Pasted image 20251102112737.png]]
- list常用函数列表
	- ![[Pasted image 20251102113031.png]]
## 8.4set/multiset关联式容器
- 底层结构使用二叉树实现
- 所有的元素在插入时会自动被排序，而<font color=red>set容器中不允许有重复的元素，multiset允许</font>
- set（自动升序）
	- ```
	  //构造与赋值
	  set<T>st//默认构造函数
	  set(const set&st)//拷贝构造函数
	  /set&operator=(const set&st)//重载等号操作符
	  
	  //插入与删除
	  insert(elem)//插入元素
	  clear()//清除所有元素
	  erase(pos)//删除pos迭代器所指元素，返回下一个元素的迭代器
	  erase(beg,end)//删除区间[begin,end)的所有元素，返回下一个元素的迭代器
	  erase(elem)//删除容器中值为elem的元素
	  
	  //大小与交换
	  size()
	  empty()
	  swap(st)
	  
	  //统计与查找
	  find(key)//查找key是否存在，若存在返回该键的元素的迭代器，不存在，返回set.end()
	  count(key)//统计key的元素的个数(set里元素不重复，count=0/1)
	  ```
- set与multiset的区别
	- ![[Pasted image 20251105083446.png]]
- multiset
	- ```
	  lower_bound(elem)查找第一个大于等于elem的元素的迭代器
	  upper_bound(elelm)查找第一个大于elem的元素的迭代器
	  ```
## 8.5map/multimap关联容器（映射）
- 概念
	- ![[Pasted image 20251105125716.png]]
- pair对组
	- ![[Pasted image 20251105125919.png]]
	- 标准头文件`#include<utility>`
	- vs里面，某些编译器可以不声明这个头文件直接使用，貌似在cpp中，pair被放入了std命名空间中了
	- 初始化
		- ![[Pasted image 20251105130222.png]]
	- 数据访问
		- ![[Pasted image 20251105130336.png]]
	- make_pair
		- ![[Pasted image 20251105130439.png]]
- map
	- 构造与赋值
		- ```
		  map<T,T>m//默认构造函数
		  map(const map&mp)//拷贝构造函数
		  map&operator=（const map&mp)//重载等号操作符
		  ```
- [[C++其他使用细节#21.unordered_map]]
## 8.6STL常用算法
- `算法主要是由头文件<algorithm><functional><numeric>组成`
	- algorithm时所有stl头文件中最大的一个，范围涉及到比较，交换，查找，遍历，赋值，修改等等
	- numeric体积很小，只包括几个再序列上面进行简单数学运算的模板函数
	- functional定义了一些模板类，用以声明函数对象
	- [[C++其他使用细节#19_Pred(Predicate)谓语是什么？]]
- 遍历算法
	- for_each（遍历容器）
		- ```
		  for_each(iterator beg,iterator,end,_fund);
		  //遍历算法，遍历容器元素
		  //beg 开始迭代器，end结束迭代器
		  //_func函数或者函数对象
		  ```
	- transform（搬运容器到另一个容器）
		- ```
		  transform(iterator beg1,iterator,end1,iterator beg2,_func)
		  //beg1源容器开始迭代器
		  //end1源容器结束迭代器
		  //beg2目标容器开始迭代器
		  //_func函数或者函数对象
		  ```
- 查找算法
	- find（查找元素）
		- 查找指定元素，找到返回指定元素的迭代器，找不到返回结束迭代器end()
		- ```
		  find(iterator beg,iterator end,value);
		  ```
	- find_if（按条件查找元素）
		- 按值查找元素，返回指定位置迭代器，找不到返回结束迭代器位置
		- ```
		  find_if(iterator beg,iterator end,_Pred);
		  //_Pred函数或者谓语（返回bool类型的仿函数）
		  ```
	- adjacent_find(查找相邻重复元素)
		- 查找相邻重复元素，返回相邻元素的第一个位置的迭代器
		- ```
		  adjacent_find(iterator beg,iterator end);
		  ```
	- binary_search（二分查找法）
		- 查找指定元素是否存在
		- ```
		  bool binary_search(iterator beg,iterator end,value);
		  //在无序序列中不可用
		  ```
	- count（统计元素个数）
		- ```
		  count(iterator beg,iterator end,value);
		  //value统计的元素
		  ```
	- count_if（按条件统计元素个数）
		- ```
		  count_if(iterator beg,iterator end,_Pred);
		  //_Pred谓语
		  ```
- 排序算法
	- sort(对容器内元素进行排序)
		- ```
		  sort(iterator beg,iterator end,Pred);
		  //自动升序，降序可以自定义Pred
		  ```
	- random_shuffle(洗牌，指定范围内的元素随机调整次序)
		- ```
		  random_shuffle(iterator begin,iterator end);
		  ```
	- merge(容器元素合并，并存储到另一容器中)
		- ```
		  merge(iterator beg1,iterator end1,iterator beg2,iterator end2,iterator dest);
		  //两个容器必须是有序的
		  //beg1,end1容器1的迭代
		  //beg2,end2容器2的迭代
		  //dest目标容器的开始迭代器
		  ```
	- reverse(反转指定范围的元素)
		- ```
		  reverse(iterator beg,iterator end);
		  ```
- 拷贝和替换算法
	- copy(容器内指定范围的元素拷贝到另一个容器中)
		- ```
		  copy(itereator beg,iterator end,iterator dest);
		  //dest目标开始迭代器
		  ```
	- replace(将容器内指定范围的元素修改为新元素)
		- ```
		  replace(iterator beg,iterator end,oldvalue,newvalue);
		  ```
	- replace_if(容器内指定范围满足条件的元素替换为新元素)
		- ```
		  reoplace_if(iterator beg,iterator end,_pred,newvalue);
		  ```
	- swap(交换两个容器的元素)
		- ```
		  swap(container c1,container c2);
		  //c1,c2互换的两个容器
		  ```
- 算术生成算法
	- 属于小型算法，使用时包含的头文件为`#include<numeric>`
	- accumulate(计算容器元素累计总和)
		- ```
		  accumulate(iterator beg,iterator end,value);
		  //value起始值
		  ```
		- [[C++其他使用细节#​**1. `accumulate`函数详解**​]]
		- [[C++其他使用细节#3.2`std accumulate`自定义二元操作的原理详解]]
	- fill(向容器中添加元素)
		- ```
		  fill(iterator beg,iterator end,value);
		  //value填充值
		  ```
- 常用集合算法
	- set_intersection(求两个容器的交集)
		- ```
		  set_intersection(iterator beg1,iterator end1,itertor beg2,iterator end2,iterator dest);
		  //两个集合必须是有序序列
		  //目标容器开辟空间需要从两个容器中去小值
		  //返回值是交集中最后一个元素的位置
		  //大容器包含小容器，开辟空间，去小容器的size即可
		  ```
	- set_union(求两个的容器的并集)
		- ```
		  set_union(iterator beg1,iterator end1,itertor beg2,iterator end2,iterator dest);
		  //两个容器没有交集，并集就是两个容器size相加
		  ```
	- set_difference(求两个容器的差集)
		- ```
		  set_difference(iterator beg1,iterator end1,itertor beg2,iterator end2,iterator dest);
		  //两个容器香蕉，开辟空间，取大容器的size即可
		  ```
# 9.异常处理
- 概述
	- ![[Pasted image 20251102171611.png]]
	- ![[Pasted image 20251102171737.png]]
- 标准异常
	- ![[Pasted image 20251102172006.png]]
	- ![[Pasted image 20251102172345.png]]
- 抛出异常
	- ![[Pasted image 20251102172536.png]]
- 捕获异常
	- ![[Pasted image 20251102172806.png]]
- 打印throw关键字抛出的异常信息
	- ![[Pasted image 20251102173136.png]]
- 自定义异常
	- 通过继承和重载exception类来定义新的异常
	- ```
	  #include<iostream>
	  #include<exception>
	  
	  class MyException:public exception{
		public:
			const char* what()const throw(){
				return "my test exception";
			}
		  
	  }
	  //what()是一个由exception类提供的公共方法。它用于返回异常的原因
	  ```
	- ![[Pasted image 20251103181357.png]]
# 10.模板
- 模板概念
	- ![[Pasted image 20251104095919.png]]
	- 函数模板
		- ```
		  //T代表的是一种类型
		  //也可以用class来代替typename
		  template<typename T1,typename T2,...,typename Tn>
		  返回类型 函数名（参数列表）{
			  //函数体
		  }
		  ```
	- 函数模板原理
		- ![[Pasted image 20251104103028.png]]
	- 类模板
		- ```
		  template<class T1,class T2,...,class Tn>
		  class 类模板名{
			  //类内成员声明
		  };
		  ```
		- 类模板实例化
			- 需要在类模板后面跟<>,然后将实例化的类型放在<>中
		- <font color=red>类模板中的成员函数若是放在类外定义时，需要加模板参数列表</font>
			- ![[Pasted image 20251104111737.png]]
	- 模板别名
		- ![[Pasted image 20251104114345.png]]
		- ![[Pasted image 20251104114431.png]]
- [[C++其他使用细节#19.模板在编译时的原理]]
# 11文件操作
- 数据流概念
	- 一组有序，有起点和终点的字节数据序列。包括输入流和输出流
	- cpp通过一种成为流的机制提供了更为精良的输入和输出方法。流是一种灵活且面向对象的I/O方法。
	- 根据操作对象不同分为<font color=red>文件流。字符串流。控制台流</font>
- 控制台流
	- ![[Pasted image 20251104165724.png]]
- 文件流
	- ![[Pasted image 20251104170000.png]]
	- 由于文件设备不像显示器屏幕和键盘那样标准的默认设备，所以我们定义一个流对象
		- ![[Pasted image 20251104170155.png]]
	- mode属性表
		- ![[Pasted image 20251104170524.png]]
	- 打开文件属性值
		- ![[Pasted image 20251104170856.png]]
- 字符串流
	- ![[Pasted image 20251104170927.png]]
- 文件的输入与输出
	- 打开文件
		- ![[Pasted image 20251104171115.png]]
		- ![[Pasted image 20251104171353.png]]
		- open函数打开文件的默认方式与类相关
			- ![[Pasted image 20251104171456.png]]
	- 写入和读取
		- ![[Pasted image 20251104171554.png]]
	- 关闭文件
		- ![[Pasted image 20251104171723.png]]
# C++11新特性
## 1.lambda表达式
- 一个匿名类函数，在编译时将表达式转换为匿名类函数
- ```
  [capture-list](parameters)mutable->return-type{statement}
  //捕获列表（参数）->返回值{函数体}；
  ```
- ![[Pasted image 20251103081932.png]]
- 捕获列表
	- 描述了上下文中哪些数据可以被lambda使用，以及实用的方式传值还是传引用
		- ```
		  [a,&b]//其中a以复制捕获b以引用捕获
		  [this]以引用捕获当前对象*this
		  [&]以引用捕获所有用于lambda体内的自动变量，并以引用捕获当前对象，若存在
		  [=]以复制捕获所有用于lambda体内的自动变量，并以引用捕获当前对象，若存在
		  []不捕获，大部分情况不捕获就可以了
		  ```
	- 参数列表和饭hi值类型都是可选部分，而捕捉列表和函数体可以为空，最简单的lambda函数：[]{}；该函数不能做任何事，没有意义
	- 函数对象又称为仿函数，即可以像函数一样使用的对象，就是在类中重载了operator()运算符的类对象，从使用方式上来看，函数对象与lambda表达式完全一样
- [综合案例](D:\Develop\vs2022\develop\ProblemSolve\ProblemSolve\StudentManager-lambda.cpp)
## 2.auto
- auto与const
	- ![[Pasted image 20251103151239.png]]
	- <font color=red>当类型不为引用时，auto的推导结果将不保留表达式的const属性</font>
	- <font color=red>当类型为引用时，auto的推导结果将保留表达式的const属性</font>
- auto高级用法
	- 除了可以独立使用，还可以和某些具体类型混合使用，这样auto表示的就是“半个”类型，而不是完整类型
	- ```
	  int x=0;
	  auto*pt1=&x;//pt1为int*,auto推导为int
	  auto pt2=&x;//pt2为int*,auto推导为int*
	  auto&r1=x;//r1为int&,auto推导为int
	  auto r2=r1;//r2为int,auto推导为int
	  ```
- auto的限制（在C++11标准的限制）
	- 不能在函数的参数中使用(yes)
	- 不能作用于类的非静态成员(no)
	- 不能作用于模板参数
	- 不能用于推导数组类型
- [[C++其他使用细节#17.用auto推导为数组的方式]]
## 3.decltype
- `#include<typeinfo>->typeid(num3).name`
- ![[Pasted image 20251108084920.png]]
- ```
  auto num1=100;
  auto num2=200;
  decltype (num1+num2)num3;
  //num3的类型就是num1+num2最终的结果的类型
  ```
- 在泛型编程中，可能需要通过参数的运算来得到返回值的类型
	- ```
	  #include<iostream>
	  template<typename R,typename T,typename U>
	  R add(T t,U u){
		return t+u;}
		int main(){
			int a=1;float b=2.0;
			auto c=add<decltype(a+b)>(a,b);
			std::cout<<c<<std::endl;
			return 0;
		}
		```
	- ```
	  template<typename T,typename U>
	  decltype(t+u)add(T t,U u){return t+u;}
	  //cpp的返回值是前置语法，在返回值定义的时候参数变量还不存在，所以报错！
	  template<typename T,typename U>
	  auto add(T t,U u)->decltype(t9/60+u)//尾随返回类型
	  {
		return t+u;
	  }
	  c++14开始可以直接写成
	  template<class T,class U>
	  auto add(T t,U u){return T+u032/69633```
	- 
## 4.右值引用&&
- [右值引用深度解析](https://blog.csdn.net/weixin_45031801/article/details/141219782?spm=1001.2014.3001.5506))
- c++98中提出了引用的概念，引用即别名，引用变量与其引用实体公共同一块内存空间，而引用的底层是通过指针来实现的，因此使用引用，可以提高程序的可读性
- 比如交换两个变量的值，消除两个对象交互时不必要的对象拷贝，节省运算存储资源，提高效率
	- ```
	  void change(int&n1,int&n2){
		  int temp=n1;
		  n1=n2;
		  n2=temp;
	  }
	  ```
- C++11中引入了右值引用，右值引用也是别名，但其只能对右值引用
	- ```
	  int func1(int v1,int v2){return v1+v2; }
	  int main(){
		  const int&&num1=10;//右值示例
		  //引用函数返回值，返回值是一个临时变量，为右值
		  int&&num2=func1(10,20);
		  std::cout<<num1<<std::endl;
		  std::cout<<num2<<std::endl;
		  return 0;
	  }
	  ```
- 右值与左值
	- 一般认为：左值可放在赋值符号的左边，右值课放在赋值符号的右边，或者能够取地址的成为左值，反之称为右值
	- 左值也能放在赋值符号的右边，右值只能放在赋值符号的右边
		- ```
		  const int num4=30;//特例：num4虽然是左值，但是为const常量，只读不允许修改
		  cout<<&num4<<endl;//num4可以取地址，使用严格来看也是左值
		  int num3=10;
		  num3+2=200;//编译失败：因为num3+2的结果是一个临时变量，没有具体名称，也不能取地址，因此为右值
		  ```
## 5.移动语义
	转移语义可以将资源（堆、系统对象等）从一个对象转移到另一个对象，这样可以减少不必要的临时对象的创建、拷贝及销毁。移动语义与拷贝语义是相对的，可以类比文件的剪切和拷贝。在现有的C++机制中，自定义的类要实现转移语义，需要定义移动构造函数，还可以定义转移赋值操作符。
- <font color=red>注意：</font>
	- 参数（右值）的符号必须是&&
	- 参数（右值）不可以是常量，因为我们需要修改右值
	- 参数（右值）的资源链接和标记必须修改，否则，右值的析构函数就会释放资源。转移到新对象的资源也就无效了
- <font color=red>标准库函数std::move</font>：将左值变成右值
# 6.列表初始化
	C++11扩大了用大括号扩起的列表（初始化列表）的使用范围，使其可用于所有的内置类型和用户自定义的类型，使用初始化列表时，可添加等号，也可不添加
# 7.智能指针
1. shared_ptr
	- 多个shared_ptr智能指针可以共同<font color=red>使用同一块堆内存</font>。并且，由于该类型智能指针在实现上采用的是引用计数机制，即便有一个shared_ptr指针放弃了堆内存的“使用权”（引用计数减1），也不会影响其他指向同一堆内存的shared_ptr指针（只有引用计数为0时，堆内存才会被自动释放）。
	- 创建
		- ```
		  shared_ptr<int>p1;//不传入任何实参
		  shared_ptr<int>p2(nullptr);//传入空指针nullptr
		  //空的shared_ptr指针，其初始引用计数为0，而不是1.
		  //在构建shared_ptr之只能指针，也可以明确其指向
		  shared_ptr<int>p(new int(5));
		  //使用std::make_shared<T>模板函数，也可以用于初始化
		  shared_ptr<int>p=make_shared<int>(5);
		  shared_ptr<int>p3;
		  //调用拷贝构造函数shared_ptr<int>p4(p3);
		  shared_ptr<int>p4=p3;
		  //调用移动构造函数
		  shared_ptr<int>p5(mave(p4));
		  shared_ptr<int>5=move(p4);
		  
		  //指定default_delete作为释放规则
		  shared_ptr<int>p1(new int[3],default_delete<int[]>());
		  //初始化智能指针，并自定义释放规则
		  shared_ptr<int>p2(new int[3],deleteInt);
		  void deleteInt(int*p){delete[]p;}
		  ```
2. 