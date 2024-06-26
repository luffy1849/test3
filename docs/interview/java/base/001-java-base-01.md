---
title: java基础面试问题(一)
---

# Java概述

## 什么是Java

Java是一门面向对象编程语言，不仅吸收了C++语言的各种优点，还摒弃了C++里难以理解的多继 承、指针等概念，因此Java语言具有功能强大和简单易用两个特征。Java语言作为静态面向对象编程语言的代表，极好地实现了面向对象理论，允许程序员以优雅的思维方式进行复杂的编程 。

## Jdk和Jre和JVM的区别

 

* JDK ：Jdk还包括了一些Jre之外的东西 ，就是这些东西帮我们编译Java代码的， 还有就是监控Jvm 的一些工具 Java Development Kit是提供给Java开发人员使用的，其中包含了Java的开发工具，也包括了JRE。所以安装了JDK，就无需再单独安装JRE了。其中的开发工具：编译工具(javac.exe)， 打包工具(jar.exe)等

* JRE ：Jre大部分都是 C 和 C++ 语言编写的，他是我们在编译java时所需要的基础的类库 Java Runtime  Environment包括Java虚拟机和Java程序所需的核心类库等。核心类库主要是java.lang 包：包含了运行Java程序必不可少的系统类，如基本数据类型、基本数学函数、字符串处理、线 程、异常处理类等，系统缺省加载这个包

如果想要运行一个开发好的Java程序，计算机中只需要安装JRE即可。

* Jvm：在倒数第二层 由他可以在（最后一层的）各种平台上运行 Java Virtual Machine是Java虚拟机，Java程序需要运行在虚拟机上，不同的平台有自己的虚拟机，因此Java语言可以实现跨平台。

![img](https://upload-images.jianshu.io/upload_images/54256-cea8bcf9e1be3413.png?imageMogr2/auto-orient/strip|imageView2/2/w/770/format/webp)

 

## 什么是跨平台性？原理是什么

所谓跨平台性，是指java语言编写的程序，一次编译后，可以在多个系统平台上运行。

实现原理：Java程序是通过java虚拟机在系统平台上运行的，只要该系统可以安装相应的java虚拟机，该系统就可以运行java程序。

## Java语言有哪些特点

简单易学（Java语言的语法与C语言和C++语言很接近） 面向对象（封装，继承，多态）

平台无关性（Java虚拟机实现平台无关性）

支持网络编程并且很方便（Java语言诞生本身就是为简化网络编程设计的） 支持多线程（多线程机制使应用程序在同一时间并行执行多项任）

健壮性（Java语言的强类型机制、异常处理、垃圾的自动收集等） 安全性好

## 什么是字节码？采用字节码的最大好处是什么

**字节码**：Java源代码经过虚拟机编译器编译后产生的文件（即扩展为.class的文件），它不面向任何特定的处理器，只面向虚拟机。

#### 采用字节码的好处：

Java语言通过字节码的方式，在一定程度上解决了传统解释型语言执行效率低的问题，同时又保留了解释型语言可移植的特点。所以Java程序运行时比较高效，而且，由于字节码并不专对一种特定的机器，因此，Java程序无须重新编译便可在多种不同的计算机上运行。

#### java中的编译器和解释器：

Java中引入了虚拟机的概念，即在机器和编译程序之间加入了一层抽象的虚拟机器。这台虚拟的机器在任何平台上都提供给编译程序一个的共同的接口。编译程序只需要面向虚拟机，生成虚拟机能够理解的代码，然后由解释器来将虚拟机代码转换为特定系统的机器码执行。

在Java中，这种供虚 拟机理解的代码叫做字节码（即扩展为.class的文件），它不面向任何特定的处理器，只面向虚拟机。

每一种平台的解释器是不同的，但是实现的虚拟机是相同的。Java源程序经过编译器编译后变成字节码，字节码由虚拟机解释执行，虚拟机将每一条要执行的字节码送给解释器，解释器将其翻译成特定机器上的机器码，然后在特定的机器上运行，这就是上面提到的Java的特点的编译与解释并存的解释。

Java源代码---->编译器---->jvm可执行的Java字节码(即虚拟指令)---->jvm---->jvm中解释器-->机器可执行的二进制机器码-->程序运行。

## 什么是Java程序的主类？应用程序和小程序的主类有何不同？

一个程序中可以有多个类，但只能有一个类是主类。在Java应用程序中，这个主类是指包含main() 方法的类。而在Java小程序中，这个主类是一个继承自系统类JApplet或Applet的子类。应用程序 的主类不一定要求是public类，但小程序的主类要求必须是public类。主类是Java程序执行的入口 点。

## Java应用程序与小程序之间有那些差别？

简单说应用程序是从主线程启动(也就是main()方法)。applet小程序没有main方法，主要是嵌在浏 览器页面上运行(调用init()线程或者run()来启动)，嵌入浏览器这点跟ﬂash的小游戏类似。

## Java和C++的区别

* 都是面向对象的语言，都支持封装、继承和多态

* Java不提供指针来直接访问内存，程序内存更加安全

* Java的类是单继承的，C++支持多重继承；虽然Java的类不可以多继承，但是接口可以多继承。
* Java有自动内存管理机制，不需要程序员手动释放无用内存

## Oracle JDK 和 OpenJDK 的对比

1. Oracle JDK版本将每三年发布一次，而OpenJDK版本每三个月发布一次；

2. OpenJDK 是一个参考模型并且是完全开源的，而Oracle JDK是OpenJDK的一个实现，并不是完全开源的；

3. Oracle JDK 比 OpenJDK 更稳定。OpenJDK和Oracle JDK的代码几乎相同，但Oracle JDK有更多的类和一些错误修复。因此，如果您想开发企业/商业软件，我建议您选择Oracle  JDK，因为它经过了彻底的测试和稳定。某些情况下，有些人提到在使用OpenJDK 可能会遇到了许多应用程序崩溃的问题，但是，只需切换到Oracle JDK就可以解决问题；

4. 在响应性和JVM性能方面，Oracle JDK与OpenJDK相比提供了更好的性能；

5. Oracle JDK不会为即将发布的版本提供长期支持，用户每次都必须通过更新到最新版本获得支持来获取最新版本；

6. Oracle JDK根据二进制代码许可协议获得许可，而OpenJDK根据GPL v2许可获得许可。

# 基础语法

## 数据类型

### Java有哪些数据类型

**定义**：Java语言是强类型语言，对于每一种数据都定义了明确的具体的数据类型，在内存中分配了不同大小的内存空间。

#### 分类 

基本数据类型

* 数值型

* 整数类型(byte,short,int,long)

​    浮点类型(float,double) 

​	字符型(char)

​	布尔型(boolean) 

* 引用数据类型

​	类(class)

​	接口(interface) 

​	数组([])



**Java基本数据类型图**



![image-20240418174551795](https://flydean-1301049335.cos.ap-guangzhou.myqcloud.com/img/202404181745473.png)

 

 

### switch 是否能作用在 byte 上，是否能作用在 long 上，是否能作用在 String上

在 Java 5 以前，switch(expr)中，expr 只能是 byte、short、char、int。

从 Java5 开始，Java 中引入了枚举类型，expr 也可以是 enum 类型，从 Java 7 开始，expr 还可以是字符串（String）， 但是长整型（long）在目前所有的版本中都是不可以的。

### 用最有效率的方法计算 2 乘以 8

2 << 3（左移 3 位相当于乘以 2 的 3 次方，右移 3 位相当于除以 2 的 3 次方）。

### Math.round(11.5) 等于多少？Math.round(-11.5)等于多少

Math.round(11.5)的返回值是 12，Math.round(-11.5)的返回值是-11。四舍五入的原理是在参数上加 0.5 然后进行下取整。

### float f=3.4;是否正确

不正确。3.4 是双精度数，将双精度型（double）赋值给浮点型（float）属于下转型（down- casting，也称为窄化）会造成精度损失，因此需要强制类型转换float f =(float)3.4; 或者写成 float f =3.4F;。

### short s1 = 1; s1 = s1 + 1;有错吗?short s1 = 1; s1 += 1;有错吗

对于 short s1 = 1; s1 = s1 + 1;由于 1 是 int 类型，因此 s1+1 运算结果也是 int型，需要强制转换类型才能赋值给 short 型。

而 short s1 = 1; s1 += 1;可以正确编译，因为 s1+= 1;相当于 s1 = (short(s1 + 1);其中有隐含的强制类型转换。

## 编码

### Java语言采用何种编码方案？有何特点？

Java语言采用Unicode编码标准，Unicode（标准码），它为每个字符制订了一个唯一的数值，因 此在任何的语言，平台，程序都可以放心的使用。

## 注释

### 什么Java注释

**定义**：用于解释说明程序的文字

**分类**

​	单行注释

​	格式： // 注释文字

​	多行注释

​	格式： /* 注释文字 */

​	文档注释

​	格式：/** 注释文字 */

#### 作用 

在程序中，尤其是复杂的程序中，适当地加入注释可以增加程序的可读性，有利于程序的修改、调试和交流。注释的内容在程序编译的时候会被忽视，不会产生目标代码，注释的部分不会对程序的 执行结果产生任何影响。

## 访问修饰符

### 访问修饰符   public,private,protected,以及不写（默认）时的区别

**定义**：Java中，可以使用访问修饰符来保护对类、变量、方法和构造方法的访问。Java 支持 4 种不同的访问权限。

#### 分类

* private : 在同一类内可见。使用对象：变量、方法。 注意：不能修饰类（外部类）

* default (即缺省，什么也不写，不使用任何关键字）: 在同一包内可见，不使用任何修饰符。使用对象：类、接口、变量、方法。

* protected : 对同一包内的类和所有子类可见。使用对象：变量、方法。 注意：不能修饰类（外部类）。

* public : 对所有类可见。使用对象：类、接口、变量、方法

**访问修饰符图**

![image-20240418175027713](https://flydean-1301049335.cos.ap-guangzhou.myqcloud.com/img/202404181750296.png)

 

## 运算符

### &和&&的区别

&运算符有两种用法：(1)按位与；(2)逻辑与。

&&运算符是短路与运算。逻辑与跟短路与的差别是非常巨大的，虽然二者都要求运算符左右两端的布尔值都是true 整个表达式的值才是true。

&&之所以称为短路运算，是因为如果&&左边的表达式的值是 false，右边的表达式会被直接短路掉，不会进行运算。

## 关键字

### Java 有没有 goto

goto 是 Java 中的保留字，在目前版本的 Java 中没有使用。

### final 有什么用？

被ﬁnal修饰的类不可以被继承被ﬁnal修饰的方法不可以被重写

被ﬁnal修饰的变量不可以被改变，被ﬁnal修饰不可变的是变量的引用，而不是引用指向的内容， 引用指向的内容是可以改变的

### final finally finalize区别

ﬁnal可以修饰类、变量、方法，修饰类表示该类不能被继承、修饰方法表示该方法不能被重写、 修饰变量表示该变量是一个常量不能被重新赋值。

ﬁnally一般作用在try-catch代码块中，在处理异常的时候，通常我们将一定要执行的代码方法ﬁnally代码块中，表示不管是否出现异常，该代码块都会执行，一般用来存放一些关闭资源的代码。

ﬁnalize是一个方法，属于Object类的一个方法，而Object类是所有类的父类，该方法一般由垃圾回收器来调 用，当我们调用System.gc() 方法的时候，由垃圾回收器调用ﬁnalize()，回收垃圾，一个对象是否可回收的最后判断。

### this关键字的用法

this是自身的一个对象，代表对象本身，可以理解为：指向对象本身的一个指针。this的用法在java中大体可以分为3种：

1. 普通的直接引用，this相当于是指向当前对象本身。

2. 形参与成员名字重名，用this来区分：

```java
public Person(String name, int age){
  this.name = name;
  this.age =age;
}
```

3. 引用本类的构造函数

```java
 class Person{

private  String  name; private  int age;

public Person() {
}
public  Person(String  name)  { this.name  =  name;}
public  Person(String  name,  int  age)  { this(name);
this.age  =  age;
}
}
```

### super关键字的用法

super可以理解为是指向自己超（父）类对象的一个指针，而这个超类指的是离自己最近的一个父 类。

super也有三种用法： 

1.普通的直接引用

与this类似，super相当于是指向当前对象的父类的引用，这样就可以用super.xxx来引用父类的成员。

2.子类中的成员变量或方法与父类中的成员变量或方法同名时，用super进行区分

```java
class Person{
protected  String  name;

public  Person(String  name)  { this.name  =  name;
}

}

class Student extends Person{ private  String  name;

public  Student(String  name,  String  name1)  { super(name);
this.name  =  name1;
}
public  void  getInfo(){
System.out.println(this.name); System.out.println(super.name);
}
}

public  class  Test  {
public  static  void  main(String[]  args)  { Student  s1  =  new  Student("Father","Child"); s1.getInfo();

}
}

```

3. 引用父类构造函数

super（参数）：调用父类中的某一个构造函数（应该为构造函数中的第一条语句）。

this（参数）：调用本类中另一种形式的构造函数（应该为构造函数中的第一条语句）。

### this与super的区别

super: 它引用当前对象的直接父类中的成员用来访问直接父类中被隐藏的父类中成员数据或函数，基类与派生类中有相同成员定义时如：super.变量名  super.成员函数据名（实参） 

this：它代表当前对象名在程序中易产生二义性之处，应使用this来指明当前对象；如果函数的形参与类中的成员数据同名，这时需用this来指明成员变量名

super()和this()类似,区别是，super()在子类中调用父类的构造方法，this()在本类内调用本类的其它构造方法。

super()和this()均需放在构造方法内第一行。

尽管可以用this调用一个构造器，但却不能调用两个。

this和super不能同时出现在一个构造函数里面，因为this必然会调用其它的构造函数，其它的构造函数必然也会有super语句的存在，所以在同一个构造函数里面有相同的语句，就失去了语句的意义，编译器也不会通过。

this()和super()都指的是对象，所以，均不可以在static环境中使用。包括：static变量,static方法，static语句块。

从本质上讲，this是一个指向本对象的指针, 然而super是一个Java关键字。

### static存在的主要意义

static的主要意义是在于创建独立于具体对象的域变量或者方法。**以致于即使没有创建对象，也能 使用属性和调用方法**！

static关键字还有一个比较关键的作用就是**用来形成静态代码块以优化程序性能**。static块可以置于类中的任何地方，类中可以有多个static块。在类初次被加载的时候，会按照static块的顺序来执 行每个static块，并且只会执行一次。

为什么说static块可以用来优化程序性能，是因为它的特性:只会在类加载的时候执行一次。因此，很多时候会将一些只需要进行一次的初始化操作都放在static代码块中进行。

### static的独特之处

1、被static修饰的变量或者方法是独立于该类的任何对象，也就是说，这些变量和方法**不属于任 何一个实例对象，而是被类的实例对象所共享**。

>  怎么理解 “被类的实例对象所共享” 这句话呢？就是说，一个类的静态成员，它是属于大伙的【大伙指的是这个类的多个对象实例，我们都知道一个类可以创建多个实例！】，所有的类对象共享 的，不像成员变量是自个的【自个指的是这个类的单个实例对象】

2、在该类被第一次加载的时候，就会去加载被static修饰的部分，而且只在类第一次使用时加载 并进行初始化，注意这是第一次用就要初始化，后面根据需要是可以再次赋值的。

3、static变量值在类加载的时候分配空间，以后创建类对象的时候不会重新分配。赋值的话，是可以任意赋值的！

4、被static修饰的变量或者方法是优先于对象存在的，也就是说当一个类加载完毕之后，即便没有创建对象，也可以去访问。

### static应用场景

因为static是被类的实例对象所共享，因此如果**某个成员变量是被所有对象所共享的，那么这个成 员变量就应该定义为静态变量**。

因此比较常见的static应用场景有：

1、修饰成员变量 2、修饰成员方法 3、静态代码块 4、修饰类【只能修饰内部类也就是静态内部类】 5、静态导包

### static注意事项

1、静态只能访问静态。

2、非静态既可以访问非静态的，也可以访问静态的。

## 流程控制语句

### break ,continue ,return 的区别及作用

break 跳出总上一层循环，不再执行循环(结束当前的循环体)

continue 跳出本次循环，继续执行下次循环(结束正在执行的循环 进入下一个循环条件) 

return 程序返回，不再执行下面的代码(结束当前的方法 直接返回)

### 在 Java中，如何跳出当前的多重嵌套循环

在Java中，要想跳出多重循环，可以在外面的循环语句前定义一个标号，然后在里层循环体的代码中使用带有标号的break语句，即可跳出外层循环。例如：



```java
public  static  void  main(String[]  args)  { ok:
for  (int  i  =  0;  i  <  10;  i++)  {
	for  (int  j  =  0;  j  <  10;  j++)  {
  System.out.println("i="  +  i  +  ",j="  +  j); 
  if (j == 5) {
	break ok;
	}
}
}
}
```

 

 
