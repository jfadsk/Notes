## 1.初始JVM

### 1.1jvm是什么

	JVM是Java Virtual Machine（Java虚拟机）的缩写，JVM是一种用于计算设备的规范，它是一个虚构出来的计算机，是通过在实际的计算机上仿真模拟各种计算机功能来实现的。引入Java语言虚拟机后，Java语言在不同平台上运行时不需要重新编译。Java语言使用Java虚拟机屏蔽了与具体平台相关的信息，使得Java语言编译程序只需生成在Java虚拟机上运行的目标代码（字节码），就可以在多种平台上不加修改地运行。
![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-10-15_18-40-36-2022-10-1518:40:56.png)

JVM并不是只为Java语言服务，而是针对**字节码文件，**只要是字节码文件，JVM就支持。

![](https://gitee.com/xie-qianyu/picture/raw/master/4a59b61884e7443f9d16ad5ad36e98bc-2022-10-1518:45:22.png)

 像java语言自不必说，还有大数据开发常用的Scala语言，Groovy语言，python等其他语言经过处理也可以转换成字节码文件，从而在JVM环境中运行。

### 1.2虚拟机

​	虚拟机就是一台虚拟的计算机，可以执行一系列的虚拟计算机命令。虚拟机分为两类：**系统虚拟机**和**程序虚拟机**。

​	系统虚拟机：VMware这些，就是对物理计算机的仿真，提供了一个可运行的完整操作系统的软件平台。

​	程序虚拟机：典型就是java虚拟机，他是专门为**执行单个计算机程序而设计**的在java虚拟机中执行的指令我们称之为java字节码指令。

### 1.3java虚拟机

​	java虚拟机就是一台执行java字节码文件的虚拟计算机，他拥有独立的运行机制，运行的java字节码文件也未必就是java语言编译而成的。

​	JVM平台的各种语言可以共享java虚拟机带来的**跨平台性**，优秀的垃圾回收器，以及可靠的**即时编辑器**。

​	java技术的核心就是java虚拟机。所有的java程序都运行在java虚拟机中。

**作用：**java虚拟机就是二进制字节码的运行环境，负责装载字节码到其内部，解释/编译为对应平台上的机器指令执行。每一条java指令，java虚拟机规范中都有详细的定义，如：怎么取操作数、怎么处理操作数，处理结果放在哪里。

**特点**:

​	1.一次编译，到处运行

​	2.自动内存管理

​	3.自动垃圾回收功能

### 1.4 JVM架构模型

​	java编译器输入的指令流基本上是一种**基于栈的指令集架构**，另外一种指令集架构则是**基于寄存器的指令集架构**。

#### 	1.4.1 基于栈式的架构特点：

​		-> 设计和实现更简单，适用于资源受限的系统。

​		-> 避开了寄存器的分配难题：使用零地址指令分配。

​		-> 指令流中的指令大部分是零地址指令，其执行过程依赖于操作栈。指令集更小，编译器容易实现。

​		-> 不需要硬件支持，可移植性更好，更好实现跨平台。

#### 1.4.2 基于寄存器架构的特点：

​		-> 典型的应用实X86的二进制指令集：比如传统的PC以及Android的Davlik虚拟机。

​		**-> 指令集架构则完全依赖于硬件，可移植性较差。**

​		**-> 性能优秀和执行更加的高效。**

​		->话费更少的指令去完成一项工作。

​		-> 在大部分情况下,基于**寄存器架构的指令集**往往都是以**一地址指令，二地址指令和三地址指令**为主，而基于**栈式架构的指令集**却是以**零地址**为主。

​	**PS**： **什么叫做零地址指令**

​		在执行指令的时候有两个值  一个是**地址**一个是**操作数**，一个地址是**一地址指令**，相应的还有二地址指令，三地址指令。而**零地址**则是在执行指令时，只需要**操作数**，不要**地址**了,应为栈的操作，只需要看重操作数，而下面的**指令**或者**操作数**，在当前下，是不需要考虑的。

​	![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-10-15_20-15-15-2022-10-1520:29:21.png)

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-10-15_20-27-28-2022-10-1520:30:21.png)

#### 1.4.3 总结：

​		**由于跨平台的设计，java指令都是根据栈来设计的**。不同平台CPU架构不同，所以不能设计为基于寄存器的。优点是跨平台，指令集小，编译器容易实现，缺点是性能下降，实现同样的功能需要更多的指令。

​	**栈：**跨平台性, 指令集小，指令多。执行性能比 寄存器差。

### 1.5 JVM的生命周期

#### 1.5.1 虚拟机的启动

​			Java虚拟机的启动是通过引导类加载器(bootstrap class loader)创建一个初始类(initial class)来完成的，这个类是由虚拟机的具体实现指定的。

#### 1.5.2 虚拟机的执行

​		**>**	一个运行中的Java虚拟机有着一个清晰的任务：执行Java程序。

​		**>**	程序开始执行时他才运行，程序结束时他就停止。
​		**>**	执行一个所谓的Java程序的时候，真真正正在执行的是一个叫做**Java虚拟机的进程。**

#### 1.5.3 虚拟机的退出

​		有以下几中情况：

```java
1.程序正常执行结束
2.程序在执行过程中遇到了异常或错误而异常终止
3.由于操作系统出现错误而导致java虚拟机进程终止
4.某线程调用Runtime类或者System类的exit方法，或者Runtime类的halt方法，并且java安全管理器也允许这次exit或者halt操作。
5.除此之外，JNT(Java Native Interface) 规范描述了用JNT Invocation API 来加载或
卸载 java虚拟机时， java虚拟机的退出情况。
```

### 1.6解释器和及时编译器（JIT）

#### 1.6.1解释器工作机制

​		1.解释器真正意义上所承担的角色就是一个运行时“翻译者”，将字节码文件中的内容“翻译”为对应平台的本地机器指令执行。

​		2.当一条字节码指令被解释执行完成后，接着再根据PC寄存器中记录的下一条需要被执行的字节码指令执行解释操作。

#####  1.6.1.1现状

​		1.由于解释器在设计和实现上非常简单，因此除了Java语言之外，还有许多高级语言同样也是基于解释器执行的，比如Python、Perl、Ruby等。
​		2.但是在今天，基于解释器执行已经沦落为低效的代名词，并且时常被一些C/C+ +程序员所调侃。
​		3.为了解决这个问题，JVM平台支持一种叫作即时编译的技术。即时编译的目的是避免函数被解释执行，而是将整个函数体编译成为机器码，每次函数执行时，只执行编译后的机器码即可，这种方式可以使执行效率大幅度提升。

#### 1.6.2 及时编译器（JIT）

​		HotSpotVM是目前市面上高性能虚拟机的代表作之一。它采用解释器与即时编译器并存的架构。在Java虚拟机运行时，解释器和即时编译器能够相互协作，各自取长补短，尽力去选择最合适的方式来权衡编译本地代码的时间和直接解释执行代码的时间。

​	![](https://gitee.com/xie-qianyu/picture/raw/master/44cad0d04c2e401797e073b81180f855-2022-10-1817:59:25.png)

##### 1.6.2.1 问题：有了及时编译器为什么还需要解释器

​	![](https://gitee.com/xie-qianyu/picture/raw/master/50fb547fd4a7481bbdd0ecac7e35ad2e-2022-10-1817:59:32.png)

##### 1.6.2.2 HotSpot虚拟机的执行方式（热点代码探测技术）

当虚拟机启动的时候，解释器可以首先发挥作用，而不必等待即时编译器全部编
译完成再执行，这样可以省去许多不必要的编译时间。并且随着程序运行时间的
推移，即时编译器逐渐发挥作用，根据热点探测功能，将有价值的字节码编译为
本地机器指令，以换取更高的程序执行效率。

​		1.通过计数器找到最具编译价值的代码，触发及时编译或栈上替换。

​		2.通过编译器与解释器协同工作，在最优化的程序响应时间与最佳执行性能中取得平衡。

## 2.类加载器子系统

### 2.1内存构造

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-10-18_17-56-00-2022-10-1817:59:42.png)

​	

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-10-18_17-56-51-2022-10-1817:59:44.png)

如果自己想写一个java虚拟机的话 ， 需要实现**类加载器**和**执行引擎**

### 2.2类加载器

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-10-18_18-04-44-2022-10-1818:04:52.png)

#### 2.2.1 作用

  1. 类加载器子系统负责从文件系统或者网络中加载class 文件，class文件在文件开头有特定的文件标识。

  2. ClassLoader 只负责class文件的加载，至于它是否可以运行，则由ExecutionEngine决定，

  3. 加载的类信息存放于一块称为方法区的内存空间，除了类的信息外，方法区中还会存放运行时常量池信息，可能还包括字符串字面量和数字常量（这部分常量是Class文件中常量池部分的内存映射）

     ##### 2.2.1.1类加载器ClassLoader的角色

     ![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-10-18_18-23-57-2022-10-1818:24:14.png)

###  2.3加载过程

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-10-18_18-27-22-2022-10-1818:27:30.png)

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-10-18_18-32-04-2022-10-1818:32:32.png)

#### 2.3.1类加载过程Loading加载阶段

​	  **加载：**

​	1. 通过一个类的全限定名获取定义此类的二进制字节流

			2. 将这个字节流所代表的静态存储结构转化为方法区的运行时数据结构
			2. 在内存中生成一个代表这个类的java.lang.class对象，作为方法区这个类的各种数据的访问入口。

####  2.3.2类加载过程Linking链接阶段

##### 	2.3.2.1 验证（Verify）

*  目的在于确保class文件的字节流中包含的信息符合当前虚拟机要求，保证被加载类的正确性，不会危害虚拟机自身的危害。

* 主要包含四种验证： 文件格式验证 ， 元数据验证 ， 字节码验证 ， 符号引用验证。

  ![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-10-24_10-23-17-2022-10-2410:23:35.png)

  ​	java 虚拟机解读 **CA FE BA BE** 。确保符合虚拟机的要求.

##### 2.3.2.2 准备（Prepare）

* 为类变量分配内存并且设置该类 的默认初始值，即零值。
* 这里不包含用**final修饰的static**，因为final在编译的时候就会分配了，准备阶段会显示初始化；
* **这里不会实例变量分配初始化**，类变量会分配在方法区中，而实例变量是会随着对象一起分配到**java堆**中。

##### 2.3.2.3 解析（Resolve）

* 将常量池内的符号引用转换为直接引用的过程，‘
* 事实上，解析操作往往会伴随着JVM在执行玩初始化之后在执行。
* 符号引用及时一组符号来描述所用用的目标 ， 符号引用的字面量形式明确定义在《java 虚拟机规范》的class文件格式中，直接引用就是直接指向目标的指针，相对偏移量或一个间接定位到目标的句柄。
* 解析动作主要针对类或接口，字段，类方法，接口方法，方法类型等。对用常量池中的CONSTANT_Class_info , CONSTANT_Fieldref_info , CONSTANT_Methodref_info 等。

#### 2.3.3类加载过程Initialization初始化阶段

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-10-24_10-42-08-2022-10-2410:42:25.png)

初始化阶段就是执行类构造器法（）的过程。

此方法不需定义，是javac编译器自动收集类中的所有类变量的赋值动作和静态代码块中的语句合并而来。

- 也就是说，当我们代码中包含static变量的时候，就会有clinit方法

构造器方法中指令按语句在源文件中出现的顺序执行。

（）不同于类的构造器。（关联：构造器是虚拟机视角下的（））若该类具有父类，JVM会保证子类的（）执行前，父类的（）已经执行完毕。

- 任何一个类在声明后，都有生成一个构造器，默认是空参构造器

```
public class ClassInitTest {
    private static int num = 1;
    static {
        num = 2;
        number = 20;
        System.out.println(num);
        System.out.println(number);  //报错，非法的前向引用
    }

    private static int number = 10;

    public static void main(String[] args) {
        System.out.println(ClassInitTest.num); // 2
        System.out.println(ClassInitTest.number); // 10
    }
}
```

关于涉及到父类时候的变量赋值过程

```
public class ClinitTest1 {
    static class Father {
        public static int A = 1;
        static {
            A = 2;
        }
    }

    static class Son extends Father {
        public static int b = A;
    }

    public static void main(String[] args) {
        System.out.println(Son.b);
    }
}
```

我们输出结果为 2，也就是说首先加载ClinitTest1的时候，会找到main方法，然后执行Son的初始化，但是Son继承了Father，因此还需要执行Father的初始化，同时将A赋值为2。我们通过反编译得到Father的加载过程，首先我们看到原来的值被赋值成1，然后又被复制成2，最后返回

```
iconst_1
putstatic #2 <com/atguigu/java/chapter02/ClinitTest1$Father.A>
iconst_2
putstatic #2 <com/atguigu/java/chapter02/ClinitTest1$Father.A>
return
```

虚拟机必须保证一个类的（）方法在多线程下被同步加锁。

```
public class DeadThreadTest {
    public static void main(String[] args) {
        new Thread(() -> {
            System.out.println(Thread.currentThread().getName() + "\t 线程t1开始");
            new DeadThread();
        }, "t1").start();

        new Thread(() -> {
            System.out.println(Thread.currentThread().getName() + "\t 线程t2开始");
            new DeadThread();
        }, "t2").start();
    }
}
class DeadThread {
    static {
        if (true) {
            System.out.println(Thread.currentThread().getName() + "\t 初始化当前类");
            while(true) {

            }
        }
    }
}
```

上面的代码，输出结果为

```
线程t1开始
线程t2开始
线程t2 初始化当前类
```

从上面可以看出初始化后，只能够执行一次初始化，这也就是同步加锁的过程

### 2.4 类加载器的分类

JVM支持两种类型的类加载器 。分别为引导类加载器（Bootstrap ClassLoader）和自定义类加载器（User-Defined ClassLoader）。

从概念上来讲，自定义类加载器一般指的是程序中由开发人员自定义的一类类加载器，但是Java虚拟机规范却没有这么定义，而是将所有派生于抽象类ClassLoader的类加载器都划分为自定义类加载器。

无论类加载器的类型如何划分，在程序中我们最常见的类加载器始终只有3个，如下所示：

![](https://gitee.com/xie-qianyu/picture/raw/master/image-20200705094149223-2022-10-2416:26:25.png)

这里的四者之间是包含关系，不是上层和下层，也不是子系统的继承关系。

我们通过一个类，获取它不同的加载器

```java
public class ClassLoaderTest {
    public static void main(String[] args) {
        // 获取系统类加载器
        ClassLoader systemClassLoader = ClassLoader.getSystemClassLoader();
        System.out.println(systemClassLoader);

        // 获取其上层的：扩展类加载器
        ClassLoader extClassLoader = systemClassLoader.getParent();
        System.out.println(extClassLoader);

        // 试图获取 根加载器
        ClassLoader bootstrapClassLoader = extClassLoader.getParent();
        System.out.println(bootstrapClassLoader);

        // 获取自定义加载器
        ClassLoader classLoader = ClassLoaderTest.class.getClassLoader();
        System.out.println(classLoader);
        
        // 获取String类型的加载器
        ClassLoader classLoader1 = String.class.getClassLoader();
        System.out.println(classLoader1);
    }
}
```

得到的结果，从结果可以看出 根加载器无法直接通过代码获取，同时目前用户代码所使用的加载器为系统类加载器。同时我们通过获取String类型的加载器，发现是null，那么说明String类型是通过根加载器进行加载的，也就是说Java的核心类库都是使用根加载器进行加载的。

```
sun.misc.Launcher$AppClassLoader@18b4aac2
sun.misc.Launcher$ExtClassLoader@1540e19d
null
sun.misc.Launcher$AppClassLoader@18b4aac2
null 
```

#### 2.4.1启动类加载器（引导类加载器，Bootstrap ClassLoader）

* 这个类加载使用c/c++语言实现的，嵌套在JVM内部
* 它用来加载java的核心库（JAVAHOME/jre/1ib/rt.jar、resources.jar或sun.boot.class.path路径下的内容），用于提供JVM自身需要的类。
* 并不继承自Java.lang.ClassLoader，没有父加载器
* 加载扩展类和应用程序类加载器，并指定为他们的父类加载器。
* 处于安全的考虑，Bootstrap启动类加载器只加载包名为java，， Javax ， sun 等开头的类。

#### 2.4.2扩展类加载器（Extension ClassLoader）

* Java语言编写，由sun.misc.Launcher$ExtClassLoader实现。
* 派生于ClassLoader类
* 父类加载器为启动类加载器
* 从java.ext.dirs系统属性做置顶的目录中加载类库，或从JDK的安装目录的jre/lib/ext字目录（扩展目录）下加载类库。如果用户创建的JAR放在此目录下，也会自动由扩展类加载器加载。

#### 2.4.3  应用程序类加载器（系统类加载器，AppClassLoader）

- javI语言编写，由sun.misc.LaunchersAppClassLoader实现
- 派生于ClassLoader类
- 父类加载器为扩展类加载器
- 它负责加载环境变量classpath或系统属性java.class.path指定路径下的类库
- 该类加载是程序中默认的类加载器，一般来说，Java应用的类都是由它来完成加载
- 通过classLoader#getSystemclassLoader（）方法可以获取到该类加载器

#### 2.4.4用户自定义加载器

在java的日常应用程序开发中，类的加载几乎是由上述3中类加载器相互配合执行的，在必要时，我们可以自定义加载器，来定制类的加载方式。为什么要自定义类加载器？

* 隔离加载类
* 修改类加载的方式
* 扩展加载源
* 防止源码泄露

用户自定义类加载器实现步骤：

* 开发人员可以通过继承抽象类ava.1ang.ClassLoader类的方式，实现自己的类加载器，以满足一些特殊的需求
* 在JDK1.2之前，在自定义类加载器时，总会去继承ClassLoader类并重写loadClass（）方法，从而实现自定义的类加载类，但是在JDK1.2之后已不再建议用户去覆盖loadclass（）方法，而是建议把自定义的类加载逻辑写在findclass（）方法中
* 在编写自定义类加载器时，如果没有太过于复杂的需求，可以直接继承URIClassLoader类，这样就可以避免自己去编写findclass（）方法及其获取字节码流的方式，使自定义类加载器编写更加简洁。

#### 2.4.5查看根加载器所能加载的目录

刚刚我们通过概念了解到了，根加载器只能够加载 java /lib目录下的class，我们通过下面代码验证一下

```java
public class ClassLoaderTest1 {
    public static void main(String[] args) {
        System.out.println("*********启动类加载器************");
        // 获取BootstrapClassLoader 能够加载的API的路径
        URL[] urls = sun.misc.Launcher.getBootstrapClassPath().getURLs();
        for (URL url : urls) {
            System.out.println(url.toExternalForm());
        }

        // 从上面路径中，随意选择一个类，来看看他的类加载器是什么：得到的是null，说明是  根加载器
        ClassLoader classLoader = Provider.class.getClassLoader();
    }
}
```

得到的结果：

```
*********启动类加载器************
file:/E:/Software/JDK1.8/Java/jre/lib/resources.jar
file:/E:/Software/JDK1.8/Java/jre/lib/rt.jar
file:/E:/Software/JDK1.8/Java/jre/lib/sunrsasign.jar
file:/E:/Software/JDK1.8/Java/jre/lib/jsse.jar
file:/E:/Software/JDK1.8/Java/jre/lib/jce.jar
file:/E:/Software/JDK1.8/Java/jre/lib/charsets.jar
file:/E:/Software/JDK1.8/Java/jre/lib/jfr.jar
file:/E:/Software/JDK1.8/Java/jre/classes
null
```

#### 2.4.6关于ClassLoader

ClassLoader类，它是一个抽象类，其后所有的类加载器都继承自ClassLoader**（不包括启动类加载器）**

![image-20200705103516138](https://gitee.com/xie-qianyu/picture/raw/master/image-20200705103516138-2022-10-2417:12:26.png)

sun.misc.Launcher 它是一个java虚拟机的入口应用

![](https://gitee.com/xie-qianyu/picture/raw/master/image-20200705103636003-2022-10-2417:12:55.png)

获取ClassLoader的途径

- 获取当前ClassLoader：clazz.getClassLoader()
- 获取当前线程上下文的ClassLoader：Thread.currentThread().getContextClassLoader()
- 获取系统的ClassLoader：ClassLoader.getSystemClassLoader()
- 获取调用者的ClassLoader：DriverManager.getCallerClassLoader()

### 2.5 双亲委派机制

java虚拟机对class文件采用的是按需加载的方式，也就是说当需要使用该类是才会将它的class文件加载到内存中生成class对象。而且加载某个类的class文件时，java虚拟机采用的是**双亲委派模式**，即把请求交由父类处理，他是一种任务委派模式。

#### 2.5.1工作原理

* 如果一个类加载器收到了类加载请求，他并不会自己先去加载，而是把这个请求委托给父类的加载器去执行。
* 如果父类加载器还存在其父类加载器，则进一步向上委托，依次递归，请求最终将到达最顶层的启动类加载器。
* 如果父类加载器可以完成类加载任务，就成功返回，倘若父类加载器无法完成此加载任务，子加载器才会尝试自己去加载，这就是双亲委派机制。

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-10-24_17-49-01-2022-10-2417:49:25.png)

#### 2.5.2双亲委派机制举例

当我们加载jdbc.jar 用于实现数据库连接的时候，首先我们需要知道的是 jdbc.jar是基于SPI接口进行实现的，所以在加载的时候，会进行双亲委派，最终从根加载器中加载 SPI核心类，然后在加载SPI接口类，接着在进行反向委派，通过线程上下文类加载器进行实现类 jdbc.jar的加载。

![](https://gitee.com/xie-qianyu/picture/raw/master/image-20200705105810107-2022-10-2418:00:25.png)

#### 2.5.3沙箱安全机制

自定义string类，但是在加载自定义String类的时候会率先使用引导类加载器加载，而引导类加载器在加载的过程中会先加载jdk自带的文件（rt.jar包中java\lang\String.class），报错信息说没有main方法，就是因为加载的是rt.jar包中的string类，该类中是没有main方法的。这样可以保证对java核心源代码的保护，这就是沙箱安全机制。

#### 2.5.4双亲委派机制的优势

* 避免类的重复加载
* 保护程序的安全，防止核心API被随意篡改

​		✓ 自定义类：java.lang.String

​		✓ 自定义类：java.lang.XqyStart （报错：阻止创建 java.lang开头的类）



###  2.6其他

#### 2.6.1判断两个class对象是否相同

* 在JVM表示两个class对象是否为同一个类，存在两个必要条件：

​        ⇒  类的完整类名必须一致,包括包名.

​		⇒  加载这个类的ClassLoader(指ClassLoader的实例对象)必须相同。

* 换句话说，在JVM中，即使这两个类对象（class对象）来源于同一个class文件，被同一个虚拟机所加载，但是只要加载它们的ClassLoader实例对象不同，那么这两个类对象也是不相等的。

JVM必须知道一个类型是由启动加载器加载的还是由用户类加载器加载的。如果一个类型是由用户类加载器加载的，那么JVM会将这个类加载器的一个引用作为类型信息的一部分保存在方法区中。当解析一个类型到另一个类型的引用的时候，JVM需要保证这两个类型的类加载器是相同的。



#### 2.6.2 类的主动使用和被动使用

Java程序对类的使用方式分为：主动使用和被动使用。 

​	主动使用，又分为七种情况：

* 创建类的实例
* 访问某个类或者接口的静态变量，或者对该静态变量赋值。
* 调用类的静态方法
* 反射（比如：Class.forName("com.xqy.Test") ）
* 初始化一个类的子类
* Java虚拟机启动时被标明为启动类
* JDK 7 开始提供的动态语言支持：

​		java.lang.incoke.MethodHandle 实例的解析结果

​		REF getStatic、REF putStatic、REF invokeStatic 句柄对应的类没有初始化，则初始化。

​	

  **©**  除了以上的7中情况，其他适用Java类的方式都被看做是对类的被动使用，都不会导致类的初始化。



## 3.运行时数据区概述及线程

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-10-24_18-43-14-2022-10-2418:43:25.png)

​		当我们通过前面的：类的加载-> 验证 -> 准备 -> 解析 -> 初始化 这几个阶段完成后，就会用到执行引擎对我们的类进行使用，同时执行引擎将会使用到我们运行时数据区。

​	![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-10-24_18-45-39-2022-10-2418:46:25.png)

也就是大厨做饭，我们把大厨后面的东西（切好的菜，刀，调料），比作是运行时数据区。而厨师可以类比于执行引擎，将通过准备的东西进行制作成精美的菜品

![](https://gitee.com/xie-qianyu/picture/raw/master/image-20200705112036630-2022-10-2418:48:25.png)

### 3.1内存

​	内存是非常重要的系统资源，是硬盘和CPU的中间仓库及桥梁，承载着操作系统和应用程序的实时运行JVM内存布局规定了Java在运行过程中内存申请、分配、管理的策略，保证了JVM的高效稳定运行。不同的JVM对于内存的划分方式和管理机制存在着部分差异。结合JVM虚拟机规范，来探讨一下经典的JVM内存布局。

```文本
我们通过磁盘或者网络IO得到的数据，都需要先加载到内存中，然后CPU从内存中获取数据进行读取，也就是说内存充当了CPU和磁盘之间的桥梁
```

### 3.2  线程

**运行时数据区完整图**

![](https://gitee.com/xie-qianyu/picture/raw/master/image-20200705112416101-2022-10-2516:13:19.png)

Java 虚拟机定义类若干种程序运行期间会使用到的运行时数据区，其中有一些会随着虚拟机启动而创建，随着虚拟机退出而销毁，另外一些则是与线程一一对应的，这些与线程对应的数据 区域会随着线程开始和结束而创建和销毁。

**灰色的为单独线程私有的，红色的为多个线程共享的**。即:

* 每个线程：独立包括程序计数器，栈，本地方法栈。
* 线程间共享：堆，堆外内存（永久代或元空间，代码缓存）。

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-10-25_16-25-35-2022-10-2516:26:05.png)

**概念：**

线程是一个程序里的运行单元。JVM允许一个应用有多个线程并行的执行。 在Hotspot JVM里，每个线程都与操作系统的本地线程直接映射。

- 当一个Java线程准备好执行以后，此时一个操作系统的本地线程也同时创建。Java线程执行终止后，本地线程也会回收。

操作系统负责所有线程的安排调度到任何一个可用的CPU上。一旦本地线程初始化成功，它就会调用Java线程中的run（）方法。

### 3.3 JVM系统线程

如果你使用Jconsole或者是任何一个调试工具，都能看到在后台有许多线程在运行。这些后台线程不包括调用public static void main（String[]）的main线程以及所有这个main线程自己创建的线程.

⇒ 这些主要的后台系统线程在Hotspot JVM里主要是以下几个：

- 虚拟机线程：这种线程的操作是需要JVM达到安全点才会出现。这些操作必须在不同的线程中发生的原因是他们都需要JVM达到安全点，这样堆才不会变化。这种线程的执行类型包括"stop-the-world"的垃圾收集，线程栈收集，线程挂起以及偏向锁撤销。
- 周期任务线程：这种线程是时间周期事件的体现（比如中断），他们一般用于周期性操作的调度执行。
- GC线程：这种线程对在JVM里不同种类的垃圾收集行为提供了支持。
- 编译线程：这种线程在运行时会将字节码编译成到本地代码。
- 信号调度线程：这种线程接收信号并发送给JVM，在它内部通过调用适当的方法进行处理。

## 4.程序计数器（PC寄存器）

### 4.1介绍

JVM中的程序计数寄存器（Program Counter Register）中，Register的命名源于CPU的寄存器，寄存器存储指令相关的现场信息。CPU只有把数据装载到寄存器才能够运行。这里，并非是广义上所指的物理寄存器，或许将其翻译为PC计数器（或指令计数器）会更加贴切（也称为程序钩子），并且也不容易引起一些不必要的误会。**JVM中的PC寄存器是对物理PC寄存器的一种抽象模拟。**

![](https://gitee.com/xie-qianyu/picture/raw/master/image-20200705155551919-2022-10-2516:49:05.png)

它是一块很小的内存空间，几乎可以忽略不记。也是运行速度最快的存储区域。

在JVM规范中，每个线程都有它自己的程序计数器，是线程私有的，生命周期与线程的生命周期保持一致。

任何时间一个线程都只有一个方法在执行，也就是所谓的当前方法。程序计数器会存储当前线程正在执行的Java方法的JVM指令地址；或者，如果是在执行native方法，则是未指定值（undefned）。

它是程序控制流的指示器，分支、循环、跳转、异常处理、线程恢复等基础功能都需要依赖这个计数器来完成。字节码解释器工作时就是通过改变这个计数器的值来选取下一条需要执行的字节码指令。

它是唯一一个在Java虚拟机规范中没有规定任何outotMemoryError情况的区域。也没有GC。

### 4.2作用

**PC寄存器 用来存储指向下一条指令的地址。也即将要执行的指令代码。由执行引擎读取下一条指令。**

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-10-25_16-58-38-2022-10-2516:58:57.png)

然后将代码进行编译成字节码文件，我们再次查看 ，发现在字节码的左边有一个行号标识，它其实就是指令地址，用于指向当前执行到哪里。

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-10-15_20-27-28-2022-10-2517:03:19.png)

通过PC寄存器，我们就可以知道当前程序执行到哪一步了

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-10-25_17-07-06-2022-10-2517:08:05.png)

### 4.3两个问题

#### 4.3.1  使用PC寄存器存储字节码指令地址有什么用呢？

* 为什么使用PC寄存器记录当前线程的执行地址呐？

**答：** 因为CPU需要不停地切换各个线程，这时候切换回来以后，就得知道接着从哪开始接续执行。

JVM的字节码解释器就需要通过改变PC寄存器的值来明确下一条应该执行什么样的字节码指令。

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-10-25_17-46-06-2022-10-2517:47:05.png)

#### 4.3.2 PC寄存器为什么会被设定为线程私有？

**答：** 我们都知道所谓的多线程在一个特定的时间段内只会执行其中某一个线程的方法，CPU会不停地做任务切换，这样必然导致经常中断或者恢复。如何保证分毫无差那？**为了能够准确的记录各个线程正在执行的当前字节码指令地址，最好的方法自然是为每个线程都分配一个PC寄存器。** 这样以来各个线程之间便可以进行独立计算，从而不会出现相互干扰的情况。

由于cpu时间片轮的限制，众多线程在并发执行过程中，任何一个确定的时刻，一个处理器或者多核处理器中的一个内核，只会执行某个线程的一条指令。

这样必然导致经常中断或恢复，如何保证分毫无差呐?  每个线程在创建后 ， 都会产生自己的程序计数器和栈帧 ， 程序计数器在各个线程之间互不影响。

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-10-25_18-04-28-2022-10-2518:05:05.png)

### 4.4CPU时间片

CPU时间片即CPU分配给各个程序的时间，每个线程被分配一个时间段 ， 被称作它的时间片。

在宏观上：我们可以同时打开多个应用程序，每个程序并行不悖 ， 同时运行。

但在微观上： 由于只有一个CPU，一次只能处理程序要求的一部分，如何处理公平，一种方法就是引入时间片 ， 每个程序轮流执行。

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-10-25_18-11-13-2022-10-2518:12:05.png)

**串行：** 某个时间段内挨着一个一个排队来执行。

**并行：** 多核CPU同时执行多个线程任务。

**并发：** 一个CPU同时执行多个任务 ， 各个线程抢夺CPU的时间片 ， 在各个线程间来回切换。



**并行是一个时刻有多个线程执行，而并发是指某时间段内有多个线程执行**

## 5.虚拟机栈

### 5.1 虚拟机栈概述

由于跨平台性的设计，Java的指令都是根据栈来设计的。不同平台CPU架构不同，所以不能设计为基于寄存器的。 **优点是跨平台，指令集小，编译器容易实现，缺点是性能下降，实现同样的功能需要更多的指令。**

有不少Java开发人员一提到Java内存结构，就会非常粗粒度地将JVM中的内存区理解为仅有Java堆（heap）和 Java栈（stack）？为什么？

**首先栈是运行时的单位 ， 而堆是存储的单位。**

**即：** **栈**解决程序的运行问题 ， 即程序如何执行，或者说如何处理数据 。

​		**堆**解决的是数据存储问题 ， 即数据怎么放 ， 放在哪儿。

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-10-26_19-20-05-2022-10-2619:20:16.png)

#### 5.1.1 Java虚拟机栈是什么

Java虚拟机栈（Java Virtual Machine Stack），早期也叫做java栈，每个线程在创建是都会创建一个虚拟机栈，其内存保存一个个的栈帧（Stack Frame），对应这一次次的java方法调用。

**是线程私有的**

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-10-26_19-25-54-2022-10-2619:26:09.png)

#### 5.1.2 生命周期

生命周期和线程一致，也就是线程结束了 ， 该虚拟机栈也就销毁了。



#### 5.1.3 作用

主管java程序的运行，他保存方法的局部变量 ，部分结果 ， 并参与方法的调用和返回，

⇒ 局部变量： 他是相比于成员变量来说的（或者属性）

⇒ 基本数据变量： 相较于引用类型变量（类 ， 数组 ， 接口）



#### 5.1.4 栈的特点

栈是一种快速有效的分配存储方式 ， 访问速度仅次于程序计数器。 JVM直接对java栈的操作只有两个：

* 每个方法执行，伴随着进栈（入栈 ，压栈）。
* 执行结束后的出栈操**作**

**对于栈来说不存在垃圾回收问题（GC）但是栈存在溢出问题（OOM）。**

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-10-26_19-38-23-2022-10-2619:39:09.png)

####  5.1.5 开发中栈遇到的常见异常

java虚拟机规范 允许java栈的大小是动态的或者是固定不变的。

如果采用固定大小的java虚拟机栈，那每一个线程的java虚拟机栈容量可以在线程创建的时候独立选定。如果线程请求分配的栈容量超过Java虚拟机栈允许的最大容量，Java虚拟机将会抛出一个StackoverflowError 异常。

如果Java虚拟机栈可以动态扩展，并且在尝试扩展的时候无法申请到足够的内存，或者在创建新的线程时没有足够的内存去创建对应的虚拟机栈，那Java虚拟机将会抛出一个 outofMemoryError 异常。

```java
public class StackErrorTest {
    private static int count = 1;
    public static void main(String[] args) {
        System.out.println(count++);
        main(args);
    }
}
```

#### 5.1.6 设置栈内存大小

我们可以使用参数 -Xss选项来设置线程的最大栈空间，栈的大小直接决定了函数调用的最大可达深度

```java
-Xss1m
-Xss1k
```

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-10-26_19-55-17-2022-10-2619:58:09.png)

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-10-26_19-55-46-2022-10-2619:59:07.png)

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-10-26_19-56-05-2022-10-2619:59:08.png)

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-10-26_19-56-31-2022-10-2619:59:09.png)



### 5.2 栈的存储单位

#### 5.2.1 栈中存储什么？

每个线程都有自己的栈，栈中的数据都是以栈帧（Stack Frame）的格式存在。在这个线程上正在执行的每个方法都各自对应一个栈颜（Stack Frame）。栈帧是一个内存区块，是一个数据集，维系着方法执行过程中的各种数据信息。

```java
OOP的基本概念：类和对象

类中基本结构：field（属性、字段、域）、method
```

JVM直接对Java栈的操作只有两个，就是对栈帧的**压栈**和**出栈**，遵循**“先进后出”/“后进先出”**原则。

在一条活动线程中，**一个时间点上，只会有一个活动的栈帧**。即只有当前正在执行的方法的栈帧（栈顶栈帧）是有效的，这个栈帧被称为当前栈帧（Current Frame），与当前栈帧相对应的方法就是当前方法（Current Method），定义这个方法的类就是当前类（Current Class）。

**执行引擎运行的所有字节码指令只针对当前栈帧进行操作**。

如果在该方法中调用了其他方法，对应的新的栈帧会被创建出来，放在栈的顶端，成为新的当前帧。

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-10-26_20-09-26-2022-10-2620:10:09.png)

```java
public class StackFrameTest {
    public static void main(String[] args) {
        method01();
    }

    private static int method01() {
        System.out.println("方法1的开始");
        int i = method02();
        System.out.println("方法1的结束");
        return i;
    }

    private static int method02() {
        System.out.println("方法2的开始");
        int i = method03();;
        System.out.println("方法2的结束");
        return i;
    }
    private static int method03() {
        System.out.println("方法3的开始");
        int i = 30;
        System.out.println("方法3的结束");
        return i;
    }
}
```

```java
方法1的开始
方法2的开始
方法3的开始
方法3的结束
方法2的结束
方法1的结束
```

满足栈先进后出的概念，通过Idea的 DEBUG，能够看到栈信息

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-10-26_20-18-36-2022-10-2620:19:09.png)

#### 5.2.2 栈运行原理

不同线程中所包含的栈帧是不允许存在相互引用的，即不可能在一个栈帧之中引用另外一个线程的栈帧。

如果当前方法调用了其他方法，方法返回之际，当前栈帧会传回此方法的执行结果给前一个栈帧，接着，虚拟机会丢弃当前栈帧，使得前一个栈帧重新成为当前栈帧。

Java方法有两种返回函数的方式：

* 一种是正常的函数返回，使用return指令；
* 另外一种是抛出异常。不管使用哪种方式，都会导致栈帧被弹出。

#### 5.2.3 栈帧的内部结构

每个栈帧中存储着：

- 局部变量表（Local Variables）
- 操作数栈（operand Stack）（或表达式栈）
- 动态链接（DynamicLinking）（或指向运行时常量池的方法引用）
- 方法返回地址（Return Address）（或方法正常退出或者异常退出的定义）
- 一些附加信息

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-10-26_20-36-30-2022-10-2620:37:09.png)

并行每个线程下的栈都是私有的，因此每个线程都有自己各自的栈，并且每个栈里面都有很多栈帧,**栈帧的数量取决与栈帧的大小，栈帧的大小主要取决于局部变量表 和 操作数栈的大小**

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-10-26_20-36-59-2022-10-2620:38:09.png)



### 5.3 局部变量表

局部变量表：Local Variables，被称之为**局部变量数组**或**本地变量表**

**定义为一个数字数组，主要用于存储方法参数和定义在方法体内的局部变量**这些数据类型包括各类基本数据类型、对象引用（reference），以及returnAddress类型。

由于局部变量表是建立在线程的栈上，是线程的私有数据，因此**不存在数据安全问题**

**局部变量表所需的容量大小是在编译期确定下来的，**并保存在方法的Code属性的maximum local variables数据项中。在方法运行期间是不会改变局部变量表的大小的。

**方法嵌套调用的次数由栈的大小决定**。一般来说，**栈越大，方法嵌套调用次数越多**。对一个函数而言，它的参数和局部变量越多，使得局部变量表膨胀，它的栈帧就越大，以满足方法调用所需传递的信息增大的需求。进而函数调用就会占用更多的栈空间，导致其嵌套调用次数就会减少。

**局部变量表中的变量只在当前方法调用中有效。**在方法执行时，虚拟机通过使用局部变量表完成参数值到参数变量列表的传递过程。**当方法调用结束后，随着方法栈帧的销毁，局部变量表也会随之销毁**

#### 5.3.1 关于Slot的理解

参数值的存放总是在局部变量数组的index0 开始 ， 到数组长度减1的索引结束。

局部变量表，**最基本的存储单元是Slot（变量槽）**局部变量表中存放编译期可知的各种基本数据类型（8种），引用类型（reference），returnAddress类型的变量。

在局部变量表里，**32位以内的类型只占用一个slot（包括returnAddress类型），64位的类型（1ong和double）占用两个slot。**

> byte、short、char 在存储前被转换为int，boolean也被转换为int，0表示false，非0表示true。 1ong和double则占据两个slot。

JVM会为局部变量表中的每一个Slot都分配一个访问索引，通过这个索引即可成功访问到局部变量表中指定的局部变量值

当一个实例方法被调用的时候，它的方法参数和方法体内部定义的局部变量将会**按照顺序**被复制到局部变量表中的每一个slot上

**如果需要访问局部变量表中一个64bit的局部变量值时，只需要使用前一个索引即可**。（比如：访问1ong或doub1e类型变量）

如果当前帧是由构造方法或者实例方法创建的，那么**该对象引用this将会存放在index为0的slot处**，其余的参数按照参数表顺序继续排列。

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-10-29_16-13-40-2022-10-2916:14:19.png)

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-10-29_15-50-41-2022-10-2915:51:01.png)

#### 5.3.2 Slot的重复利用

栈帧中的局部变量表中的槽位是可以重用的，如果一个局部变量过了其作用域，那么在其作用域之后申明的新的局部变就很有可能会复用过期局部变量的槽位，从而达到节省资源的目的。

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-10-29_16-25-45-2022-10-2916:26:19.png)

#### 5.3.3 静态变量与局部变量的对比

变量的分类：

- 按数据类型分：基本数据类型、引用数据类型
- 按类中声明的位置分：成员变量（类变量，实例变量）、局部变量
  - 类变量：linking的paper阶段，给类变量默认赋值，initial阶段给类变量显示赋值即静态代码块
  - 实例变量：随着对象创建，会在堆空间中分配实例变量空间，并进行默认赋值
  - 局部变量：在使用前必须进行显式赋值，不然编译不通过。

参数表分配完毕之后，再根据方法体内定义的变量的顺序和作用域分配。

我们知道类变量表有两次初始化的机会，第一次是在“准备阶段”，执行系统初始化，对类变量设置零值，另一次则是在“初始化”阶段，赋予程序员在代码中定义的初始值。

和类变量初始化不同的是，局部变量表不存在系统初始化的过程，这意味着一旦定义了局部变量则必须人为的初始化，否则无法使用。

在栈帧中，与性能调优关系最为密切的部分就是前面提到的局部变量表。在方法执行时，虚拟机使用局部变量表完成方法的传递。

**局部变量表中的变量也是重要的垃圾回收根节点，只要被局部变量表中直接或间接引用的对象都不会被回收。**



### 5.4 操作数栈

#### 5.4.1概念

操作数栈：Operand Stack

每一个独立的栈帧除了包含局部变量表以外，还包含一个后进先出（Last - In - First -Out）的 **操作数栈**，也可以称之为 **表达式栈**（Expression Stack）

**操作数栈，在方法执行过程中，根据字节码指令，往栈中写入数据或提取数据，即入栈（push）和 出栈（pop）**

- 某些字节码指令将值压入操作数栈，其余的字节码指令将操作数取出栈。使用它们后再把结果压入栈
- 比如：执行复制、交换、求和等操作

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-10-29_18-05-38-2022-10-2918:06:19.png)

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-10-29_18-09-22-2022-10-2918:10:19.png)

操作数栈，**主要用于保存计算过程的中间结果，同时作为计算过程中变量临时的存储空间**。

操作数栈就是JVM执行引擎的一个工作区，当一个方法刚开始执行的时候，一个新的栈帧也会随之被创建出来，**这个方法的操作数栈是空的。.**

> 这个时候数组是有长度的，因为数组一旦创建，那么就是不可变的

每一个操作数栈都会拥有一个明确的栈深度用于存储数值，其所需的最大深度在编译期就定义好了，保存在方法的Code属性中，为maxstack的值。

栈中的任何一个元素都是可以任意的Java数据类型

- 32bit的类型占用一个栈单位深度
- 64bit的类型占用两个栈单位深度

操作数栈**并非采用访问索引的方式来进行数据访问**的，而是只能通过标准的入栈和出栈操作来完成一次数据访问

**如果被调用的方法带有返回值的话，其返回值将会被压入当前栈帧的操作数栈中**，并更新PC寄存器中下一条需要执行的字节码指令。

操作数栈中元素的数据类型必须与字节码指令的序列严格匹配，这由编译器在编译器期间进行验证，同时在类加载过程中的类检验阶段的数据流分析阶段要再次验证。|

另外，我们说Java虚拟机的**解释引擎是基于栈的执行引擎**，其中的栈指的就是操作数栈。

#### 5.4.2代码追踪

我们给定代码

```java
public void testAddOperation() {
    byte i = 15;
    int j = 8;
    int k = i + j;
}
```

使用javap 命令反编译class文件： javap -v 类名.class

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-10-29_18-32-24-2022-10-2918:33:19.png)

> byte、short、char、boolean 内部都是使用int型来进行保存的
>
> 从上面的代码我们可以知道，我们都是通过bipush对操作数 15 和 8进行入栈操作
>
> 同时使用的是 iadd方法进行相加操作，i -> 代表的就是 int，也就是int类型的加法操作

执行流程如下所示：

首先执行第一条语句，PC寄存器指向的是0，也就是指令地址为0，然后使用bipush让操作数15入栈。

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-10-29_18-32-50-2022-10-2918:33:25.png)

执行完后，让PC + 1，指向下一行代码，下一行代码就是将操作数栈的元素存储到局部变量表1的位置，我们可以看到局部变量表的已经增加了一个元素

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-10-29_18-33-13-2022-10-2918:33:26.png)

> 为什么局部变量表不是从0开始的呢？
>
> 其实局部变量表也是从0开始的，但是因为0号位置存储的是this指针，所以说就直接省略了~

然后PC+1，指向的是下一行。让操作数8也入栈，同时执行istore操作，存入局部变量表中

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-10-29_18-33-43-2022-10-2918:34:44.png)

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-10-29_18-33-49-2022-10-2918:34:50.png)

然后从局部变量表中，依次将数据放在操作数栈中然后从局部变量表中，依次将数据放在操作数栈中

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-10-29_18-34-01-2022-10-2918:35:08.png)

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-10-29_18-34-08-2022-10-2918:35:16.png)

然后将操作数栈中的两个元素执行相加操作，并存储在局部变量表3的位置

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-10-29_18-34-15-2022-10-2918:35:35.png)

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-10-29_18-34-22-2022-10-2918:35:42.png)

最后PC寄存器的位置指向10，也就是return方法，则直接退出方法

------



### 5.5 栈顶缓存技术

栈顶缓存技术：Top Of Stack Cashing

前面提过，基于栈式架构的虚拟机所使用的零地址指令更加紧凑，但完成一项操作的时候必然需要使用更多的入栈和出栈指令，这同时也就意味着将需要更多的指令分派（instruction dispatch）次数和内存读/写次数。

由于操作数是存储在内存中的，因此频繁地执行内存读/写操作必然会影响执行速度。为了解决这个问题，HotSpot JVM的设计者们提出了栈顶缓存（Tos，Top-of-Stack Cashing）技术，**将栈顶元素全部缓存在物理CPU的寄存器中，以此降低对内存的读/写次数，提升执行引擎的执行效率。**

> 寄存器：指令更少，执行速度快

------



### 5.6 动态链接（或指向运行时常量池的方法引用）

动态链接：Dynamic Linking

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-10-29_19-20-10-2022-10-2919:20:19.png)

> 动态链接、方法返回地址、附加信息 ： 有些地方被称为帧数据区

每一个栈帧内部都包含一个指向**运行时常量池**中**该栈帧所属方法的引用**包含这个引用的目的就是为了支持当前方法的代码能够实现**动态链接（Dynamic Linking）**。比如：invokedynamic指令

在Java源文件被编译到字节码文件中时，所有的变量和方法引用都作为符号引用（symbolic Reference）保存在class文件的常量池里。

比如：描述一个方法调用了另外的其他方法时，就是通过常量池中指向方法的符号引用来表示的，**那么动态链接的作用就是为了将这些符号引用转换为调用方法的直接引用**。

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-10-29_19-20-49-2022-10-2919:21:19.png)

* 为什么需要运行时常量池？

* 因为在不同的方法，都可能调用常量或者方法，所以只需要存储一份即可，节省了空间

* 常量池的作用：就是为了提供一些符号和常量，便于指令的识别

### 5.7 方法的调用

**在JVM中，将符号引用转换为调用方法的直接引用与方法的绑定机制相关**

#### 5.7.1 链接

##### 5.7.1.1 静态链接

当一个字节码文件被装载进JVM内部时，如果被调用的**目标方法在编译期可知**，且运行期保持不变时，这种情况下降调用方法的符号引用转换为直接引用的过程称之为静态链接

##### 5.7.1.2 动态链接

如果**被调用的方法在编译期无法被确定下来**，也就是说，只能够在程序运行期将调用的方法的符号转换为直接引用，由于这种引用转换过程具备动态性，因此也被称之为动态链接。

#### 5.7.2 绑定机制

对应的方法的绑定机制为：早期绑定（Early Binding）和晚期绑定（Late Binding）。**绑定是一个字段、方法或者类在符号引用被替换为直接引用的过程，这仅仅发生一次。**

##### 5.7.2.1 早期绑定

早期绑定就是指被调用的**目标方法如果在编译期可知，且运行期保持不变时**，即可将这个方法与所属的类型进行绑定，这样一来，由于明确了被调用的目标方法究竟是哪一个，因此也就可以使用静态链接的方式将符号引用转换为直接引用。

##### 5.7.2.2 晚期绑定

如果**被调用的方法在编译期无法被确定下来，只能够在程序运行期根据实际的类型绑定相关的方法**，这种绑定方式也就被称之为晚期绑定。

------

```java
1.使用private或static或final修饰的变量或者方法，使用静态链接早期绑定。而虚方法（可以被子类重写的方法）则会根据运行时的对象进行动态链接晚期绑定。
2.重载（Overload）的方法是用静态链接早期绑定绑定完成，而重写（Override）的方法则使用动态链接晚期绑定完成。
```

##### 5.7.2.3 发展历史

随着高级语言的横空出世，类似于Java一样的基于面向对象的编程语言如今越来越多，尽管这类编程语言在语法风格上存在一定的差别，但是它们彼此之间始终保持着一个共性，那就是都支持封装、继承和多态等面向对象特性，既然**这一类的编程语言具备多态特性，那么自然也就具备早期绑定和晚期绑定两种绑定方式。**

Java中任何一个普通的方法其实都具备虚函数的特征，它们相当于C++语言中的虚函数（C++中则需要使用关键字virtual来显式定义）。如果在Java程序中不希望某个方法拥有虚函数的特征时，则可以使用关键字final来标记这个方法。

#### 5.7.3 虚方法和非虚方法

* 如果方法在编译期就确定了具体的调用版本 ， 这个版本在运行时是不可变的。这个方法成为**非虚方法**。
* 静态方法 ，私有方法 ， final方法 ， 实例构造器 ，(super.)父类方法都是非虚方法。
* **其他方法称为虚方法**。

> 子类对象的多态的使用前提
>
> - 类的继承关系
> - 方法的重写

虚拟机中提供了以下几条方法调用指令：

##### 普通调用指令：

- invokestatic：调用静态方法，解析阶段确定唯一方法版本
- invokespecial：调用<init>方法、私有及父类方法，解析阶段确定唯一方法版本
- invokevirtual：调用所有虚方法
- invokeinterface：调用接口方法

##### 动态调用指令：

- invokedynamic：动态解析出需要调用的方法，然后执行

前四条指令固化在虚拟机内部，方法的调用执行不可人为干预，而invokedynamic指令则支持由用户确定方法版本。其中invokestatic指令和invokespecial指令调用的方法称为非虚方法，其余的（fina1修饰的除外）称为虚方法。

##### invokednamic指令

JVM字节码指令集一直比较稳定，一直到Java7中才增加了一个invokedynamic指令，**这是Java为了实现动态类型语言】支持而做的一种改进。**

但是在Java7中并没有提供直接生成invokedynamic指令的方法，需要借助ASM这种底层字节码工具来产生invokedynamic指令。**直到Java8的Lambda表达式的出现，invokedynamic指令的生成，在Java中才有了直接的生成方式。**

Java7中增加的动态语言类型支持的本质是对Java虚拟机规范的修改，而不是对Java语言规则的修改，这一块相对来讲比较复杂，增加了虚拟机中的方法调用，最直接的受益者就是运行在Java平台的动态语言的编译器。

#### 5.7.4 动态类型语言和静态类型语言

动态类型语言和静态类型语言两者的区别就在于对类型的检查是在编译期还是在运行期，满足前者就是静态类型语言，反之是动态类型语言。

说的再直白一点就是，**静态类型语言是判断变量自身的类型信息；动态类型语言是判断变量值的类型信息，变量没有类型信息，变量值才有类型信息，这是动态语言的一个重要特征。**

> Java：String info = "mogu blog"; (Java是静态类型语言的，会先编译就进行类型检查)
>
> JS：var name = "shkstart"; var name = 10; （运行时才进行检查）

#### 5.7.5 方法重写的本质

1. 找到操作数栈顶的第一个元素所执行的对象的实际类型 ，记作 C。
2. 如果在类型C 中找到与常量中的描述符合简单名称的方法 ， 则进行访问权限校验 ， 如果通过返回这个方法的直接引用 ，查找过程结束 ， 则返回java.lang.IllegalAccessError 异常。
3. 否则  ， 按照继承关系从下往上依次执行对C的各个父类进行第二步的搜索和验证过程 。 
4. 如果始终没有找到合适的方法  ，则抛出java.lang.AbstractMethodsrror异常。

**IllegalAccessError介绍：**

程序视图访问或修改一个属性或调用一个放啊发 ， 这个属性或方法 ， 你没有权限方法 ， 一般的  ， 这个会引起编译器异常 。 这个错误如果发生在运行时 ， 就说明一个类发生了不兼容的改变。

#### 5.7.6 虚方法表

* 在面向对象的编程中， 会很频繁的使用到动态分派 ， 如果在每次动态分派的过程中都要宠你更新在类的方法元数据中 搜索合适的目标的话就可能影响到执行效率 。 因此 ， **为了提高性能。** JVM 采用在类的方法区建立一个虚方法表（virtual method table） （非虚方法不会出现在表中） 来实现 。 **使用索引表来代替查找**。

* 每个类中都有一个虚方法表 ， 表中存放着各个方法的实际入口。

* 那么虚方法表什么时候被创建那？

  虚方法表会在类加载的链接阶段被创建并开始初始化 ， 类的变量初始值准备完成之后 ，JVM会把该类的方法表也初始化完毕。

  ![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-11-02_19-35-19-2022-11-219:35:31.png)



### 5.8 方法返回地址(return address)

* 方法返回地址中存放调用该方法的PC寄存器的值。**（也就是该方法如果正常返回之后，代码从上一个方法的哪里开始执行）**
* 一个方法的结束，有两种方式：
  * 正常执行退出
  * 出现未处理的异常，非正常退出
* 无论通过那种方式退出，在方法退出之后都返回到该方法被调用的位置 。方法正常退出时 ，**调用者的PC计数器的值作为放回地址，即调用该方法的指令的下一条指令的地址** ，而通过异常退出的 ， 返回地址是要通过异常表来确定，栈帧中一般不会保存这部分信息。

当一个方法开始执行后，只有两种方式可以退出这个方法：

执行引擎遇到任意一个方法返回的字节码指令（return），会有返回值传递给上层的方法调用者**，简称正常完成出口；**

- 一个方法在正常调用完成之后，究竟需要使用哪一个返回指令，还需要根据方法返回值的实际数据类型而定。
- 在字节码指令中，返回指令包含ireturn（当返回值是boolean，byte，char，short和int类型时使用），lreturn（Long类型），freturn（Float类型），dreturn（Double类型），areturn。另外还有一个return指令声明为void的方法，实例初始化方法，类和接口的初始化方法使用。

在方法执行过程中遇到异常（Exception），并且这个异常没有在方法内进行处理，也就是只要在本方法的异常表中没有搜索到匹配的异常处理器，就会导致方法退出，**简称异常完成出口**。

方法执行过程中，抛出异常时的异常处理，存储在一个异常处理表，方便在发生异常的时候找到处理异常的代码

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-11-02_20-00-14-2022-11-220:00:47.png)

本质上，方法的退出就是当前栈帧出栈的过程。此时，需要恢复上层方法的局部变量表、操作数栈、将返回值压入调用者栈帧的操作数栈、设置PC寄存器值等，让调用者方法继续执行下去。

**正常完成出口和异常完成出口的区别在于：通过异常完成出口退出的不会给他的上层调用者产生任何的返回值。**

------

### 5.9 一些附加信息

栈帧中还允许携带与Java虚拟机实现相关的一些附加信息 ， 例如：对程序调试提供支持的信息。

### 5.10 栈的相关面试题

##### 1.举例栈溢出的情况（StackOverFlowError？

* 通过-Xss设置栈的大小。

##### 2.调整栈大小 ， 就能保证不出现溢出吗？

* 不能保证不溢出

##### 3.分配的栈内存越大越好吗？

* 不是，虽然在一定时间内降低了OOM的概率，但是这会挤占其他线程的空间，因为整个空间是有限的。

##### 4.垃圾回收是否会涉及到虚拟机栈？

* 不会

##### 5.方法中定义的局部变量是否线程安全？

* 具体问题具体分析。

```java
/**
 * 面试题
 * 方法中定义局部变量是否线程安全？具体情况具体分析
 * 何为线程安全？
 *    如果只有一个线程才可以操作此数据，则必是线程安全的
 *    如果有多个线程操作，则此数据是共享数据，如果不考虑共享机制，则为线程不安全
 */
public class StringBuilderTest {

    // s1的声明方式是线程安全的
    public static void method01() {
        // 线程内部创建的，属于局部变量
        StringBuilder s1 = new StringBuilder();
        s1.append("a");
        s1.append("b");
    }

    // 这个也是线程不安全的，因为有返回值，有可能被其它的程序所调用
    public static StringBuilder method04() {
        StringBuilder stringBuilder = new StringBuilder();
        stringBuilder.append("a");
        stringBuilder.append("b");
        return stringBuilder;
    }

    // stringBuilder 是线程不安全的，操作的是共享数据
    public static void method02(StringBuilder stringBuilder) {
        stringBuilder.append("a");
        stringBuilder.append("b");
    }


    /**
     * 同时并发的执行，会出现线程不安全的问题
     */
    public static void method03() {
        StringBuilder stringBuilder = new StringBuilder();
        new Thread(() -> {
            stringBuilder.append("a");
            stringBuilder.append("b");
        }, "t1").start();

        method02(stringBuilder);
    }

    // StringBuilder是线程安全的，但是String也可能线程不安全的
    public static String method05() {
        StringBuilder stringBuilder = new StringBuilder();
        stringBuilder.append("a");
        stringBuilder.append("b");
        return stringBuilder.toString();
    }
}
```

总结一句话就是：如果对象是在内部产生，并在内部消亡，没有返回到外部，那么它就是线程安全的，反之则是线程不安全的。

##### 6.运行时数据区，是否存在Error和GC？

| 运行时数据区 | 是否存在Error | 是否存在GC |
| :----------- | ------------- | ---------- |
| 程序计数器   | 否            | 否         |
| 虚拟机栈     | 是            | 否         |
| 本地方法栈   | 是            | 否         |
| 方法区       | 是（OOM）     | 是         |
| 堆           | 是            |            |

------

## 6.本地方法接口

### 6.1 什么是本地方法

简单地讲，一个Native Methodt是一个Java调用非Java代码的接囗。一个Native Method是这样一个Java方法：该方法的实现由非Java语言实现，比如C。这个特征并非Java所特有，很多其它的编程语言都有这一机制，比如在C++中，你可以用extern "c" 告知c++编译器去调用一个c的函数。

"A native method is a Java method whose implementation is provided by non-java code."（本地方法是一个非Java的方法，它的具体实现是非Java代码的实现）

在定义一个native method时，并不提供实现体（有些像定义一个Java interface），因为其实现体是由非java语言在外面实现的。

本地接口的作用是融合不同的编程语言为Java所用，它的初衷是融合C/C++程序。

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-11-05_13-45-07-2022-11-513:45:18.png)

代码举例说明Native方法是如何编写的

```java
public class IhaveNatives {
    public native void Native1(int x);
    native static public long Native2();
    native synchronized private float Native3(Object o);
    native void Natives(int[] ary) throws Exception;
}
```

> 需要注意的是：标识符native可以与其它java标识符连用，但是abstract除外

### 6.2 为什么使用Native Method

Java使用起来非常方便，然而有些层次的任务用Java实现起来不容易，或者我们对程序的效率很在意时，问题就来了。

#### 6.2.1与java环境的交互

**有时Java应用需要与Java外面的环境交互，这是本地方法存在的主要原因**。你可以想想Java需要与一些底层系统，如操作系统或某些硬件交换信息时的情况。本地方法正是这样一种交流机制：它为我们提供了一个非常简洁的接口，而且我们无需去了解Java应用之外的繁琐的细节。

#### 6.2.2 与操作系统的交互

JVM支持着Java语言本身和运行时库，它是Java程序赖以生存的平台，它由一个解释器（解释字节码）和一些连接到本地代码的库组成。然而不管怎样，它毕竟不是一个完整的系统，它经常依赖于一底层系统的支持。这些底层系统常常是强大的操作系统。**通过使用本地方法，我们得以用Java实现了jre的与底层系统的交互，甚至JVM的一些部分就是用c写的**。还有，如果我们要使用一些Java语言本身没有提供封装的操作系统的特性时，我们也需要使用本地方法。

#### 6.2.3 Sun·s Java

**Sun的解释器是用C实现的，这使得它能像一些普通的C一样与外部交互。**jre大部分是用Java实现的，它也通过一些本地方法与外界交互。例如：类java.lang.Thread的setpriority（）方法是用Java实现的，但是它实现调用的是该类里的本地方法setpriorityo（）。这个本地方法是用C实现的，并被植入JVM内部，在Windows 95的平台上，这个本地方法最终将调用Win32 setpriority（）ApI。这是一个本地方法的具体实现由JVM直接提供，更多的情况是本地方法由外部的动态链接库（external dynamic link library）提供，然后被JVw调用。

### 6.3 现状

**目前该方法使用的越来越少了，除非是与硬件有关的应用**，比如通过Java程序驱动打印机或者Java系统管理生产设备，在企业级应用中已经比较少见。因为现在的异构领域间的通信很发达，比如可以使用Socket通信，也可以使用Web Service等等，不多做介绍。

------

## 7.本地方法栈（C栈）

**java虚拟机用于管理java方法的调用 ， 而本地方法栈用去管理本地方法的调用。**

**本地方法栈，也是线程私有的。**

允许被实现成固定或者是可动态扩展的内存大小。（在内存溢出方面是相同的）

- 如果线程请求分配的栈容量超过本地方法栈允许的最大容量，Java虚拟机将会抛出一个stackoverflowError 异常。
- 如果本地方法栈可以动态扩展，并且在尝试扩展的时候无法申请到足够的内存，或者在创建新的线程时没有足够的内存去创建对应的本地方法栈，那么Java虚拟机将会抛出一个outofMemoryError异常。

本地方法是使用C语言实现的。

它的具体做法是Native Method Stack中登记native方法，在Execution Engine 执行时加载本地方法库。

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-11-05_14-22-17-2022-11-514:22:38.png)

**当某个线程调用一个本地方法时，它就进入了一个全新的并且不再受虚拟机限制的世界。它和虚拟机拥有同样的权限。**

- 本地方法可以通过本地方法接口来访问虚拟机内部的运行时数据区。
- 它甚至可以直接使用本地处理器中的寄存器
- 直接从本地内存的堆中分配任意数量的内存。

**并不是所有的JVM都支持本地方法。因为Java虚拟机规范并没有明确要求本地方法栈的使用语言、具体实现方式、数据结构等。**如果JVM产品不打算支持native方法，也可以无需实现本地方法栈。

在Hotspot JVM中，直接将本地方法栈和虚拟机栈合二为一。

------



## 8.栈

### 8.1 堆的核心概述

**堆针对一个JVM进程来说是唯一的，也就是一个进程只有一个JVM，但是进程包含多个线程，他们是共享同一堆空间的**

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-11-05_14-50-59-2022-11-514:51:38.png)

一个JVM实例只存在一个堆内存，堆也是Java内存管理的核心区域。

Java堆区在JVM启动的时候即被创建，其空间大小也就确定了。是JVM管理的最大一块内存空间。

* 堆内存的大小是可以调节的。

《Java虚拟机规范》规定，堆可以处于**物理上不连续**的内存空间中，但在**逻辑上**它应该被视为**连续**的。

所有的线程共享Java堆，在这里还可以划分线程私有的缓冲区（Thread Local Allocation Buffer，TLAB）。

> -Xms10m：最小堆内存
>
> -Xmx10m：最大堆内存

下图就是使用：Java VisualVM查看堆空间的内容，通过 jdk bin提供的插件

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-11-05_15-11-56-2022-11-515:12:38.png)

《Java虚拟机规范》中对Java堆的描述是：所有的对象实例以及数组都应当在运行时分配在堆上。（The heap is the run-time data area from which memory for all class instances and arrays is allocated）

我要说的是：“几乎”所有的对象实例都在这里分配内存。—从实际使用角度看的。

- 因为还有一些对象是在栈上分配的

数组和对象可能永远不会存储在栈上，因为栈帧中保存引用，这个引用指向对象或者数组在堆中的位置。

在方法结束后，堆中的对象不会马上被移除，仅仅在垃圾收集的时候才会被移除。

- 也就是触发了GC的时候，才会进行回收
- 如果堆中对象马上被回收，那么用户线程就会收到影响，因为有stop the word

堆，是GC（Garbage Collection，垃圾收集器）执行垃圾回收的重点区域。

![](https://gitee.com/xie-qianyu/picture/raw/master/Snipaste_2022-11-05_16-13-30-2022-11-516:14:38.png)

-/9999
