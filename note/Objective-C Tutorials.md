# 基本Objective-C

## 概述

------

Objective-C 是一种通用的、面向对象的编程语言，它在 C 编程语言中添加了 Smalltalk 风格的消息传递。 这是 Apple 用于 OS X 和 iOS 操作系统及其各自的 API Cocoa 和 Cocoa Touch 的主要编程语言。 本参考资料将带您通过简单实用的方法学习 Objective-C 编程语言。2014年Apple推出了Swift，至今Swift不断发展更新完善，Apple平台正全面向Swift迁移，但与不用担心老Objective-C项目不被支持，您可以在同一Xcode项目中同时使用Objectice-C和Swift。

此参考资料专为初学者准备，可帮助他们了解与 Objective-C 编程语言相关的基本概念和高级概念。

在您开始使用本参考资料中提供的各种类型的示例进行练习之前，最好有一些C语言编程基础。



## 环境设置

------

### 本地环境设置

你需要在你的电脑上安装 **文本编辑器** 和 **GCC 编译器**。

------

### 文本编辑器

这将用于键入您的程序。 一些编辑器的示例包括 Windows 记事本、操作系统编辑命令、Brief、Epsilon、EMACS 和 vim 或 vi。

文本编辑器的名称和版本可能因操作系统而异。 例如，记事本将在 Windows 上使用，而 vim 或 vi 既可以在 Windows 上使用，也可以在 Linux 或 UNIX 上使用。

您使用编辑器创建的文件称为源文件并包含程序源代码。 Objective-C 程序的源文件通常以扩展名"**.m**"命名。

在开始你的编程之前，确保你有一个文本编辑器，并且你有足够的经验来编写一个计算机程序，将它保存在一个文件中，编译它并最终执行它。

------

### GCC 编译器

写在源文件中的源代码是程序的人类可读源代码。 它需要被"编译"成机器语言，这样你的 CPU 才能真正按照给定的指令执行程序。

此 GCC 编译器将用于将您的源代码编译成最终的可执行程序。 假设您具有关于编程语言编译器的基本知识。

GCC 编译器可在各种平台上免费使用，下面介绍在各种平台上设置的过程。

------

### 在 UNIX/Linux 上安装

第一步是安装 gcc 和 gcc Objective-C 包。 这是由

```
$ su - 
$ yum install gcc
$ yum install gcc-objc
```

下一步是使用以下命令设置包依赖关系

```
$ yum install make libpng libpng-devel libtiff libtiff-devel libobjc 
   libxml2 libxml2-devel libX11-devel libXt-devel libjpeg libjpeg-devel
```

为了获得 Objective-C 的全部功能，请下载并安装 GNUStep。 这可以通过从 [http://main.gnustep.org/resources/downloads.php](http://wwwmain.gnustep.org/resources/downloads.php?site=ftp%3A%2F%2Fftp.gnustep.org%2Fpub%2Fgnustep%2F#core/) 下载软件包来完成。

现在，我们需要切换到下载的文件夹并解压文件 

```
$ tar xvfz gnustep-startup-.tar.gz
```

现在，我们需要切换到使用创建的文件夹 gnustep-startup 

```
$ cd gnustep-startup-<version>
 
```

接下来，我们需要配置构建过程 

```
$ ./configure
 
```

然后，我们可以通过 

```
$ make
 
```

我们最终需要通过以下方式设置环境 

```
$ . /usr/GNUstep/System/Library/Makefiles/GNUstep.sh
```

我们有一个 helloWorld.m Objective-C 如下 

```
#import <Foundation/Foundation.h>

int main (int argc, const char * argv[]) {
   NSAutoreleasePool * pool = [[NSAutoreleasePool alloc] init];
   
   NSLog (@"hello world");
   [pool drain];
   return 0;
}
 
```

现在，我们可以编译并运行一个 Objective-C 文件 helloWorld.m，方法是使用 cd 切换到包含该文件的文件夹，然后使用以下步骤 

```
$ gcc `gnustep-config --objc-flags` 
-L/usr/GNUstep/Local/Library/Libraries 
-lgnustep-base helloWorld.m -o helloWorld
$ ./helloWorld
 
```

我们可以看到如下输出 

```
2013-09-07 10:48:39.772 tutorialsPoint[12906] hello world
```

------

### 在 Mac OS 上安装

如果您使用 Mac OS X，获得 GCC 的最简单方法是从 Apple 网站下载 Xcode 开发环境并按照简单的安装说明进行操作。 一旦你设置了 Xcode，你就可以使用 GNU 编译器来编译 C/C++。

Xcode 目前在 [developer.apple.com/technologies/tools/](https://developer.apple.com/technologies/tools/) 上可用。

------

### 在 Windows 上安装

为了在windows上运行Objective-C程序，我们需要安装MinGW和GNUStep Core。 两者都可以在 https://www.gnu.org/software/gnustep/windows/installer.html 上买到。

首先，我们需要安装 MSYS/MinGW 系统包。 然后，需要安装 GNUstep 核心包。 两者都提供了一个 windows 安装程序。

然后通过选择 Start -> All Programs -> GNUstep -> Shell 来使用 Objective-C 和 GNUstep

切换到包含 helloWorld.m 的文件夹

可以使用 

```
$ gcc `gnustep-config --objc-flags` 
-L /GNUstep/System/Library/Libraries hello.m -o hello -lgnustep-base -lobjc
```

可以使用 

```
./hello.exe
```

得到以下输出 

```
2013-09-07 10:48:39.772 tutorialsPoint[1200] hello world
```



## 程序结构

------

### Objective-C Hello World 示例

一个 Objective-C 程序基本上由以下部分组成 

- 预处理器命令
- 接口
- 执行
- 方法
- 变量
- 声明和表达式
- 注释

让我们看一个打印"Hello World"字样的简单代码 

```objective-c
#import <Foundation/Foundation.h>

@interface SampleClass:NSObject
- (void)sampleMethod;
@end

@implementation SampleClass

- (void)sampleMethod {
   NSLog(@"Hello, World! \n");
}

@end

int main() {
   /* my first program in Objective-C */
   SampleClass *sampleClass = [[SampleClass alloc]init];
   [sampleClass sampleMethod];
   return 0;
}
 
```

让我们看看上面程序的各个部分 

- 程序 *#import <Foundation/Foundation.h>* 的第一行是预处理器命令，它告诉 Objective-C 编译器在进行实际编译之前包含 Foundation.h 文件。
- 下一行 *@interface SampleClass:NSObject* 展示了如何创建一个接口。 它继承了NSObject，它是所有对象的基类。
- 下一行 *- (void)sampleMethod;* 展示了如何声明一个方法。
- 下一行 *@end* 标记接口的结束。
- 下一行 *@implementation SampleClass* 展示了如何实现接口SampleClass。
- 下一行 *- (void)sampleMethod{}* 显示了 sampleMethod 的实现。
- 下一行 *@end* 标志着一个实现的结束。
- 下一行 *int main()* 是程序开始执行的 main 函数。
- 下一行 /*...*/ 将被编译器忽略，它已被放置在程序中添加附加注释。 所以这样的行在程序中被称为注释。
- 下一行 *NSLog(...)* 是 Objective-C 中可用的另一个函数，它会导致消息"Hello, World!" 显示在屏幕上。
- 下一行 **return 0;** 终止 main() 函数并返回值 0。

------

### Compile & Execute Objective-C Program

现在当我们编译并运行程序时，我们将得到如下结果。

```objective-c
2017-10-06 07:48:32.020 demo[65832] Hello, World!
```



## 基本语法

------

### Objective-C 中的标记

Objective-C 程序由各种标记组成，标记可以是关键字、标识符、常量、字符串文字或符号。 例如，以下 Objective-C 语句由六个标记组成 −

```objective-c
NSLog(@"Hello, World! \n");
 
```

各个标记是 −

```objective-c
NSLog
@
(
   "Hello, World! \n"
)
;
 
```

------

### 分号;

在Objective-C程序中，分号是语句的结束符。 也就是说，每个单独的语句必须以分号结束。 它表示一个逻辑实体的结束。

例如，下面是两个不同的语句 −

```objective-c
NSLog(@"Hello, World! \n");
return 0;
 
```

------

### 注释

注释就像 Objective-C 程序中的帮助文本，它们会被编译器忽略。 它们以 /* 开头并以字符 */ 结束，如下所示 −

```objective-c
/* my first program in Objective-C */
```

您不能在注释中添加注释，并且它们不会出现在字符串或字符文字中。

------

### 标识符

Objective-C 标识符是用于标识变量、函数或任何其他用户定义项的名称。 标识符以字母 A 到 Z 或 a 到 z 或下划线 _ 开头，后跟零个或多个字母、下划线和数字（0 到 9）。

Objective-C 不允许在标识符中使用标点符号，例如 @、$ 和 %。 Objective-C 是一种**区分大小写**的编程语言。 因此，*Manpower* 和 *manpower* 是 Objective-C 中的两个不同标识符。 以下是可接受的标识符的一些示例 −

```
mohd       zara    abc   move_name  a_123
myname50   _temp   j     a23b9      retVal
```

------

### 保留关键字

下面的列表显示了 Objective-C 中的一些保留字。 这些保留字不能用作常量或变量或任何其他标识符名称。

| auto     | else               | long      | switch         |
| -------- | ------------------ | --------- | -------------- |
| break    | enum               | register  | typedef        |
| case     | extern             | return    | union          |
| char     | float              | short     | unsigned       |
| const    | for                | signed    | void           |
| continue | goto               | sizeof    | volatile       |
| default  | if                 | static    | while          |
| do       | int                | struct    | _Packed        |
| double   | protocol           | interface | implementation |
| NSObject | NSInteger          | NSNumber  | CGFloat        |
| property | nonatomic;         | retain    | strong         |
| weak     | unsafe_unretained; | readwrite | readonly       |

------

### Objective-C 中的空格

仅包含空格且可能带有注释的行称为空行，Objective-C 编译器会完全忽略它。

空格是 Objective-C 中用来描述空格、制表符、换行符和注释的术语。 空格将语句的一部分与另一部分分开，使编译器能够识别语句中的一个元素（例如 int）在哪里结束以及下一个元素在哪里开始。 因此，在下面的语句中 −

```objective-c
int age;
```

int 和 age 之间必须至少有一个空白字符（通常是一个空格），编译器才能区分它们。 另一方面，在以下声明中，

```objective-c
fruit = apples + oranges;   // get the total fruit
 
```

fruit 和 = 之间，或 = 和 apples 之间不需要空格字符，但如果您希望提高可读性，可以随意包含一些空格字符。



### 数据类型

------

在 Objective-C 编程语言中，数据类型是指用于声明不同类型的变量或函数的广泛系统。 变量的类型决定了它在存储中占用多少空间以及如何解释存储的位模式。

Objective-C 中的类型可以分为以下几类 −

| 序号 |                         类型 & 描述                          |
| :--- | :----------------------------------------------------------: |
| 1    | **基本类型 −**它们是算术类型，由两种类型组成:(a) 整数类型和 (b) 浮点类型。 |
| 2    | **枚举类型−**它们又是算术类型，用于定义在整个程序中只能分配特定离散整数值的变量。 |
| 3    |      **类型 void −**类型说明符*void* 表示没有可用的值。      |
| 4    | **派生类型 −**它们包括 (a) 指针类型，(b) 数组类型，(c) 结构类型，(d) 联合类型和 (e) 函数类型。 |

数组类型和结构类型统称为聚合类型。 函数的类型指定了函数返回值的类型。 我们将在下一节中看到基本类型，而其他类型将在接下来的章节中介绍。

------

### 整数类型

下表为您提供了有关标准整数类型及其存储大小和取值范围的详细信息 −

| 类型           |  存储大小  | 取值范围                                             |
| :------------- | :--------: | :--------------------------------------------------- |
| char           |   1字节    | -128 到 127 或 0 到 255                              |
| unsigned char  |   1字节    | 0 到 255                                             |
| signed char    |   1字节    | -128 到 127                                          |
| int            | 2 或 4字节 | -32,768 至 32,767 或 -2,147,483,648 至 2,147,483,647 |
| unsigned int   | 2 或 4字节 | 0 到 65,535 或 0 到 4,294,967,295                    |
| short          |   2字节    | -32,768 到 32,767                                    |
| unsigned short |   2字节    | 0 到 65,535                                          |
| long           |   4字节    | -2,147,483,648 到 2,147,483,647                      |
| unsigned long  |   4字节    | 0 到 4,294,967,295                                   |

要在特定平台上获取类型或变量的确切大小，可以使用 **sizeof** 运算符。表达式 *sizeof(type)* 产生对象或类型的存储大小（以字节为单位）。 以下是在任何机器上获取 int 类型大小的示例 −

```objective-c
#import <Foundation/Foundation.h>

int main() {
   NSLog(@"Storage size for int : %d \n", sizeof(int));
   return 0;
}
 
```

当你编译并执行上面的程序时，它在 Linux 上产生如下结果 −

```objective-c
2013-09-07 22:21:39.155 demo[1340] Storage size for int : 4 
```

------

### 浮点类型

下表为您提供了有关标准浮点类型的详细信息，包括存储大小和值范围及其精度 −

|    类型     | 存储大小 |        取值范围        |      精度      |
| :---------: | :------: | :--------------------: | :------------: |
|    float    |  4字节   |    1.2E-38到3.4E+38    |    6 位小数    |
|   double    |  8字节   |   2.3E-308到1.7E+308   | 小数点后 15 位 |
| long double |  10字节  | 3.4E-4932 到 1.1E+4932 |   19 位小数    |

头文件 float.h 定义了宏，允许您在程序中使用这些值和有关实数二进制表示的其他详细信息。 以下示例将打印 float 类型占用的存储空间及其范围值 −

```objective-c
#import <Foundation/Foundation.h>

int main() {
   NSLog(@"Storage size for float : %d \n", sizeof(float));
   return 0;
}
 
```

当你编译并执行上面的程序时，它在 Linux 上产生如下结果 −

```objective-c
2013-09-07 22:22:21.729 demo[3927] Storage size for float : 4 
```

------

### void 类型

void 类型指定没有可用的值。 用于三种情况 −

| 序号 |                          类型和描述                          |
| :--- | :----------------------------------------------------------: |
| 1    | **函数返回 void**在 Objective-C 中有很多函数不返回值，或者你可以说它们返回 void。 没有返回值的函数的返回类型为 void。 例如，**void exit (int status);** |
| 2    | **函数参数为 void**在 Objective-C 中有许多不接受任何参数的函数。 没有参数的函数可以接受为 void。 例如，**int rand(void);** |

此时您可能还不理解 void 类型，所以让我们继续，我们将在后续章节中介绍这些概念。



## 变量

------

变量只不过是给我们的程序可以操作的存储区域的名称。 Objective-C 中的每个变量都有一个特定的类型，它决定了变量内存的大小和布局； 该内存中可以存储的值的范围； 以及可以应用于变量的一组操作。

变量名可以由字母、数字和下划线字符组成。 它必须以字母或下划线开头。 大写字母和小写字母是不同的，因为 Objective-C 是区分大小写的。 基于上一章讲解的基本类型，会有以下基本变量类型 −

| 序号 |               类型 & 描述                |
| :--- | :--------------------------------------: |
| 1    | **char**通常是一个八位字节（一个字节）。 |
| 2    |      **int**机器最自然的整数大小。       |
| 3    |         **float**单精度浮点值。          |
| 4    |         **double**双精度浮点值。         |
| 5    |          **void**表示没有类型。          |

Objective-C 编程语言还允许定义各种其他类型的变量，我们将在后续章节中介绍这些变量，如枚举、指针、数组、结构、联合等。本章我们只研究基本的变量类型。

------

### Objective-C 中的变量定义

变量定义意味着告诉编译器在何处以及为变量创建多少存储空间。 变量定义指定一种数据类型并包含该类型的一个或多个变量的列表，如下所示 −

```objective-c
type variable_list;
 
```

这里，**type**必须是有效的Objective-C数据类型，包括char、w_char、int、float、double、bool或任何用户定义的对象等，以及**variable_list** 可以由一个或多个用逗号分隔的标识符名称组成。 此处显示了一些有效的声明 −

```objective-c
int    i, j, k;
char   c, ch;
float  f, salary;
double d;
 
```

行 **int i, j, k;** 声明和定义了变量 i, j 和 k; 它指示编译器创建名为 i、j 和 k 的 int 类型变量。

变量可以在它们的声明中被初始化（分配一个初始值）。 初始化器由一个等号和一个常量表达式组成，如下所示 −

```
type variable_name = value;
 
```

Some examples are −

```objective-c
extern int d = 3, f = 5;    // declaration of d and f. 
int d = 3, f = 5;           // definition and initializing d and f. 
byte z = 22;                // definition and initializes z. 
char x = 'x';               // the variable x has the value 'x'.
 
```

对于没有初始化器的定义:具有静态存储持续时间的变量被隐式初始化为 NULL（所有字节的值为 0）； 所有其他变量的初始值未定义。

------

### Objective-C 中的变量声明

变量声明向编译器保证存在一个具有给定类型和名称的变量，以便编译器继续进行进一步的编译，而无需有关该变量的完整详细信息。 变量声明仅在编译时有意义，编译器在程序链接时需要实际的变量声明。

当您使用多个文件并且您在其中一个文件中定义您的变量时，变量声明很有用，这将在程序链接时可用。 您将使用 **extern** 关键字在任何地方声明变量。 虽然你可以在你的 Objective-C 程序中多次声明一个变量，但它只能在文件、函数或代码块中定义一次。

------

### 示例

试试下面的例子，其中变量已经在顶部声明，但它们已经在主函数内部定义和初始化 −

```objective-c
#import <Foundation/Foundation.h>

// Variable declaration:
extern int a, b;
extern int c;
extern float f;

int main () {
  /* variable definition: */
  int a, b;
  int c;
  float f;
 
  /* actual initialization */
  a = 10;
  b = 20;
  
  c = a + b;
  NSLog(@"value of c : %d \n", c);

  f = 70.0/3.0;
  NSLog(@"value of f : %f \n", f);
 
  return 0;
}
 
```

当上面的代码被编译和执行时，会产生如下结果 −

```objective-c
2013-09-07 22:43:31.695 demo[14019] value of c : 30 
2013-09-07 22:43:31.695 demo[14019] value of f : 23.333334 
 
```

相同的概念适用于函数声明，您在函数声明时提供函数名称，并且可以在其他任何地方给出其实际定义。 在下面的例子中，它是使用 C 函数解释的，正如你所知，Objective-C 也支持 C 风格的函数 −

```objective-c
// function declaration
int func();

int main() {
   // function call
   int i = func();
}

// function definition
int func() {
   return 0;
}
 
```

------

### Objective-C 中的左值和右值

Objective-C中有两种表达式 −

- **lvalue** − 引用内存位置的表达式称为"左值"表达式。 左值可能出现在赋值的左侧或右侧。
- **rvalue** − 术语右值是指存储在内存中某个地址的数据值。 右值是一个不能被赋值的表达式，这意味着右值可能出现在赋值的右侧，但不会出现在左侧。

变量是左值，因此可能出现在赋值语句的左侧。 数字文字是右值，因此可能无法分配并且不能出现在左侧。 以下是有效声明 −

```objective-c
int g = 20;
```

但以下不是有效的语句，会产生编译时错误 −

```objective-c
10 = 20;
```



## 常量

------

常量指的是程序在执行期间不能改变的固定值。 这些固定值也称为**字面量**。

常量可以是任何基本数据类型，例如*整数常量、浮点常量、字符常量或字符串文字*。 还有枚举常量。

**常量** 就像常规变量一样对待，只是它们的值在定义后不能修改。

------

### 整型字面量

整型字面量可以是十进制、八进制或十六进制常量。 前缀指定基数或基数:十六进制为 0x 或 0X，八进制为 0，十进制为空。

整数文字也可以有一个后缀，它是 U 和 L 的组合，分别表示无符号和长整型。 后缀可以是大写或小写，并且可以是任何顺序。

这里有一些整型字面量的例子 −

```objective-c
212         /* Legal */
215u        /* Legal */
0xFeeL      /* Legal */
078         /* Illegal: 8 is not an octal digit */
032UU       /* Illegal: cannot repeat a suffix */
 
```

以下是各种类型的整数字面量的其他示例 −

```objective-c
85         /* decimal */
0213       /* octal */
0x4b       /* hexadecimal */
30         /* int */
30u        /* unsigned int */
30l        /* long */
30ul       /* unsigned long */
 
```

------

### 浮点字面量

浮点字面值有整数部分、小数点、小数部分和指数部分。 您可以用十进制形式或指数形式表示浮点文字。

当使用小数形式表示时，您必须包括小数点、指数或两者，而当使用指数形式表示时，您必须包括整数部分、小数部分或两者。 带符号的指数由 e 或 E 引入。

下面是一些浮点字面量的例子 −

```objective-c
3.14159       /* Legal */
314159E-5L    /* Legal */
510E          /* Illegal: incomplete exponent */
210f          /* Illegal: no decimal or exponent */
.e55          /* Illegal: missing integer or fraction */
 
```

------

### 字符常量

字符文字包含在单引号中，例如，'x'，并且可以存储在 **char** 类型的简单变量中。

字符文字可以是纯字符（例如，'x'）、转义序列（例如，'\t'）或通用字符（例如，'\u02C0'）。

C 语言中有些字符前面加反斜杠时会有特殊的含义，用于表示换行符（\n）或制表符（\t）。 在这里，您有一些此类转义序列代码的列表 −

| 转义序列    |         含义         |
| :---------- | :------------------: |
| \\          |        \ 字符        |
| \'          |        ' 字符        |
| \"          |        " 字符        |
| \?          |        ? 字符        |
| \a          |      警报或响铃      |
| \b          |        退格键        |
| \f          |         换页         |
| \n          |        换行符        |
| \r          |         回车         |
| \t          |      水平制表符      |
| \v          |      垂直制表符      |
| \ooo        |  一到三位的八进制数  |
| \xhh 。 . . | 一位或多位十六进制数 |

以下是显示少量转义序列字符的示例 −

```objective-c
#import <Foundation/Foundation.h>

int main() {
   NSLog(@"Hello\tWorld\n\n");
   return 0;
}
 
```

当上面的代码被编译和执行时，会产生如下结果 −

```objective-c
2013-09-07 22:17:17.923 demo[17871] Hello	World
```

------

### 字符串文字

字符串文字或常量用双引号""括起来。 字符串包含类似于字符文字的字符:纯字符、转义序列和通用字符。 您可以使用字符串文字将长行分成多行并使用空格分隔它们。

这里有一些字符串文字的例子。 所有三种形式都是相同的字符串。

```objective-c
"hello, dear"

"hello, \

dear"

"hello, " "d" "ear"
 
```

------

### 定义常量

C中定义常量有两种简单的方法 −

- 使用 **#define** 预处理器。
- 使用 **const** 关键字。

------

### #define 预处理器

下面是使用 #define 预处理器定义常量的形式 −

```objective-c
#define identifier value
 
```

下面的例子详细解释了 −

```objective-c
#import <Foundation/Foundation.h>

#define LENGTH 10   
#define WIDTH  5
#define NEWLINE '\n'

int main() {
   int area;
   area = LENGTH * WIDTH;
   NSLog(@"value of area : %d", area);
   NSLog(@"%c", NEWLINE);

   return 0;
}
 
```

当上面的代码被编译和执行时，会产生如下结果 −

```objective-c
2013-09-07 22:18:16.637 demo[21460] value of area : 50
2013-09-07 22:18:16.638 demo[21460] 
 
```

------

### const 关键字

可以使用 **const**前缀来声明特定类型的常量，如下所示 −

```objective-c
const type variable = value;
 
```

下面的例子详细解释了 −

```objective-c
#import <Foundation/Foundation.h>

int main() {
   const int  LENGTH = 10;
   const int  WIDTH  = 5;
   const char NEWLINE = '\n';
   int area;  
   
   area = LENGTH * WIDTH;
   NSLog(@"value of area : %d", area);
   NSLog(@"%c", NEWLINE);

   return 0;
}
 
```

当上面的代码被编译和执行时，会产生如下结果 −

```objective-c
2013-09-07 22:19:24.780 demo[25621] value of area : 50
2013-09-07 22:19:24.781 demo[25621] 
```

请注意，以大写形式定义常量是一种很好的编程习惯。