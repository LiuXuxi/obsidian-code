

---

  

## 一、填空题相关（每题1分，共10分）

  

---

  

**1.** 包有什么作用？程序中如何创建或设置包？语法上有何规定？

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

**包的作用：**

- ① **组织管理类**：将功能相关的类组织在一起，方便管理和查找

- ② **避免命名冲突**：不同包中可以有同名类，通过全限定名区分

- ③ **访问控制**：包级访问权限（default）限制外部包对类成员的访问

  

**语法规定：**

- 创建包：`package 包名;` 必须是 Java 源文件的**第一条语句**（注释除外）

- 包名习惯全小写，对应文件夹层次结构，如 `package com.example.test;`

- 带包的类编译运行：`javac -d . Test.java` → `java com.example.test.Test`

  

</details>

  

---

  

**2.** 构造方法有什么作用？有什么特点？与普通方法有什么不同？如何使用？

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

**作用：** 在创建对象（new）时**初始化对象的成员变量**，为对象分配内存后进行属性赋值。

  

**特点：**

- ① 方法名**必须与类名完全相同**

- ② **没有返回值类型**（连 void 也不写）

- ③ 可被**重载**（多个不同参数的构造方法）

- ④ 若未定义任何构造方法，编译器**自动提供**默认无参构造方法

  

**与普通方法的不同：**

|| 构造方法 | 普通方法 |

||----------|----------|

|| 必须与类同名 | 任意合法名称 |

|| 无返回值类型 | 必须有返回值类型或 void |

|| new 时自动调用 | 需显式调用 |

|| 不能被继承 | 可被继承 |

  

**使用：** `new 类名(参数);` 如 `Student s = new Student("张三", 20);`

  

</details>

  

---

  

**3.** 接口与类有什么不同？

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

| 对比项 | 接口 (interface) | 类 (class) |

|--------|------------------|------------|

| 实例化 | **不能**实例化 | 可以实例化（抽象类除外） |

| 方法 | 默认 `public abstract`（Java 8+ 可有 default/static 方法） | 必须有方法体（抽象方法除外） |

| 变量 | 只能是 `public static final` 常量 | 可以有实例变量、静态变量 |

| 构造方法 | **没有**构造方法 | 有构造方法 |

| 继承 | 可以**多继承**接口：`interface A extends B, C` | 只能**单继承**：`class A extends B` |

| 实现 | 类可以实现**多个**接口 | 类只能继承一个父类 |

| 访问修饰符 | 方法隐式 `public`，接口本身可 `public` 或默认 | 所有四种修饰符均可 |

  

</details>

  

---

  

**4.** 关键字 import、class、package 在类文件中出现的顺序有什么要求？

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

Java 源文件中各元素的**必须顺序**：

  

```

1. package 语句        （可选，如有则必须是第一条语句）

2. import 语句         （可选，可有多条，紧跟 package 之后）

3. class/interface 定义 （必须有）

```

  

```java

package com.example;       // 第1：包声明

  

import java.util.List;     // 第2：导入语句

import java.io.*;

  

public class Test {        // 第3：类定义

    // ...

}

```

  

</details>

  

---

  

**5.** 类成员的访问修饰符有哪些？他们的作用域（可见性）有什么不同？

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

Java 有**四种**访问权限修饰符，可见性从窄到宽：

  

| 修饰符 | 同类 | 同包 | 子类 | 全局（任意类） |

|--------|------|------|------|----------------|

| `private` | ✅ | ❌ | ❌ | ❌ |

| `default`（不写） | ✅ | ✅ | ❌ | ❌ |

| `protected` | ✅ | ✅ | ✅ | ❌ |

| `public` | ✅ | ✅ | ✅ | ✅ |

  

- **private**：封装核心，只有本类能访问

- **default**：包级访问，常用于包内部协作的类

- **protected**：为子类开放，子类可跨包访问

- **public**：完全公开，API 对外接口

  

</details>

  

---

  

**6.** 对于检查性异常（Checked 异常）有哪两种处理方式？多种异常时如何捕获处理或抛出？

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

**两种处理方式：**

  

① **try-catch 捕获处理：**

```java

try {

    FileReader fr = new FileReader("test.txt");

} catch (FileNotFoundException e) {

    System.out.println("文件未找到");

}

```

  

② **throws 声明抛出：**

```java

public void readFile() throws IOException {

    FileReader fr = new FileReader("test.txt");

}

```

  

**多种异常处理：**

```java

try {

    // 可能抛出多种异常的代码

} catch (FileNotFoundException e) {  // 子类异常在前

    // 处理文件未找到

} catch (IOException e) {            // 父类异常在后

    // 处理其他 IO 异常

} finally {

    // 始终执行的清理代码

}

```

  

> ⚠️ catch 顺序：**先子类后父类**，否则父类会先捕获所有异常导致子类的 catch 永远不执行（编译错误）。

  

</details>

  

---

  

**7.** 已知 Math.random() 返回 [0.0, 1.0) 之间的 double 值，如何编写表达式得到约定范围 [m, n] 的值？

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

```java

int result = (int)(Math.random() * (n - m + 1)) + m;

```

  

**推导过程：**

1. `Math.random()` → [0.0, 1.0)

2. `Math.random() * (n - m + 1)` → [0.0, n - m + 1)

3. `(int)(...)` → [0, n - m]（整数）

4. `+ m` → **[m, n]**

  

**示例：** 获取 [5, 10] 之间的随机整数：

```java

int num = (int)(Math.random() * 6) + 5;  // 6 = 10 - 5 + 1

```

  

</details>

  

---

  

**8.** 掌握一维和二维数组的声明和创建的基本语法。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

**一维数组：**

```java

// 声明

int[] a;

int a[];

  

// 创建（静态初始化）

int[] a = {1, 2, 3};

int[] a = new int[]{1, 2, 3};

  

// 创建（动态初始化）

int[] a = new int[5];    // 5 个元素，默认值 0

```

  

**二维数组：**

```java

// 声明

int[][] a;

int a[][];

int[] a[];    // 合法但少用

  

// 创建（静态初始化）

int[][] a = {{1,2}, {3,4,5}, {6}};

  

// 创建（动态初始化）

int[][] a = new int[3][4];  // 3行4列（矩形）

int[][] a = new int[3][];   // 3行，每行列数不同（锯齿形）

a[0] = new int[2];

a[1] = new int[5];

```

  

</details>

  

---

  

**9.** 掌握字符串方法 substring(m,n) 的使用。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

```java

String substring(int beginIndex)           // 从 beginIndex 到末尾

String substring(int beginIndex, int endIndex) // 从 beginIndex 到 endIndex-1

```

  

**规则：前闭后开 [m, n)**

  

```java

String s = "HelloWorld";

s.substring(0, 5);    // "Hello"  (索引 0-4)

s.substring(5);       // "World"  (索引 5 到末尾)

s.substring(3, 7);    // "loWo"   (索引 3-6)

```

  

| 索引 | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |

|------|---|---|---|---|---|---|---|---|---|---|

| 字符 | H | e | l | l | o | W | o | r | l | d |

  

> ⚠️ `substring(m, n)` 不包含索引 n 的字符。

  

</details>

  

---

  

**10.** 如何调用包装类 Integer 的静态方法将数字字串转换为整形值？

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

```java

// 方法1：parseInt（返回 int 基本类型）

int num = Integer.parseInt("123");    // num = 123

  

// 方法2：valueOf（返回 Integer 对象）

Integer num = Integer.valueOf("123"); // num = 123 (Integer 对象)

  

// 处理异常

try {

    int num = Integer.parseInt("abc"); // 抛出 NumberFormatException

} catch (NumberFormatException e) {

    System.out.println("字符串格式不正确");

}

```

  

| 方法 | 返回类型 | 说明 |

|------|----------|------|

| `Integer.parseInt(String)` | `int` | 最常用，直接得基本类型 |

| `Integer.valueOf(String)` | `Integer` | 返回包装对象，可利用缓存池 |

  

</details>

  

---

  

**11.** java.lang 包中的哪个类可用于创建线程安全的可变字符串对象？哪个用于创建非线程安全的可变字符串对象？

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

| 类 | 线程安全 | 可变性 | 性能 |

|----|----------|--------|------|

| **StringBuffer** | ✅ 线程安全（方法 synchronized） | 可变 | 较慢 |

| **StringBuilder** | ❌ 非线程安全 | 可变 | 较快 |

| String | ✅ 不可变（immutable） | **不可变** | — |

  

```java

// 线程安全

StringBuffer sb1 = new StringBuffer("hello");

sb1.append(" world");

  

// 非线程安全（单线程优先使用）

StringBuilder sb2 = new StringBuilder("hello");

sb2.append(" world");

```

  

> **记忆：** Buffer 像保险柜（安全但慢），Builder 像工具箱（快但不安全）。

  

</details>

  

---

  

**12.** 使用 new 创建一个对象实例时，其成员变量会在什么内存中存放？其对象引用（地址）又存放在什么内存中？

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

| 内容 | 存放位置 | 说明 |

|------|----------|------|

| **对象（成员变量）** | **堆内存（Heap）** | new 出来的对象都在堆中，由 GC 管理 |

| **对象引用（地址）** | **栈内存（Stack）** | 局部变量、方法参数引用在栈中 |

| **静态变量** | **方法区/元空间（Method Area）** | 类级别的变量 |

  

```

栈 (Stack)              堆 (Heap)

┌───────────┐          ┌────────────────┐

│ p ────────┼─────────→│ Person 对象    │

│ (引用地址) │          │ name = "张三"  │

└───────────┘          │ age = 20       │

                       └────────────────┘

```

  

</details>

  

---

  

**13.** 掌握 TCP Socket 网络程序开发的客户端和服务器端编程的基本方法及流程。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

**服务端流程：**

```java

// 1. 创建 ServerSocket，绑定端口

ServerSocket server = new ServerSocket(8888);

  

// 2. 监听连接（阻塞等待）

Socket client = server.accept();

  

// 3. 获取输入/输出流

BufferedReader in = new BufferedReader(

    new InputStreamReader(client.getInputStream()));

PrintWriter out = new PrintWriter(client.getOutputStream(), true);

  

// 4. 读写数据

String msg = in.readLine();

out.println("回复: " + msg);

  

// 5. 关闭连接

client.close();

server.close();

```

  

**客户端流程：**

```java

// 1. 创建 Socket，连接服务器

Socket socket = new Socket("127.0.0.1", 8888);

  

// 2. 获取输入/输出流

PrintWriter out = new PrintWriter(socket.getOutputStream(), true);

BufferedReader in = new BufferedReader(

    new InputStreamReader(socket.getInputStream()));

  

// 3. 读写数据

out.println("Hello Server");

String response = in.readLine();

  

// 4. 关闭连接

socket.close();

```

  

</details>

  

---

  

**14.** 对于 Java 异形二维数组，如何得到其行数和各一维数据的列数？

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

```java

int[][] a = {{1,2}, {3,4,5}, {6,7,8,9}};

  

int rows = a.length;       // 行数 = 3（外层数组长度）

  

int cols0 = a[0].length;   // 第0行列数 = 2

int cols1 = a[1].length;   // 第1行列数 = 3

int cols2 = a[2].length;   // 第2行列数 = 4

  

// 遍历异形数组

for (int i = 0; i < a.length; i++) {

    for (int j = 0; j < a[i].length; j++) {

        System.out.print(a[i][j] + " ");

    }

    System.out.println();

}

```

  

> **a.length** = 行数（外层数组长度），**a[i].length** = 第 i 行的列数。

  

</details>

  

---

  

**15.** 掌握多线程编程中线程的状态转换与相关方法的对应关系。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

**线程5种状态转换图：**

  

```

            start()

  新建 ──────────→ 就绪 ←──────────────┐

                    │                    │

                    │ CPU调度            │

                    ↓                    │

  死亡 ←── 运行完毕  运行                 │

   ↑               │   │                │

   │   sleep()     │   │ wait()         │

   │   时间到      │   ↓                │

   │            阻塞 等待 ← notify()     │

   │   join()    (timed)  等待池        │

   │   interrupt  │   │                │

   └──────────────┘   └── notifyAll() ──┘

```

  

| 方法 | 作用 | 状态转换 |

|------|------|----------|

| `start()` | 启动线程 | 新建 → 就绪 |

| `sleep(long ms)` | 休眠指定时间 | 运行 → 阻塞（时间到自动回就绪） |

| `wait()` | 释放锁并等待 | 运行 → 等待池 |

| `notify()/notifyAll()` | 唤醒等待线程 | 等待池 → 就绪 |

| `join()` | 等待该线程执行完 | 当前线程 → 阻塞 |

| `interrupt()` | 中断线程 | 设置中断标志 |

  

</details>

  

---

  

**16.** 声明一个类的子类时的关键字是？声明需要实现某个接口的类时的关键字是？在方法内引用与局部变量同名的成员变量的关键字是？

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

| 场景 | 关键字 | 示例 |

|------|--------|------|

| 声明子类 | **`extends`** | `class Dog extends Animal` |

| 实现接口 | **`implements`** | `class Dog implements Pet` |

| 引用被隐藏的成员变量 | **`this`** | `this.name = name;` |

| 引用被隐藏的父类成员变量 | **`super`** | `super.name` |

  

```java

class Dog extends Animal implements Pet {  // extends + implements

    private String name;

    public void setName(String name) {

        this.name = name;  // this 区分成员变量和局部变量

    }

}

```

  

</details>

  

---

  

**17.** final 关键字可用于哪些地方？各有什么作用？

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

| 用法 | 作用 | 示例 |

|------|------|------|

| **final 修饰变量** | 变量变成常量，不可修改 | `final int MAX = 100;` |

| **final 修饰方法** | 方法不能被重写 | `public final void show()` |

| **final 修饰类** | 类不能被继承 | `final class String` |

| **final 修饰参数** | 参数在方法内不可修改 | `void f(final int x)` |

  

```java

final class Math {               // 不可被继承

    public static final double PI = 3.14159;  // 常量

    public final int abs(int x) { return x > 0 ? x : -x; }  // 不可重写

}

```

  

> ⚠️ `final` 和 `abstract` 互斥：final 阻止重写/继承，abstract 强制重写/继承。

  

</details>

  

---

  

**18.** synchronized 关键字在多线程编程中有什么作用？有什么副作用？

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

**作用：**

- 保证**线程安全**，同一时刻只有一个线程能执行被 synchronized 修饰的代码

- 保证了**原子性**和**可见性**（进入 synchronized 块前会从主存刷新变量）

  

**使用方式：**

```java

// 1. 同步方法

public synchronized void sell() {

    tickets--;

}

  

// 2. 同步代码块

synchronized (obj) {

    tickets--;

}

```

  

**副作用：**

- ① **性能下降**：线程竞争锁时需要等待，降低并发效率

- ② **死锁风险**：多个线程互相等待对方释放锁

- ③ 锁粒度太大可能导致线程长时间阻塞

  

</details>

  

---

  

**19.** 满足什么条件子类的方法都会覆盖父类的方法？

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

子类方法覆盖（重写）父类方法需满足的条件：

  

1. **方法名完全相同**

2. **参数列表完全相同**（类型、个数、顺序）

3. **返回值类型相同**或是父类返回值的子类型（协变返回）

4. **访问权限不能更低**（public > protected > default > private）

5. 不能抛出比父类**更宽泛**的检查异常

6. 父类方法不能是 **`static`**（静态方法只能被隐藏，不能被重写）

7. 父类方法不能是 **`final`**（final 方法禁止重写）

8. 父类方法不能是 **`private`**（私有方法不可见，子类无法重写）

  

```java

class Animal {

    protected Animal cry() throws IOException { ... }

}

class Dog extends Animal {

    @Override

    public Dog cry() throws FileNotFoundException { ... }  // 正确重写

}

```

  

</details>

  

---

  

**20.** 写出子类 Child 继承父类 Father 并实现接口 Fun1 和 Fan2 的声明语句。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

```java

public class Child extends Father implements Fun1, Fan2 {

    // 类体

}

```

  

**语法规则：**

- `extends` 必须写在 `implements` **前面**

- 只能继承**一个**父类（单继承）

- 可以实现**多个**接口（逗号分隔）

  

</details>

  

---

  

**21.** Java 多线程编程的两种基本方法是？

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

**方法一：继承 Thread 类**

```java

class MyThread extends Thread {

    public void run() {

        System.out.println("线程运行中");

    }

}

MyThread t = new MyThread();

t.start();  // 启动线程

```

  

**方法二：实现 Runnable 接口（推荐）**

```java

class MyRunnable implements Runnable {

    public void run() {

        System.out.println("线程运行中");

    }

}

Thread t = new Thread(new MyRunnable());

t.start();

```

  

| 对比 | 继承 Thread | 实现 Runnable |

|------|-------------|---------------|

| 扩展性 | 不能再继承其他类 | 可同时继承其他类 |

| 资源共享 | 每个线程独立 | 多个线程可共享同一个 Runnable |

| 推荐度 | 一般 | **推荐**（面向接口编程） |

  

</details>

  

---

  

## 二、单选题相关（每题1分，共10分）

  

---

  

**22.** 从以下几个抽象类和接口的表述中找出错误的。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

**常见错误说法：**

- ❌ "抽象类可以实例化" — 抽象类不能 new

- ❌ "接口可以有构造方法" — 接口没有构造方法

- ❌ "接口中的方法都是抽象的" — Java 8+ 可以有 default 和 static 方法

- ❌ "抽象类不能有构造方法" — 抽象类有构造方法（供子类调用）

- ❌ "接口可以继承类" — 接口只能继承接口

  

**正确说法：**

- ✅ 抽象类可以有构造方法

- ✅ 接口中的变量隐式为 `public static final`

- ✅ 接口中的方法隐式为 `public abstract`

- ✅ 抽象类中可以有非抽象方法

  

</details>

  

---

  

**23.** 求一个整数"除法+求余"混合表达式的结果。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

```java

// 整数除法：取整，舍去小数

10 / 3 = 3

10 / 3.0 = 3.3333...  (double)

  

// 取余/取模：%

10 % 3 = 1     (int)

10 % 3.0 = 1.0 (double)

  

// 混合运算：从左到右，*/% 优先级高于 +-

10 / 3 * 3 = 3 * 3 = 9

10 % 3 + 1 = 1 + 1 = 2

```

  

**运算符优先级：** `* / %` > `+ -` > 赋值

  

</details>

  

---

  

**24.** 从以下几个关于匿名类的表述中找正确的。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

**匿名内部类特点：**

```java

// 语法：new 父类/接口() { 类体 }

Runnable r = new Runnable() {

    public void run() {

        System.out.println("匿名类");

    }

};

```

  

**正确说法：**

- ✅ 匿名类不能有显式的构造方法（因为没有类名）

- ✅ 匿名类可以访问外部类的成员变量

- ✅ 匿名类可以访问 final 或 effectively final 的局部变量

- ✅ 匿名类必须实现接口的所有抽象方法或重写父类方法

  

**错误说法：**

- ❌ 匿名类可以有构造方法

- ❌ 匿名类可以继承一个类并同时实现接口（只能继承一个或实现一个接口）

  

</details>

  

---

  

**25.** 考查 File 类的构造方法和 isDirectory()、isFile() 等方法的使用。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

```java

File f1 = new File("D:/test/hello.txt");

File f2 = new File("D:/test", "hello.txt");

  

// 常用方法

f1.exists()         // boolean - 是否存在

f1.isFile()         // boolean - 是否是文件

f1.isDirectory()    // boolean - 是否是目录

f1.length()         // long - 文件长度（字节）

f1.getName()        // String - 文件名

f1.getPath()        // String - 路径

f1.delete()         // boolean - 删除（非空目录删不掉）

f1.createNewFile()  // boolean - 创建新文件

```

  

> ⚠️ `isFile()` 返回 `boolean`，不是 `int`；`length()` 返回 `long`，不是 `int`；`new File()` 不存在的路径不会报错。

  

</details>

  

---

  

**26.** 考查多线程编程中方法 start、isAlive、currentThread、interrupt、sleep、wait 方法的使用。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

| 方法 | 说明 | 所属 |

|------|------|------|

| `start()` | 启动线程，JVM 调用 run() | Thread |

| `isAlive()` | 线程是否存活（已启动未死亡） | Thread |

| `currentThread()` | 获取当前执行线程的引用 | Thread（静态） |

| `interrupt()` | 中断线程（设置中断标志） | Thread |

| `sleep(long ms)` | 当前线程休眠（不释放锁） | Thread（静态） |

| `wait()` | 当前线程等待（释放锁） | Object |

| `notify()/notifyAll()` | 唤醒等待线程 | Object |

  

> ⚠️ `run()` vs `start()`：`run()` 是普通方法调用（同步），`start()` 才启动新线程（异步）。

  

</details>

  

---

  

**27.** 从以下几个关于构造方法的表述中找出错误的那个。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

**常见错误说法：**

- ❌ "构造方法可以被继承" — 构造方法**不能被继承**

- ❌ "构造方法有返回值" — 构造方法连 void 都不写

- ❌ "子类可以不调用父类构造方法" — 子类构造方法必然先调用父类构造方法

  

**正确说法：**

- ✅ 构造方法名与类名相同

- ✅ 若无构造方法，编译器自动添加无参构造方法

- ✅ 构造方法可以被重载

- ✅ `super()` 必须是子类构造方法第一条语句

  

</details>

  

---

  

**28.** 从以下几个关于 final 和 abstract 类的表述中找出正确的那个。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

**final 和 abstract 的互斥关系：**

  

| | final | abstract |

|------|-------|----------|

| 修饰类 | 不能被继承 | 必须被继承（不能实例化） |

| 修饰方法 | 不能被重写 | 必须被重写 |

| 可否同时使用 | ❌ 不可 | ❌ 不可（语义互斥） |

  

**正确说法：**

- ✅ `final` 和 `abstract` 不能同时修饰同一个方法/类

- ✅ abstract 类中可以有非 abstract 方法

- ✅ abstract 类中可以有 final 方法（非 abstract 方法可以被 final 修饰）

- ✅ final 类中所有方法隐式是 final 的

  

</details>

  

---

  

**29.** 从以下几个关于接口中的数据成员的表述中找出正确的那个。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

**接口中数据成员的特点：**

- 所有变量隐式修饰为 **`public static final`**（即常量）

- **必须初始化**（因为 final）

- 可通过 `接口名.常量名` 直接访问

  

```java

interface Com {

    int MAX = 100;  // 等价于 public static final int MAX = 100;

    // int MIN;     // ❌ 错误！必须初始化

}

```

  

**常见错误：**

- ❌ 接口中的变量可以不初始化 → 必须初始化

- ❌ 接口中的变量是实例变量 → 是 static 的

- ❌ 接口中的变量可以用 private 修饰 → 只能是 public

  

</details>

  

---

  

**30.** 从以下几个关于类声明语法的表述中找出错误的那个。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

**类声明语法：**

```java

[访问修饰符] class 类名 [extends 父类] [implements 接口1, 接口2] {

    // 类体

}

```

  

**常见错误：**

- ❌ `class A extends B, C` — 不能多继承类

- ❌ `class A implements B extends C` — 顺序错误，extends 在前

- ❌ 类名可以和文件名不同（public 类除外）

  

**正确示例：**

```java

public class Child extends Father implements Fun1, Fun2 { }

```

  

</details>

  

---

  

**31.** 从以下几个关于接口中的数据成员的表述中找出正确的那个。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

同 Q29，核心要点：

- 接口中只能定义**常量**（public static final），不能有普通变量

- 常量**必须初始化**

- 隐式修饰符：`public static final`

  

</details>

  

---

  

**32.** 从以下几个关于 String 类的表述中找出正确的那个。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

**String 类特点：**

- String 是**不可变类（immutable）**：一旦创建，内容不能修改

- String 被 `final` 修饰，**不能被继承**

- 字符串拼接实际创建了新的 String 对象

- 频繁字符串操作应使用 `StringBuilder` 或 `StringBuffer`

  

**常见考点：**

```java

String s1 = "hello";

String s2 = "hello";

s1 == s2;      // true（字符串常量池）

s1.equals(s2); // true（值相等）

  

String s3 = new String("hello");

s1 == s3;      // false（new 在堆中创建新对象）

```

  

> ⚠️ `==` 比较引用地址，`equals()` 比较内容。

  

</details>

  

---

  

**33.** 从以下几个关于非抽象子类实现某个接口的表述中找出正确的那个。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

**规则：**

- 非抽象类实现接口，**必须重写接口中的所有抽象方法**

- 重写时访问权限必须是 **`public`**（接口方法隐式 public）

- 如果未全部重写，该类必须声明为 **`abstract`**

  

```java

interface Com {

    void f();      // 隐式 public abstract

    int MAX = 100; // 隐式 public static final

}

  

class A implements Com {

    public void f() { ... }  // 必须 public

}

```

  

</details>

  

---

  

**34.** 求几个混合运算表达式的最终结果类型，考查运算符优先级、类型自动转换与强制转换。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

**类型转换规则：**

- **自动提升**：byte→short→int→long→float→double

- 二元运算中，两个操作数向**更高的类型**提升

- **强制转换**：`(目标类型) 表达式`，可能丢失精度

  

**示例：**

```java

double d = 5 / 2;         // 5/2 = 2 (int), d = 2.0

double d = 5.0 / 2;       // 5.0/2.0 = 2.5 (double)

short s = 1; s = s + 1;   // ❌ s+1 是 int，不能赋给 short

short s = 1; s += 1;      // ✅ += 内置强制转换

```

  

</details>

  

---

  

**35.** 已知父-子-孙继承关系的三个类，求各类对象的所属类型，考查 instanceof 运算符的运用。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

```java

class A {}

class B extends A {}

class C extends B {}

  

C c = new C();

  

c instanceof C    // true  (C是C)

c instanceof B    // true  (C是B的子类)

c instanceof A    // true  (C是A的子类)

c instanceof Object // true (所有类都是Object的子类)

  

A a = new B();

a instanceof B    // true  (实际对象是B)

a instanceof C    // false (B不是C)

```

  

> **核心：** `obj instanceof Class` 判断 obj 的**实际运行时类型**是否是 Class 或其子类的实例。

  

</details>

  

---

  

**36.** 从以下几个关于 File、FileOutputStream、BufferedWriter 使用的表述中找出错误的那个。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

**常见错误表述：**

- ❌ `BufferedWriter` 可以直接包装 File → 需要包装的是 **Writer**

- ❌ `FileOutputStream` 按字符写出数据 → 按**字节**

- ❌ `new File("不存在的路径")` 会抛异常 → 不会抛异常

  

**正确用法：**

```java

// 正确的流的嵌套

BufferedWriter bw = new BufferedWriter(new FileWriter("a.txt"));

  

// FileOutputStream 是字节流，FileWriter 是字符流

FileOutputStream fos = new FileOutputStream("a.txt", true); // 追加模式

```

  

</details>

  

---

  

**37.** 从以下几个关于 Runnable 接口和 Thread 类包含的方法表述中找出正确的那个。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

| | Runnable 接口 | Thread 类 |

|------|--------------|-----------|

| 核心方法 | `void run()` | `void run()`, `start()`, `sleep()`, `join()`, `interrupt()` 等 |

| 方法数量 | **只有一个** run() | 多个 |

  

- `start()` 属于 **Thread 类**，不属于 Runnable 接口

- `sleep()` 是 Thread 的**静态方法**

- `run()` 两者都有

  

</details>

  

---

  

**38.** 从以下几个关于 List、Set、Map、Collection 继承关系的表述中找出正确的那个。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

**Java 集合框架继承关系：**

  

```

Collection (接口)

├── List (接口) — 有序、可重复

│   ├── ArrayList

│   ├── LinkedList

│   └── Vector

├── Set (接口) — 无序、不可重复

│   ├── HashSet

│   └── TreeSet

└── Queue (接口)

  

Map (接口) — 键值对，不继承 Collection

├── HashMap

├── TreeMap

└── Hashtable

```

  

> ⚠️ **Map 不继承 Collection 接口**，是一个独立的接口体系。

  

</details>

  

---

  

**39.** 考查 Java 语言实现多重继承效果的方式。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

Java 不支持类的多继承，但可通过**接口多实现**达到类似效果：

  

```java

interface Flyable { void fly(); }

interface Swimmable { void swim(); }

  

// 一个类实现多个接口

class Duck implements Flyable, Swimmable {

    public void fly() { ... }

    public void swim() { ... }

}

  

// 接口支持多继承

interface Amphibious extends Flyable, Swimmable { }

```

  

> Java 类单继承避免"菱形继承问题"，接口多继承无此问题（接口无状态）。

  

</details>

  

---

  

**40.** 考查 final 关键字的几种用法。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

见 Q17。final 修饰变量（常量）、方法（不可重写）、类（不可继承）。

  

</details>

  

---

  

**41.** 考查 Java 的包结构（package）与文件夹层次（目录结构）的关系。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

**对应关系：**

```

package com.example.test;

      ↓

文件夹: com/example/test/

      ↓

      com

       └── example

            └── test

                 └── Test.class

```

  

- 包名中的 `.` 对应文件系统的 `/`（或 `\`）

- 包名习惯全部**小写**

- 带包编译：`javac -d . Test.java`（自动生成对应目录结构）

- 带包运行：`java com.example.test.Test`

  

</details>

  

---

  

**42.** 根据 IO 流类的命名规范确定它们的类型（字符流、字节流、输入流、输出流）。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

| 命名模式 | 类型 | 示例 |

|----------|------|------|

| 以 `InputStream` 结尾 | 字节输入流 | FileInputStream, ObjectInputStream |

| 以 `OutputStream` 结尾 | 字节输出流 | FileOutputStream, ObjectOutputStream |

| 以 `Reader` 结尾 | 字符输入流 | FileReader, BufferedReader |

| 以 `Writer` 结尾 | 字符输出流 | FileWriter, BufferedWriter |

| 带 `Buffered` 前缀 | 缓冲流（处理流） | BufferedReader, BufferedInputStream |

| 带 `Object` 前缀 | 对象流 | ObjectInputStream, ObjectOutputStream |

  

</details>

  

---

  

**43.** 从以下几个关于匿名内部类的表述中找出错误的那个。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

见 Q24。匿名内部类没有类名，不能有显式构造方法，必须实现接口/重写父类方法。

  

</details>

  

---

  

**44.** 从以下几个关于局部变量、成员变量和形参的表述中找出错误的那个。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

| 变量类型 | 声明位置 | 默认值 | 生命周期 |

|----------|----------|--------|----------|

| **成员变量** | 类体中 | **有默认值**（0/false/null） | 与对象同在 |

| **局部变量** | 方法体内 | **无默认值**（必须初始化） | 方法执行期间 |

| **形参** | 方法参数列表 | 调用时赋值 | 方法执行期间 |

  

**常见错误：**

- ❌ 局部变量有默认值 → 局部变量**没有**默认值，必须初始化才能使用

  

</details>

  

---

  

**45.** 从以下几个关于抽象类、非抽象类和接口的表述中找出正确的那个。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

| | 抽象类 | 非抽象类 | 接口 |

|------|--------|----------|------|

| 实例化 | ❌ | ✅ | ❌ |

| 抽象方法 | 可以有 | ❌ 不能有 | 可以有 |

| 具体方法 | 可以有 | ✅ | Java 8+ 可有 default/static |

| 构造方法 | ✅ | ✅ | ❌ |

| 继承/实现 | 单继承 | 单继承 | 多继承接口 |

  

</details>

  

---

  

**46.** 从以下几个关于多线程 start、run、优先级、同步的表述中找出错误的那个。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

**常见错误说法：**

- ❌ "调用 run() 启动线程" → run() 是普通方法调用，`start()` 才启动线程

- ❌ "线程优先级越高一定越先执行" → 优先级只是建议，实际由 OS 调度

- ❌ "synchronized 修饰的方法不能被多个线程同时访问" → 同一个对象的同步方法不能同时访问，不同对象可以

  

**正确说法：**

- ✅ `start()` 启动新线程，JVM 自动调用 `run()`

- ✅ 优先级范围：1（MIN_PRIORITY）~ 10（MAX_PRIORITY），默认 5

  

</details>

  

---

  

**47.** 从以下几个关于 Socket、ServerSocket、accept()、UDP 的表述中找出错误的那个。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

**TCP 相关：**

- `ServerSocket`：服务端，绑定端口监听

- `accept()`：阻塞等待客户端连接，返回 `Socket` 对象

- `Socket`：表示一个连接端点

  

**UDP 相关：**

- `DatagramSocket`：UDP 通信

- `DatagramPacket`：数据包

  

**常见错误：**

- ❌ `accept()` 返回 `ServerSocket` → 返回的是 `Socket`

- ❌ UDP 是面向连接的 → UDP 是**无连接**的

  

</details>

  

---

  

**48.** 从以下几个关于 private 成员变量的表述中找出正确的那个。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

**private 的特点：**

- 只能在**本类内部**访问

- 子类**不能直接访问**父类的 private 成员

- 外部类通过 public 的 getter/setter 间接访问

  

```java

class Person {

    private String name;  // 只有本类能直接访问

    public String getName() { return name; }  // 对外提供访问方法

}

```

  

> **正确说法：** private 成员变量体现了"封装"特性，保护数据不被外部随意修改。

  

</details>

  

---

  

**49.** 从以下几个关于线程等待（wait）与唤醒（notify / notifyAll）的表述中找出正确的那个。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

| 方法 | 说明 |

|------|------|

| `wait()` | 释放锁，当前线程进入等待池 |

| `notify()` | 随机唤醒等待池中的一个线程 |

| `notifyAll()` | 唤醒等待池中的所有线程 |

  

**重要规则：**

- `wait()`、`notify()`、`notifyAll()` 属于 **Object 类**

- 必须在 **synchronized** 代码块/方法中调用（需要持有锁）

- `wait()` 会**释放锁**，`sleep()` **不释放锁**

  

> ⚠️ `wait()` vs `sleep()`：wait 释放锁（Object 方法），sleep 不释放锁（Thread 方法）。

  

</details>

  

---

  

**50.** 从以下几个关于构造函数的表述中找出错误的那个。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

见 Q2 和 Q27。常见错误说法：

- ❌ 构造方法可以被继承

- ❌ 构造方法有返回值类型

- ❌ 子类构造方法第一行不一定是 super()

  

</details>

  

---

  

**51.** 从以下几个关于 ArrayList 对象实例的语句中找出正确的那个（父类对象可以引用子类的实例，反之则不然）。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

```java

// ✅ 正确：父类引用指向子类对象（多态/向上转型）

List<String> list = new ArrayList<String>();

Collection<String> col = new ArrayList<String>();

Object obj = new ArrayList<String>();

  

// ❌ 错误：子类引用不能直接指向父类对象

ArrayList<String> list = new List<String>();  // List 是接口不能 new

  

// ❌ 错误：不能向下转型不兼容的类型

ArrayList<Integer> list = new ArrayList<String>(); // 泛型不兼容

```

  

> **核心：** 父类（接口）引用可以指向子类实例；子类引用不能指向父类实例。

  

</details>

  

---

  

## 三、简答题相关（3小题，每题5分，共15分）

  

---

  

**52.** 简述抽象类和接口的主要区别。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

| | 抽象类 | 接口 |

|------|--------|------|

| 关键字 | `abstract class` | `interface` |

| 实例化 | ❌ 不能 | ❌ 不能 |

| 构造方法 | ✅ 有 | ❌ 无 |

| 方法 | 可有抽象方法和具体方法 | Java 8+：抽象/default/static 方法 |

| 变量 | 任意类型 | 仅常量（public static final） |

| 继承 | 单继承 | 可多继承接口 |

| 使用场景 | "is-a" 关系，共享代码 | "can-do" 能力，定义规范 |

  

**设计理念：** 抽象类用于代码复用（模板模式），接口用于定义规范（解耦）。

  

</details>

  

---

  

**53.** 简述 TCP 单向通信编程中服务端的编程步骤。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

1. 创建 `ServerSocket`，绑定端口号

2. 调用 `accept()` 监听客户端连接（阻塞），获取 `Socket` 对象

3. 通过 Socket 获取输入流，读取客户端数据

4. 处理数据（业务逻辑）

5. 通过 Socket 获取输出流，向客户端回复

6. 关闭流和 Socket，释放资源

  

</details>

  

---

  

**54.** 简述创建线程的两种基本方式及其优缺点。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

**方式一：继承 Thread 类**

- 优点：代码简单，直接调用 Thread 的方法

- 缺点：不能再继承其他类，线程与任务耦合

  

**方式二：实现 Runnable 接口（推荐）**

- 优点：可同时继承其他类，任务与线程分离，多个线程可共享同一 Runnable

- 缺点：代码稍多一层包装

  

</details>

  

---

  

**55.** 在类的构造方法如何调用本类的无参及有参构造方法？如何调用其父类的无参及有参构造方法？

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

```java

class Son extends Father {

    Son() {

        super();         // 调用父类无参构造（默认，可省略）

    }

    Son(int x) {

        super(x);        // 调用父类有参构造

    }

    Son(int x, int y) {

        this(x);         // 调用本类有参构造

        // 其他初始化

    }

}

```

  

**规则：**

- `this(...)`：调用本类其他构造方法

- `super(...)`：调用父类构造方法

- `this()` 和 `super()` **不能同时出现**，且必须是**第一条语句**

- 如果都没写，编译器默认添加 `super()`

  

</details>

  

---

  

**56.** 简述 Java 多态的基础、实现方法及相关约定。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

**基础：** 继承（或接口实现）+ 方法重写

  

**实现方法：** 父类引用指向子类实例 → 调用重写方法时，执行子类的版本

  

**相关约定（重写规则，见 Q19）：**

- 方法名、参数列表相同

- 返回类型相同或协变

- 访问权限不能降低

- 异常不能变宽

  

**三种多态形式：**

1. 父类引用指向子类对象

2. 接口引用指向实现类对象

3. 方法参数使用父类/接口类型（最常用）

  

</details>

  

---

  

**57.** 举例 ArrayList\<String> list 的 3 种遍历方式。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

```java

ArrayList<String> list = new ArrayList<>();

list.add("a"); list.add("b"); list.add("c");

  

// 方式1：普通 for 循环

for (int i = 0; i < list.size(); i++) {

    System.out.println(list.get(i));

}

  

// 方式2：增强 for 循环

for (String s : list) {

    System.out.println(s);

}

  

// 方式3：迭代器 Iterator

Iterator<String> it = list.iterator();

while (it.hasNext()) {

    System.out.println(it.next());

}

```

  

</details>

  

---

  

**58.** 简述 this 和 super 关键字的作用。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

| 关键字 | 作用 |

|--------|------|

| **`this`** | ① 引用当前对象 ② 区分成员变量和局部变量 ③ 调用本类构造方法 `this()` |

| **`super`** | ① 引用父类对象 ② 访问被隐藏的父类成员 ③ 调用父类构造方法 `super()` |

  

```java

class Son extends Father {

    private String name;

    Son(String name) {

        super();          // 调用父类构造

        this.name = name; // 区分成员变量和局部变量

    }

}

```

  

</details>

  

---

  

**59.** 简述 Java 面向对象的三大特性及其作用。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

| 特性 | 作用 | Java 实现 |

|------|------|-----------|

| **封装** | 隐藏内部实现，保护数据安全 | private + getter/setter |

| **继承** | 代码复用，建立类之间的层级关系 | extends 单继承 |

| **多态** | 统一接口，不同实现，提高可扩展性 | 父类引用指向子类对象 + 方法重写 |

  

</details>

  

---

  

**60.** 列举至少 3 对 InputStream 和 OutputStream 流的子类并说明其特点。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

| 输入流 | 输出流 | 特点 |

|--------|--------|------|

| `FileInputStream` | `FileOutputStream` | 文件字节流，读写文件 |

| `BufferedInputStream` | `BufferedOutputStream` | 带缓冲，提高效率 |

| `ObjectInputStream` | `ObjectOutputStream` | 对象序列化，读写 Java 对象 |

| `DataInputStream` | `DataOutputStream` | 读写 Java 基本数据类型 |

| `ByteArrayInputStream` | `ByteArrayOutputStream` | 以字节数组为数据源/目标 |

  

</details>

  

---

  

## 四、程序分析题（4小题，每题5分，共20分）

  

---

  

**61.** 父类对象引用子类实例时的多态性。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

```java

class Animal {

    void cry() { System.out.println("动物叫"); }

}

class Dog extends Animal {

    void cry() { System.out.println("汪汪"); }

}

  

Animal a = new Dog();  // 父类引用指向子类对象

a.cry();               // 输出: "汪汪"（运行时多态）

  

// a 只能调用 Animal 中定义的方法

// a.wagTail();        // ❌ 编译错误：Animal 没有 wagTail()

```

  

**核心原则：**

- **编译看左边**（父类）：只能调用父类中定义的方法

- **运行看右边**（子类）：执行的是子类重写后的方法

  

</details>

  

---

  

**62.** 考核 FileInputStream 和 FileOutputStream 的读写操作。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

```java

// 写入

FileOutputStream fos = new FileOutputStream("test.txt");

fos.write("Hello".getBytes());

fos.close();

  

// 读取（逐字节）

FileInputStream fis = new FileInputStream("test.txt");

int b;

while ((b = fis.read()) != -1) {

    System.out.print((char) b);

}

fis.close();

  

// 读取（字节数组）

byte[] buf = new byte[1024];

int len;

while ((len = fis.read(buf)) != -1) {

    System.out.print(new String(buf, 0, len));

}

```

  

> `read()` 返回 -1 表示文件末尾；`read(byte[])` 返回实际读取的字节数。

  

</details>

  

---

  

**63.** 考核 TreeMap\<key,value>、Collection\<value>、Iterator\<value> 集合类的应用。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

```java

TreeMap<Integer, String> map = new TreeMap<>();

map.put(3, "c");

map.put(1, "a");

map.put(2, "b");

  

// TreeMap 按键自动排序：{1="a", 2="b", 3="c"}

  

// 获取所有值

Collection<String> values = map.values();

  

// 迭代

Iterator<String> it = values.iterator();

while (it.hasNext()) {

    System.out.println(it.next());  // a, b, c（按键顺序）

}

```

  

> TreeMap 按键自然排序；`values()` 返回的集合顺序与 key 一致。

  

</details>

  

---

  

**64.** 考核静态成员变量和静态方法的运用以及内存分析。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

```java

class Student {

    int id;           // 实例变量（堆中，每个对象一份）

    static int count; // 静态变量（方法区，所有对象共享）

    Student() {

        count++;      // 每次创建对象 count+1

    }

    static void showCount() {  // 静态方法

        // System.out.println(id); ❌ 静态方法不能访问实例变量

        System.out.println(count);

    }

}

```

  

**内存模型：**

- 静态变量在**方法区**（元空间），类加载时分配，类卸载时回收

- 实例变量在**堆**中，随对象创建而分配

  

</details>

  

---

  

**65.** 考核接口和实现接口的类的多态关系。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

```java

interface USB {

    void connect();

}

  

class Mouse implements USB {

    public void connect() { System.out.println("鼠标已连接"); }

}

  

class Keyboard implements USB {

    public void connect() { System.out.println("键盘已连接"); }

}

  

// 多态使用

USB device1 = new Mouse();

USB device2 = new Keyboard();

  

device1.connect();  // "鼠标已连接"

device2.connect();  // "键盘已连接"

```

  

> 接口引用变量可以调用所有实现类对象的多态方法。

  

</details>

  

---

  

## 四（续）、程序分析题

  

---

  

**66.** 考核 try ... catch ...finally ... 结构多异常捕获的运用。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

```java

try {

    int[] arr = new int[3];

    arr[5] = 10;  // ArrayIndexOutOfBoundsException

} catch (ArrayIndexOutOfBoundsException e) {

    System.out.println("数组越界: " + e.getMessage());

} catch (Exception e) {

    System.out.println("其他异常: " + e.getMessage());

} finally {

    System.out.println("finally 始终执行");

}

// 输出:

// 数组越界: ...

// finally 始终执行

```

  

**规则：**

- catch 自上而下匹配，**子类在前，父类在后**

- finally **始终执行**（即使有 return，除非 System.exit()）

  

</details>

  

---

  

**67.** 画图分析 Java 程序（创建一个类的两个实例）运行时的内存模型。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

```java

public class Test {

    int x, y;

    Test(int x, int y) { this.x = x; this.y = y; }

    public static void main(String[] args) {

        Test pt1 = new Test(3, 3);

        Test pt2 = new Test(4, 4);

    }

}

```

  

**内存模型：**

```

栈(Stack)                  堆(Heap)

┌───────────┐            ┌──────────────┐

│ pt1 ──────┼───────────→│ Test{x=3,y=3}│

│ pt2 ──────┼──┐         └──────────────┘

└───────────┘  │         ┌──────────────┐

               └────────→│ Test{x=4,y=4}│

                         └──────────────┘

```

  

- pt1/pt2 在栈中，存引用地址

- 两个 Test 对象在堆中，彼此独立

- 成员变量 x、y 在堆中（对象内部）

  

</details>

  

---

  

**68.** 考核构造方法、构造代码块和静态代码块的运用。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

```java

class Test {

    Test() { System.out.println("构造方法"); }

    { System.out.println("构造代码块"); }

    static { System.out.println("静态代码块"); }

}

// new Test() 输出：

// 静态代码块      (类加载时执行，仅一次)

// 构造代码块      (每次 new 在构造方法之前执行)

// 构造方法        (最后执行)

```

  

**执行顺序：** 静态代码块（类加载，一次）→ 构造代码块（每次 new）→ 构造方法（每次 new）

  

**子类执行顺序：** 父静态→子静态→父构造代码块→父构造→子构造代码块→子构造

  

</details>

  

---

  

**69.** 考核抽象类与其实现子类之间的多态性。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

```java

abstract class Shape {

    abstract double area();

}

  

class Circle extends Shape {

    double r;

    Circle(double r) { this.r = r; }

    double area() { return Math.PI * r * r; }

}

  

Shape s = new Circle(5);  // 抽象类引用指向子类

System.out.println(s.area());  // 调用 Circle 的 area()

```

  

> 抽象类不能实例化，但可以作为引用类型使用（多态）。

  

</details>

  

---

  

**70.** 考核 try ... catch ...finally ... 结构及 throw 的使用。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

```java

public static void checkAge(int age) throws Exception {

    if (age < 0) {

        throw new Exception("年龄不能为负数");  // 抛出异常

    }

}

  

// 调用处

try {

    checkAge(-1);

} catch (Exception e) {

    System.out.println(e.getMessage());  // "年龄不能为负数"

} finally {

    System.out.println("检查结束");

}

```

  

- `throw`：手动抛出异常对象（在方法内）

- `throws`：声明方法可能抛出的异常（在方法签名）

  

</details>

  

---

  

## 五、编程题（4小题，共45分）

  

---

  

**71.** ①编写一个含2个属性的类，并为其设计有参构造方法，再设计一个用于显示属性值的方法。②编写该类的一个子类，除继承父类的2个属性外再增加一个属性，并创建有参构造方法对3个属性初始化，重写显示属性的方法用于输出3个属性的值。③编写一个测试类，分别创建父类和子类的对象实例并显示各自的属性值。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

```java

// ① 父类

class Person {

    protected String name;

    protected int age;

    public Person(String name, int age) {

        this.name = name;

        this.age = age;

    }

    public void show() {

        System.out.println("姓名: " + name + ", 年龄: " + age);

    }

}

  

// ② 子类

class Student extends Person {

    private String school;

    public Student(String name, int age, String school) {

        super(name, age);

        this.school = school;

    }

    @Override

    public void show() {

        System.out.println("姓名: " + name + ", 年龄: " + age + ", 学校: " + school);

    }

}

  

// ③ 测试类

public class Test {

    public static void main(String[] args) {

        Person p = new Person("张三", 30);

        p.show();  // 姓名: 张三, 年龄: 30

        Student s = new Student("李四", 20, "清华大学");

        s.show();  // 姓名: 李四, 年龄: 20, 学校: 清华大学

    }

}

```

  

</details>

  

---

  

**72.** ①设计几何接口用于计算二维几何图形的面积。②设计圆类实现几何接口，计算圆的面积。③设计矩形类也实现几何接口，计算矩形的面积。④设计柱体类，以几何接口和高为属性并设计有参构造方法，然后设计计算体积的方法。⑤设计测试类，以几何接口分别引用矩形实例和圆实例，然后调用多态方法计算面积和体积。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

```java

// ① 几何接口

interface Geometry {

    double getArea();

}

  

// ② 圆类

class Circle implements Geometry {

    private double radius;

    public Circle(double r) { this.radius = r; }

    public double getArea() { return Math.PI * radius * radius; }

}

  

// ③ 矩形类

class Rectangle implements Geometry {

    private double width, height;

    public Rectangle(double w, double h) { width = w; height = h; }

    public double getArea() { return width * height; }

}

  

// ④ 柱体类

class Cylinder {

    private Geometry bottom;

    private double height;

    public Cylinder(Geometry bottom, double height) {

        this.bottom = bottom; this.height = height;

    }

    public double getVolume() {

        return bottom.getArea() * height;

    }

}

  

// ⑤ 测试类

public class Test {

    public static void main(String[] args) {

        Geometry circle = new Circle(3);

        Geometry rect = new Rectangle(4, 5);

        Cylinder c1 = new Cylinder(circle, 10);

        Cylinder c2 = new Cylinder(rect, 10);

        System.out.println("圆柱体积: " + c1.getVolume());

        System.out.println("方柱体积: " + c2.getVolume());

    }

}

```

  

</details>

  

---

  

**73.** 设计一个多线程程序，模拟在3个窗口争抢卖5张票的操作。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

```java

class TicketSeller implements Runnable {

    private int tickets = 5;

    public synchronized void run() {

        while (tickets > 0) {

            System.out.println(Thread.currentThread().getName()

                + " 卖出一张票，剩余: " + (--tickets));

            try { Thread.sleep(100); } catch (InterruptedException e) {}

        }

    }

}

  

public class Test {

    public static void main(String[] args) {

        TicketSeller seller = new TicketSeller();

        new Thread(seller, "窗口1").start();

        new Thread(seller, "窗口2").start();

        new Thread(seller, "窗口3").start();

    }

}

```

  

> 注意同步（synchronized）确保票数不会出现负数。

  

</details>

  

---

  

**74.** ①设计一个数组排序类，编写静态排序方法（双层嵌套循环）。②设计测试类，调用排序方法。③若要改为可对任意类型排序需修改哪两处？自定义类如何设计？

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

```java

// ① 排序类

class ArraySorter {

    public static void sort(int[] arr) {

        for (int i = 0; i < arr.length - 1; i++) {

            for (int j = 0; j < arr.length - 1 - i; j++) {

                if (arr[j] > arr[j + 1]) {

                    int temp = arr[j];

                    arr[j] = arr[j + 1];

                    arr[j + 1] = temp;

                }

            }

        }

    }

}

  

// ② 测试类

public class Test {

    public static void main(String[] args) {

        int[] arr = {5, 2, 8, 1, 9};

        ArraySorter.sort(arr);

        for (int n : arr) System.out.print(n + " ");

    }

}

  

// ③ 泛型改造：数组类型改为 T[] + Comparable<T>

// 自定义类需实现 Comparable 接口

class Student implements Comparable<Student> {

    int score;

    public int compareTo(Student o) { return this.score - o.score; }

}

```

  

</details>

  

---

  

**75.** ①设计一个计算周长和面积的接口。②创建圆类实现该接口，重写 toString。③设计测试类，键盘输入半径，输出圆的信息。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

```java

// ① 接口

interface Shape {

    double getPerimeter();

    double getArea();

}

  

// ② 圆类

class Circle implements Shape {

    private double radius;

    public Circle(double r) { this.radius = r; }

    public double getPerimeter() { return 2 * Math.PI * radius; }

    public double getArea() { return Math.PI * radius * radius; }

    public String toString() {

        return "圆[半径=" + radius + ", 周长=" + getPerimeter() + ", 面积=" + getArea() + "]";

    }

}

  

// ③ 测试类

public class Test {

    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        System.out.print("请输入半径: ");

        double r = sc.nextDouble();

        Circle c = new Circle(r);

        System.out.println(c.toString());

    }

}

```

  

</details>

  

---

  

**76.** 从键盘读入 n 个整数（n<=1000），统计每个数出现的次数，从小到大输出每个出现过的数及每个数出现的次数。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

```java

import java.util.*;

  

public class Test {

    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        TreeMap<Integer, Integer> map = new TreeMap<>();

        int n = sc.nextInt();

        for (int i = 0; i < n; i++) {

            int num = sc.nextInt();

            map.put(num, map.getOrDefault(num, 0) + 1);

        }

        for (Map.Entry<Integer, Integer> e : map.entrySet()) {

            System.out.println(e.getKey() + " 出现 " + e.getValue() + " 次");

        }

    }

}

```

  

> 使用 TreeMap 自动按 key 排序；`getOrDefault` 简化计数逻辑。

  

</details>

  

---

  

**77.** 编程计算中华人民共和国自成立至今的天数。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

```java

import java.time.LocalDate;

import java.time.temporal.ChronoUnit;

  

public class Test {

    public static void main(String[] args) {

        LocalDate founding = LocalDate.of(1949, 10, 1);

        LocalDate today = LocalDate.now();

        long days = ChronoUnit.DAYS.between(founding, today);

        System.out.println("中华人民共和国成立至今已 " + days + " 天");

    }

}

```

  

</details>

  

---

  

**78.** 编程基于 Socket 的服务器端通信程序，读取一行客户端信息并回复。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

```java

import java.io.*;

import java.net.*;

  

public class Server {

    public static void main(String[] args) throws IOException {

        ServerSocket server = new ServerSocket(8888);

        System.out.println("服务器启动，等待连接...");

        Socket client = server.accept();

        BufferedReader in = new BufferedReader(

            new InputStreamReader(client.getInputStream()));

        PrintWriter out = new PrintWriter(client.getOutputStream(), true);

        String msg = in.readLine();

        System.out.println("收到: " + msg);

        out.println("你的信息已收到");

        client.close();

        server.close();

    }

}

```

  

</details>

  

---

  

**79.** ①设计周长和面积接口。②创建矩形类实现接口，重写 toString。③测试。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

```java

// ① 接口（同 Q75）

interface Shape {

    double getPerimeter();

    double getArea();

}

  

// ② 矩形类

class Rectangle implements Shape {

    private double length, width;

    public Rectangle(double l, double w) { length = l; width = w; }

    public double getPerimeter() { return 2 * (length + width); }

    public double getArea() { return length * width; }

    public String toString() {

        return "矩形[长=" + length + ", 宽=" + width

            + ", 周长=" + getPerimeter() + ", 面积=" + getArea() + "]";

    }

}

  

// ③ 测试

public class Test {

    public static void main(String[] args) {

        Rectangle r = new Rectangle(5, 3);

        System.out.println(r.toString());

    }

}

```

  

</details>

  

---

  

**80.** 将一个数组、一行字符串和一个布尔值通过对象输出流写入文件中，然后用对象输入流读出并输出。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

```java

import java.io.*;

  

public class Test {

    public static void main(String[] args) throws Exception {

        // 写入

        ObjectOutputStream oos = new ObjectOutputStream(

            new FileOutputStream("data.dat"));

        oos.writeObject(new int[]{1, 2, 3, 4, 5});

        oos.writeObject("Hello Java");

        oos.writeBoolean(true);

        oos.close();

        // 读出

        ObjectInputStream ois = new ObjectInputStream(

            new FileInputStream("data.dat"));

        int[] arr = (int[]) ois.readObject();

        String str = (String) ois.readObject();

        boolean flag = ois.readBoolean();

        ois.close();

        System.out.println(Arrays.toString(arr));  // [1,2,3,4,5]

        System.out.println(str);                   // Hello Java

        System.out.println(flag);                  // true

    }

}

```

  

> ⚠️ `readObject()` 返回 `Object`，需要**强制类型转换**；读的顺序必须与写的顺序一致。

  

</details>

  

---

  

**81.** 编写 TCP Socket 双向通信程序，模拟简单 QQ 聊天功能。

  

<details class="lake-collapse"><summary><strong>答案与解析</strong></summary>

  

**服务端：**

```java

import java.io.*;

import java.net.*;

  

public class ChatServer {

    public static void main(String[] args) throws IOException {

        ServerSocket server = new ServerSocket(8888);

        Socket client = server.accept();

        BufferedReader in = new BufferedReader(

            new InputStreamReader(client.getInputStream()));

        PrintWriter out = new PrintWriter(client.getOutputStream(), true);

        BufferedReader console = new BufferedReader(

            new InputStreamReader(System.in));

        String line;

        while (true) {

            // 接收客户端消息

            if (in.ready()) {

                line = in.readLine();

                if ("bye".equals(line)) break;

                System.out.println("客户端: " + line);

            }

            // 发送消息

            if (console.ready()) {

                line = console.readLine();

                out.println(line);

                if ("bye".equals(line)) break;

            }

        }

        client.close();

        server.close();

    }

}

```

  

> 双向通信需分别用两个流处理收发，可通过多线程实现同时收发。

  

</details>