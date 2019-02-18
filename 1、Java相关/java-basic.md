### Java基础

- 面向对象的特征：封装、继承和多态 

1、封装

> 定义：隐藏对象的属性和实现细节，仅对外公开接口 。
>
> 目的 ：增强安全性和简化编程，使用者不必了解具体的实现细节，而只是要通过外部接口，一特定的访问权限来使用类的成员。 

包的访问权限修饰符：

> 1、默认:包访问权限
>
> 2、public： 被public修饰的方法或者变量，在任何地方都是可见的
>
> 3、protected：如果一个类的方法或者变量被protected修饰，对于同一个包的类，这个类的方法或变量是可以被访问的。对于不同包的类，只有继承于该类的类才可以访问到该类的方法或者变量。（同类或继承该类）
>
> 4、private：如果一个类的方法或者变量被private修饰，那么这个类的方法或者变量只能在该类本身中被访问，在类外以及其他类中都不能显示地进行访问。（仅仅该类）

注意：**只有默认访问权限和public能够用来修饰类。修饰类的变量和方法四种权限都可以。（本处所说的类针对的是外部类，不包括内部类）。**

2、继承

> 使用现在已经存在的类创建新的类，继承通过extend关键字，只能是单继承。

继承链中对象方法的调用存在一个优先级：this.show(O)、super.show(O)、this.show((super)O)、super.show((super)O)。 

3、多态

> 所谓多态就是指程序中定义的引用变量所指向的具体类型和通过该引用变量发出的方法调用在编程时并不确定，而是在程序运行期间才确定，即一个引用变量倒底会指向哪个类的实例对象，该引用变量发出的方法调用到底是哪个类中实现的方法，必须在由程序运行期间才能决定。因为在程序运行时才确定具体的类，这样，不用修改源程序代码，就可以让引用变量绑定到各种不同的类实现上，从而导致该引用调用的具体方法随之改变，即不修改程序代码就可以改变程序运行时所绑定的具体代码，让程序可以选择多个运行状态，这就是多态性 。

Java实现多态有三个必要条件：继承、重写、向上转型。 

> 继承：在多态中必须存在有继承关系的子类和父类。
>
> 重写：子类对父类中某些方法进行重新定义，在调用这些方法时就会调用子类的方法。
>
> 向上转型：在多态中需要将子类的引用赋给父类对象，只有这样该引用才能够具备技能调用父类的方法和子类的方法。

- final, finally, finalize 的区别

> final ：用于声明属性,方法和类, 分别表示属性不可变, 方法不可覆盖, 类不可继承。
>
> finally：是异常处理语句结构的一部分，表示总是执行。
>
> finalize：是Object类的一个方法，在垃圾收集器执行的时候会调用被回收对象的此方法，可以覆盖此方法提供垃圾收集时的其他资源回收，例如关闭文件等. JVM不保证此方法总被调用 。

- int 和 Integer 有什么区别，Integer的值缓存范围 

```java
public static Integer valueOf(int i) {
     if (i >= IntegerCache.low && i <= IntegerCache.high)
        return IntegerCache.cache[i + (-IntegerCache.low)];
     return new Integer(i);
    }
```

> Integer 是int的包装类，int 默认值为 0，interger 默认值为 null。从源码中看出，Integer的缓存范围为-128-127。

- 装箱和拆箱的实现

```java
public class Main {
    public static void main(String[] args) {        
        Integer i = 10;
        int n = i;
    }
}
```

反编译class文件之后得到如下内容： 

![字节码](https://github.com/guofeiwu/Java-interview-starter/blob/master/%E5%9B%BE%E7%89%87/1.jpg)

从反编译得到的字节码内容可以看出，在装箱的时候自动调用的是Integerd的valueOf(int)方法。而在拆箱的时候自动调用的是Integer的intValue方法。其他的也类似，比如Double、Character，不相信的朋友可以自己手动尝试一下。因此可以用一句话总结装箱和拆箱的实现过程：

>  装箱过程是通过调用包装器的valueOf方法实现的，而拆箱过程是通过调用包装器的 xxxValue方法实现的。（xxx代表对应的基本数据类型）。

[参考blog:深入剖析Java中的装箱和拆箱](https://www.cnblogs.com/dolphin0520/p/3780005.html)



- String、StringBuilder、StringBuffer 

> String是字符串常量，StringBuffer和StringBuilder是字符串变量;
>
> StringBuffer是线程安全的，StringBuidler是非线程安全的;
>
> 执行速度 StringBuilder > StringBuffer > String;

- 重载和重写的区别

> 重载：多个同名函数同时存在，具有不同的参数个数/类型。重载Overloading是一个类中多态性的一种表现。

1、参数类型、个数、顺序至少有一个不相同。

2、不能重载只有返回值不同的方法名。

3、存在于父类和子类、同类中。

> 重写：子类重写父类的方法

1、方法名、参数、返回值相同。

2、子类方法不能缩小父类方法的访问权限。

3、子类方法不能抛出比父类方法更多的异常(但子类方法可以不抛出异常)。

4、方法被定义为final不能被重写。

- 接口和抽象类的区别

> 抽象类可以有构造方法 接口不行
>
> 抽象类可以有普通成员变量 接口没有
>
> 抽象类可以有非抽象的方法 接口必须全部抽象
>
> 抽象类的访问类型都可以  接口只能是 public abstract

**一个类可以实现多个接口 但只能继承一个抽象类** 。

- 说说反射的用途及实现 

> 获取Class对象的三种方式：1、 使用 Class 类的 `forName` 静态方法:Class.forName("全类名")
>
> 2、直接获取某一个对象的 class ，例如 int.class；
>
> 3、调用某个对象的 `getClass()` 方法 ；
>
> 主要参考blog： 
>
> [深入理解Java类型信息(Class对象)与反射机制](https://blog.csdn.net/javazejian/article/details/70768369)
>
> [深入解析Java反射（1） - 基础](https://www.sczyh30.com/posts/Java/java-reflection-1/)

- equals与==的区别 

> 1、对于==，如果作用于基本数据类型的变量，则直接比较其存储的 “值”是否相等；如果作用于引用类型的变量，则比较的是所指向的对象的地址。
>
> 2、对于equals方法，注意：equals方法不能作用于基本数据类型的变量，如果没有对equals方法进行重写，则比较的是引用类型的变量所指向的对象的地址；诸如String、Date等类对equals方法进行了重写的话，比较的是所指向的对象的内容。

- hashCode和equals方法的区别与联系

> 规范1：若重写equals(Object obj)方法，有必要重写hashcode()方法，确保通过equals(Object obj)方法判断结果为true的两个对象具备相等的hashcode()返回值 ；
>
> 规范2：如果equals(Object obj)返回false，即两个对象“不相同”，并不要求对这两个对象调用hashcode()方法得到两个不相同的数。说的简单点就是：“如果两个对象不相同，他们的hashcode可能相同”。 
>
> 根据这两个规范，可以得到如下推论： 
>
>  1、如果两个对象equals，Java运行时环境会认为他们的hashcode一定相等。 
>
>  2、如果两个对象不equals，他们的hashcode有可能相等。  
>
> 3、如果两个对象hashcode相等，他们不一定equals。  
>
> 4、如果两个对象hashcode不相等，他们一定不equals。 

- 什么是Java序列化和反序列化，如何实现Java序列化？或者请解释Serializable 接口的作用 。

>  1、无论何种类型的数据，都是以二进制的形式在网络上传送，为了由一个进程把Java对象发送给另一个进程，需要把其转换为字节序列才能在网络上传送，把JAVA对象转换为字节序列的过程就称为对象的序列化，将字节序列恢复成Java对象的过程称为对象的反序列化 .
>
> 2、只有实现了 serializable和Externalizable接口的类的对象才能被序列化  后者是前者的子类 。
>
> 3、序列化就是一种用来处理对象流的机制，所谓对象流也就是将对象的内容进行流化。可以对流化后的对象进行读写操作，也可将流化后的对象传输于网络之间。序列化是为了解决在对对象流进行读写操作时所引发的问题。 
>
> 4、序列化的实现：将需要被序列化的类实现Serializable接口，然后使用一个输出流(如：FileOutputStream)来构造一个ObjectOutputStream(对象流)对象，接着，使用ObjectOutputStream对象的writeObject(Object obj)方法就可以将参数为obj的对象写出(即保存其状态)，要恢复的话则用输入流。 

参考blog：[什么是java序列化，如何实现java序列化？](https://blog.csdn.net/hustwht/article/details/52157324)

- Object类中常见的方法，为什么wait  notify会放在Object里边？ 

![方法](https://github.com/guofeiwu/Java-interview-starter/blob/master/%E5%9B%BE%E7%89%87/2.jpg)

> notify/notifyAll和wait方法，在使用这3个方法时，必须处于synchronized代码块或者synchronized方法中，否则就会抛出IllegalMonitorStateException异常，这是因为调用这几个方法前必须拿到当前对象的监视器monitor对象，也就是说notify/notifyAll和wait方法依赖于monitor对象。并且每个对象都可以作为锁 。

