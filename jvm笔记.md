## 1.栈、堆

### 栈

栈的存取速度快，存放八种基本数据类型 （int, short, long, byte, float, double, boolean, char）和对象句柄，在函数中定义的一些**基本类型的变量(8种)和对象的引用变量**都是在函数的**栈Stack**内存中分配。

### 堆

一个jvm中只有一个堆内存，堆内存的大小是可以调节的

堆中存储实例对象。

类加载器读取了类文件之后，一般把什么东西放到堆中？

​        类的实例，里面的方法、常量、变量，保存引用对象的真实对象

1、所有通过new创建的对象的内存都存放到堆中。

2、堆内存分新生代，老年代。永恒代是方法区，不属于堆。对于Java8， HotSpots取消了永久代，那么是不是也就没有方法区了呢？当然不是，方法区是一个规范，规范没变，它就一直在。那么取代永久代的就是元空间。它可永久代有什么不同的？存储位置不同，永久代物理是是堆的一部分，和新生代，老年代地址是连续的，而元空间属于本地内存；存储内容不同，元空间存储类的元信息，静态变量和常量池等并入堆中。相当于永久代的数据被分到了堆和元空间中。

<img src="C:\Users\yyy\AppData\Roaming\Typora\typora-user-images\image-20210223150029029.png" alt="image-20210223150029029" style="zoom:50%;" />




![img](https://img2018.cnblogs.com/blog/1079203/201902/1079203-20190218210701409-339736142.png)

![img](https://img2018.cnblogs.com/blog/1079203/201902/1079203-20190218210722493-1485752892.png)

![img](https://img2018.cnblogs.com/blog/1079203/201902/1079203-20190218210741700-1061988394.png)

![img](https://img2018.cnblogs.com/blog/1079203/201902/1079203-20190218210757343-1435678281.png)

最后的永恒代，放常用库文件和方法。

Eden和survivor的比例为8：1，年轻代中的对象基本都是朝生夕死的(80%以上)，老年代比年轻代内存大。如果老年代内存满了，就会触发major GC或者full GC。触发full GC就会出现所谓的STW（stop the world）现象。即所有的进程都挂起等待清理垃圾。

major GC是回收老年代的垃圾。Full GC是回收老年代和年轻代的垃圾。

### 永久区

这个区是常驻内存的，用来存放jdk自身携带的class对象、interface元数据。存储Java运行的一些环境或类信息，这个区不存在垃圾回收。在关闭jvm虚拟机的时候会释放这个区域的内存。

- jdk1.6之前：叫永久代，常量池是在方法区
- jdk1.7        ：叫永久代，慢慢的退化了，要去永久代，常量池在堆
- jdk1.8之后：无永久代，常量池在元空间

## 2.类加载器、双亲委派机制

类加载器作用：加载class文件 - new Student(); 

![image-20210222133211351](C:\Users\yyy\AppData\Roaming\Typora\typora-user-images\image-20210222133211351.png)

### 什么是双亲委派机制

当某个类加载器需要加载某个`.class`文件时，它首先把这个任务委托给他的上级类加载器，递归这个操作，如果上级的类加载器没有加载，自己才会去加载这个类。

### 类加载器的类别

1.BootstrapClassLoader（启动类加载器）

`c++`编写，加载`java`核心库 `java.*`,构造`ExtClassLoader`和`AppClassLoader`。由于引导类加载器涉及到虚拟机本地实现细节，开发者无法直接获取到启动类加载器的引用，所以不允许直接通过引用进行操作

2.ExtClassLoader （标准扩展类加载器）

`java`编写，加载扩展库，如`classpath`中的`jre` ，`javax.*`或者
 `java.ext.dir` 指定位置中的类，开发者可以直接使用标准扩展类加载器。

3.AppClassLoader（系统类加载器）

java编写，加载程序所在的目录，如user.dir所在的位置的class

4.CustomClassLoader（用户自定义类加载器）

`java`编写,用户自定义的类加载器,可加载指定路径的`class`文件

<img src="https://upload-images.jianshu.io/upload_images/7634245-7b7882e1f4ea5d7d.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp" alt="img" style="zoom:67%;" />

### 双亲委派机制的作用

1、防止重复加载同一个`.class`。通过委托去向上面问一问，加载过了，就不用再加载一遍。保证数据安全。
 2、保证核心`.class`不能被篡改。通过委托方式，不会去篡改核心`.class`，即使篡改也不会去加载，即使加载也不会是同一个`.class`对象了。不同的加载器加载同一个`.class`也不是同一个`Class`对象。这样保证了`Class`执行安全。



### **为什么要设计这种机制**

这种设计有个好处是，如果有人想替换系统级别的类：String.java。篡改它的实现，但是在这种机制下这些系统的类已经被Bootstrap classLoader加载过了，所以并不会再去加载，从一定程度上防止了危险代码的植入。

## 3.沙箱安全机制

（不算特别重点）

### 什么是沙箱？

  Java安全模型的核心就是Java沙箱（sandbox），什么是沙箱？沙箱是一个限制程序运行的环境。沙箱机制就是将 Java 代码限定在虚拟机(JVM)特定的运行范围中，并且严格限制代码对本地系统资源访问，通过这样的措施来保证对代码的有效隔离，防止对本地系统造成破坏。沙箱**主要限制系统资源访问**，那系统资源包括什么？——`CPU、内存、文件系统、网络`。不同级别的沙箱对这些资源访问的限制也可以不一样。

### 组成沙箱的基本组件：

- `字节码校验器`（bytecode verifier）：确保Java类文件遵循Java语言规范。这样可以帮助Java程序实现内存保护。但并不是所有的类文件都会经过字节码校验，比如核心类。
- `类装载器`（class loader）：其中类装载器在3个方面对Java沙箱起作用
  - 它防止恶意代码去干涉善意的代码；
  - 它守护了被信任的类库边界；
  - 它将代码归入保护域，确定了代码可以进行哪些操作。

  虚拟机为不同的类加载器载入的类提供不同的命名空间，命名空间由一系列唯一的名称组成，每一个被装载的类将有一个名字，这个命名空间是由Java虚拟机为每一个类装载器维护的，它们互相之间甚至不可见。

  类装载器采用的机制是双亲委派模式。

1. 从最内层JVM自带类加载器开始加载，外层恶意同名类得不到加载从而无法使用；
2. 由于严格通过包来区分了访问域，外层恶意的类通过内置代码也无法获得权限访问到内层类，破坏代码就自然无法生效。

- `存取控制器`（access controller）：存取控制器可以控制核心API对操作系统的存取权限，而这个控制的策略设定，可以由用户指定。
- `安全管理器`（security manager）：是核心API和操作系统之间的主要接口。实现权限控制，比存取控制器优先级高。
- `安全软件包`（security package）：java.security下的类和扩展包下的类，允许用户为自己的应用增加新的安全特性，包括：
  - 安全提供者
  - 消息摘要
  - 数字签名
  - 加密
  - 鉴别

## 3.native关键字

凡是带了 native关键字的，说明Java的作用范围达不到了，会去调用底层C语言的库。

会进入本地方法栈

调用本地方法接口JNI

JNI的作用：扩展Java的使用，融合不同的编程语言为Java所用

Java诞生的时候，C/C++横行，必须要能够调用C/C++，它在内存中专门开辟了一块标记区域：Native Method Stack登记native方法

在最终执行的时候，通过JNI加载本地方法库中的方法

## 4.方法区

![JVM 内存初学 (堆(heap)、栈(stack)和方法区(method) )](http://static.open-open.com/lib/uploadImg/20150521/20150521171913_332.bmp)

JAVA的JVM的内存可分为3个区：堆(heap)、栈(stack)和方法区(method)

堆区:
1.存储的全部是对象，每个对象都包含一个与之对应的class的信息。(class的目的是得到操作指令)
2.jvm只有一个堆区(heap)被所有线程共享，堆中不存放基本类型和对象引用，只存放对象本身
栈区:
1.每个线程包含一个栈区，栈中只保存基础数据类型的对象和自定义对象的引用(不是对象)，对象都存放在堆区中
2.每个栈中的数据(原始类型和对象引用)都是私有的，其他栈不能访问。
3.栈分为3个部分：基本类型变量区、执行环境上下文、操作指令区(存放操作指令)。
方法区（static final Class 常量池）:
1.又叫静态区，跟堆一样，被所有的线程共享。方法区包含所有的class和static变量。
2.方法区中包含的都是在整个程序中永远唯一的元素，如class，static变量。

## 5.GC

jvm在进行GC时，并不是对这三个区域统一回收。大部分时候，回收都是新生代

- 新生代
- 幸存区（from,to)
- 老年区

GC两种类型

- 轻GC（普通的GC）
- 重GC（全局GC）

GC题目：

- jvm的内存模型和分区，详细到每个区放什么？
- 堆里面的分区有哪些？Eden,from,to,老年区，说说他们的特点
- GC的清除算法有哪些？标记清楚法、标记压缩、复制算法、引用计数器，怎么用的？
- 轻GC和重GC分别在什么时候发生？

GC算法

- 复制算法
- 标记清除法
- 标记压缩算法

内存效率：复制算法>标记清除法>标记压缩算法

内存整齐度：复制算法=标记压缩算法>标记清除法

内存利用率：标记压缩算法=标记清除法>复制算法