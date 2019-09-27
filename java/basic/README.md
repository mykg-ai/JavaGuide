入门直接移步[菜鸟教程 - Java](https://www.runoob.com/java/java-tutorial.html)

# 目录
- [Java的特点]()
- [JVM、JRE、JDK]()
- [封装、继承、多态]()
- [重写、重载]()
- [基础数据类型]()
- [线程&进程]()
- [修饰符/关键字]()
- [接口和抽象类]()
- [序列化]()
- [String、StringBuffer、StringBuilder]()
- [垃圾回收机制]()
- [锁]()
- [泛型]()
- [异常]()
- []()


## 1. Java的特点

- 平台无关性：JVM可以在大部分平台运行
- 安全可靠：Java是强语言类型，严格要求变量的数据类型；取消了危险的指针(指针可以直接操作内存，可能导致程序崩溃)，增加引用类型的概念代替指针；复杂的异常处理机制
- 面向对象程序设计(Object Oriented Programming)：封装、继承、多态
- 开源
- 多线程
- 既是编译型语言也是解释型语言：java代码都需要编译为.class的二进制文件。.class文件又是解释运行在JVM中的

> 编译型语言是在程序运行之前将程序编译为机器语言，如C、C++
解释型语言在程序运行时才翻译为机器语言，如javascript
前者执行速度快，后者跨平台性好

## 1. JVM、JRE、JDK

整体来看就是JVM<JRE<JDK
- JVM：Java Virtual Machine 运行Java字节码(.class->机器可执行的二进制机器码)的虚拟机
- JRE：Java Running Environment 是java运行环境
- JDK：Java Development Kit，除了JRE还包括编译工具javac、文档工具javadoc、调试工具jdb等

java程序从源代码到运行的步骤：
![](/imgs/java程序运行过程.jpg)

## 1. 封装、继承、多态

封装就是隐藏对象的属性和实现细节，仅对外提供接口(方法)来控制内部属性的读改。封装的目的是增强安全性和简化编程。
```
public class Person {
  private int age;

  public int getAge() {
    return this.age;
  }
}
```

继承就是子类继承父类的特征和行为。Java类(class)的继承是单继承，接口(interface)是多继承
```
public class Animal {}
public class Cat extends Animal {}
```

多态就是同一个接口，使用不同的实例而执行不同操作。
```
abstract class Animal {  
  abstract void eat();  
}
class Cat extends Animal {  
  public void eat() {  
    System.out.println("吃鱼");  
  }  
}
class Dog extends Animal {  
  public void eat() {  
    System.out.println("吃骨头");  
  }
}
```

## 1. 重写、重载

重写Override体现在子类重新编写父类的方法。
```
class Animal{
  public void move(){
    System.out.println("动物可以移动");
  }
}
class Dog extends Animal{
  public void move(){
    System.out.println("狗可以跑和走");
  }
}
```

重载Overload是在一个类里面，方法名字相同，而参数不同。返回类型可以相同也可以不同。
```
public class Overloading {
  public int test(){
    System.out.println("test1");
    return 1;
  }

  public void test(int a) {
    System.out.println("test2");
  }
}

# 或者体现在构造方法
public class Puppy{
  public Puppy() {}
  public Puppy(String name) {}
}
```

## 1. 基础数据类型

数据类型|min|max|default|二进制位数
-|-|-|-|-
byte|$-2^7$|$2^7-1$|0|8
short|$-2^{15}$|$2^{15}-1$|0|16
int|$-2^{31}$|$2^{31}-1$|0|32
long|$-2^{63}$|$2^{63}-1$|0L|64
float|||0.0f|32
double|||0.0d|64
boolean|false|true|false
char|\u0000|\uffff||16

## 1. 线程&进程

进程Process是计算机中程序的一次运行活动，是操作系统进行资源分配和调度的最小单位。一旦程序加载到内存中并准备执行，它就是一个进程。

线程Tread包含在进程中，是进程能够进行运算调度的最小单位，一个进程可以并发多个线程。Java中的并发指的是多线程。一个进程中，所有线程共享进程的内存和资源。多线程提高了程序的执行吞吐率，可以执行密集运算从而提高程序的执行效率。

父子进程使用进程间通信机制，同一进程中的线程通过读写数据到进程变量来通信。

![](/imgs/线程和进程.jpg)

**线程安全**


## 1. 修饰符/关键字

- 访问修饰符，修饰类(class)、变量(variable)、方法(method)
  - public
  - protected(不能修饰类)
  - default
  - private
- 其他
  - static
    - 静态变量：类变量，无论类实例化多少对象，静态变量只有一份
    - 静态方法：静态方法与类的实例无关
  - final
    - 修饰变量：一旦赋值，不能改变，一般与static搭配来创建常量
    - 修饰方法：可以被子类继承，但不能重写
    - 修饰类：不能被继承
  - abstract
    - 修饰类
    - 修饰方法
  - synchronized
    - 修饰方法：同一时间只能被一个线程访问
  - transient
    - 修饰变量：不会被序列化
  - volatile
    - 修饰变量：任何时刻所有线程中值都是一致的

修饰符|当前类中|同一包内|子孙类(同包)|子孙类(不同包)|其他包
-|-|-|-|-|-
public|✔|✔|✔|✔|✔
protected|✔|✔|✔|✔|✖
default|✔|✔|✔|✖|✖
private|✔|✖|✖|✖|✖

## 1. 接口和抽象类
接口interface
```
interface Animal {
  public void eat();
  public int getAge();
}
```

抽象类abstract class和抽象方法abstract method
```
public abstract class Person {
  private String name;
  public String getName() { return name; }
  public abstract double getAge();
}
```
- 抽象类不能被实例化
- 抽象方法只能存在于抽象类，抽象类可以包含普通方法
- 构造方法和static方法不能为抽象方法

**抽象类和接口的区别：**
- 抽象类中的方法可以有方法体(实现方法的具体步骤)，接口只有方法名和返回类型
- 抽象类中的成员变量可以是各种类型的，而接口中的成员变量只能是静态变量(public static final)
- 接口中不能含有静态代码块以及静态方法(用 static 修饰的方法)，而抽象类是可以有静态代码块和静态方法
- 一个类只能继承一个抽象类，而一个类却可以实现多个接口

## 1. 序列化

https://www.runoob.com/java/java-serialization.html

## 1. String、StringBuffer、StringBuilder

- 如果要操作**少量的数据**用**String**
- **多线程**操作字符串缓冲区下**操作大量数据**用**StringBuffer**
- **单线程**操作字符串缓冲区下操作**大量数据**用**StringBuilder**

## 1. 垃圾回收机制

垃圾回收Garbage Collection是Java核心技术之一，JVM会自动处理内存动态分配和垃圾回收。

## 1. 锁

同步锁

## 1. 泛型

## 1. 异常
