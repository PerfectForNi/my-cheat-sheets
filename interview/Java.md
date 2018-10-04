# Java interview cheat sheet

---

## 接口和抽象类的区别

- 含有 abstract 修饰符的 class 即为抽象类，abstract 类不能创建实例对象，含有 abstract 的方法的类必须定义为 abstract class ，abstract class 里的方法不必是抽象的，抽象类中定义抽象方法必须放在具体子类中实现，所以，不能有抽象的构造方法或抽象的静态方法，如果子类没有实现抽象父类中的所有方法，那么，子类也必须定义为抽象类。
- 接口（interface）可以说成是抽象类的特例。接口中的所有方法都必须是抽象的，接口中的方法定义默认为 public abstract 。接口中的变量是全局常量，即 public static final 修饰的。
- 区别概括如下：

> 
1. 抽象类里可以有构造方法，而接口内不能有构造方法。
2. 抽象类中可以有普通成员变量，而接口中不能有普通成员变量。
3. 抽象类中可以包含非抽象的普通方法，而接口中所有的方法必须是抽象的，不能有非抽象的普通方法。
4. 抽象类中的抽象方法的访问类型可以是 public ，protected 和默认类型，但接口中的抽象方法只能是 public 类型的，并且默认即为 public abstract 类型。
5. 抽象类中可以包含静态方法，接口内不能包含静态方法。
6. 抽象类和接口中都可以包含静态成员变量，抽象类中的静态成员变量的访问类型可以任意，但接口中定义的变量只能是 public static 类型，并且默认为 public static 类型。
7. 一个类可以实现多个接口，但只能继承一个抽象类。
8. JDK1.8 的新特性：接口的默认方法和静态方法，JDK8 允许我们给接口添加一个非抽象的方法实现，只需要使用 default 关键字即可。也可以定义被 static 修饰的静态方法。

## [集合框架](https://github.com/hadyang/interview/blob/master/java/collection.md)

Java 集合框架提供了数据持有对象的方式，提供了对数据集合的操作。Java 集合框架位于`java.util`包下，主要有三个大类：`Collection`、`Map`接口以及对集合进行操作的工具类。

### Collection

![](http://telegra.ph/file/5ef6af1e9c493b39d3e97.png)

* `ArrayList`：线程不同步。默认初始容量为 10，当数组大小不足时增长率为当前长度的`50%`。
* `Vector`：**线程同步**。默认初始容量为 10，当数组大小不足时增长率为当前长度的`100%`。它的同步是通过`Iterator`方法加`synchronized`实现的。
* `LinkedList`：线程不同步。**双端队列形式**。
* `Stack`：**线程同步**。继承自`Vector`，添加了几个方法来完成栈的功能。
* `Set`：Set 是一种不包含重复元素的 Collection，Set 最多只有一个 null 元素。
* `HashSet`：线程不同步，内部使用`HashMap`进行数据存储，提供的方法基本都是调用`HashMap`的方法，所以两者本质是一样的。**集合元素可以为**`null`。
* `NavigableSet`：添加了搜索功能，可以对给定元素进行搜索：小于、小于等于、大于、大于等于，放回一个符合条件的最接近给定元素的 key。
* `TreeSet`：线程不同步，内部使用`NavigableMap`操作。默认元素「自然顺序」排列，可以通过`Comparator`改变排序。
* `EnumSet`：线程不同步。内部使用 Enum 数组实现，速度比`HashSet`快。**只能存储在构造函数传入的枚举类的枚举值**。

### Map

![](http://telegra.ph/file/569669b49aa42ea25c4cf.png)

* `HashMap`：线程不同步。根据`key`的`hashcode`进行存储，内部使用静态内部类`Node`的数组进行存储，默认初始大小为 16，每次扩大一倍。当发生 Hash 冲突时，采用拉链法（链表）。**可以接受为 null 的键值(key)和值(value)**。JDK 1.8 中：当单个桶中元素个数大于等于 8 时，链表实现改为红黑树实现；当元素个数小于 6 时，变回链表实现。由此来防止 hashCode 攻击。
* `LinkedHashMap`：**保存了记录的插入顺序**，在用 Iterator 遍历 LinkedHashMap 时，先得到的记录肯定是先插入的. 也可以在构造时用带参数，按照应用次数排序。在遍历的时候会比 HashMap 慢，不过有种情况例外，当 HashMap 容量很大，实际数据较少时，遍历起来可能会比 LinkedHashMap 慢，因为 LinkedHashMap 的遍历速度只和实际数据有关，和容量无关，而 HashMap 的遍历速度和他的容量有关。
* `TreeMap`：线程不同步，基于**红黑树** （Red-Black tree）的 NavigableMap 实现，**能够把它保存的记录根据键排序,默认是按键值的升序排序，也可以指定排序的比较器，当用 Iterator 遍历 TreeMap 时，得到的记录是排过序的。**
* `HashTable`：线程安全，HashMap 的迭代器(Iterator)是`fail-fast`迭代器。**HashTable 不能存储 null 的 key 和 value。**

### 工具类

* `Collections`、`Arrays`：集合类的一个工具类/帮助类，其中提供了一系列静态方法，用于对集合中元素进行排序、搜索以及线程安全等各种操作。
* `Comparable`、`Comparator`：一般是用于对象的比较来实现排序，两者略有区别。
  > * 类设计者没有考虑到比较问题而没有实现 Comparable 接口。这是我们就可以通过使用 Comparator，这种情况下，我们是不需要改变对象的。
  > * 一个集合中，我们可能需要有多重的排序标准，这时候如果使用 Comparable 就有些捉襟见肘了，可以自己继承 Comparator 提供多种标准的比较器进行排序。

## Servlet 的生命周期

Servlet 的生命周期主要为三个步骤初始化 init()、业务处理 service()、
销毁 destory()。
1. init 阶段：init()方法在 Servlet 实例化的时候调用，而且只调用一次（对于
Servlet 的初始化，一般是第一次被请求时；或者在在 web.xml 中没有配置
`<servlet/>` 标签的映射 `<servlet-mapping/>` 这个时候， 我们可以配置 `<servlet>` 元素中指定了 `<load-on-startup>` 子元素时，容器在启动的时候自动加载这些 Servlet 并调用 init() 方法）， init() 方法的作用是完成一些全局性的比较花费时间的初始化工作。
2. service() 阶段：Servlet 继承了父类的 service() 方法，那么前端 URL 发出的请求不管是以 get 方式或者 post 方式，都将直接走重写的 service() 方法，而不再走 doGet() 和 doPost() 方法。
3. 终止阶段调用 destroy() 方法：Servlet 容器关闭时调用，用来关闭 Servlet 占用的一些资源。

## forward 与 redirect  区别

- Forward ：转发，是服务器内部的一种转向行为，客户端并不能察觉，URL 显示的依然是转发前的地址;它属于一次 Request 请求，转发目标页依然可以使用 Request 范围内的数据。使用场景：多用户多角色的系统根据登录用户进行模块的跳转。
- Redirect ：重定向，服务器会首先响应请求端一个状态码，请求端根据状态码再次发生的请求， URL 的地址会换成后一次请求的地址； 它属于两次 Request 请求，所以第一次 Request 请求范围内的数据将丢失，不能再从 Request 中获取数据。使用场景：Session 过期（或未登录时）跳转到登录页，系统异常跳转到异常页。

## hashCode() && equals()

在《Effective java》中有这样一句话：在每个覆盖了 equals 方法的类中，也必须覆盖 hashCode 方法，如果不这样做的话，就会违反 Object.hashCode 的通用约定，从而导致该类无法结合所有基于散列的集合一起正常动作，这样的集合包括 HashMap, Hashtable, HashSet。在默认情况下，由 Object 类定义的 hashCode 方法会针对不同的对象返回不同的整数，这一般是通过将该对象的内部地址转换成一个整数来实现的。

> 
1. 如果两个对象相等的话，它们的 hashcode 必须相等 。
2. 但如果两个对象的 hashcode 相等的话，这两个对象不一定相等。

举例说，在 HashSet 中，通过被存入对象的 hashCode()来确定对象在 HashSet 中的存储地址，通过 equals() 来确定存入的对象是否重复，hashCode() 和 equals() 都需要重新定义，因为 hashCode() 默认是由对象在内存中的存储地址计算返回一个整数得到，而 equals() 默认是比较对象的引用，如果不同时重写他们的话，那么同一个类产生的两个完全相同的对象就都可以存入 Set，因为他们是通过 equals()来确定的，这就是 HashSet 失去了意义。面试时简单的说，HashSet 的存储是先比较 HashCode，如果 HashCode 相同再比较 equals，这样做的目的是提交储存效率。所以换句方式问，如果用对象来做为 Key 值的话，要满足什么条件呢？答要重写 equals 和 HashCode 方法。

## HTTP

- HTTP 构建于`TCP/IP`协议之上，默认端口号是 80。
- HTTP 是`无连接无状态`的。

无连接的含义是 限制每次连接只处理一个请求。服务器处理完客户的请求，并收到客户的应答后，即断开连接。采用这种方式可以节省传输时间。后来使用了 Keep-Alive 技术。

无状态是指协议对于事务处理没有记忆能力，服务器不知道客户端是什么状态。即我们给服务器发送 HTTP 请求之后，服务器根据请求，会给我们发送数据过来，但是，发送完，不会记录任何信息。

HTTP 协议这种特性有优点也有缺点，优点在于解放了服务器，每一次请求「点到为止」不会造成不必要连接占用，缺点在于每次请求会传输大量重复的内容信息。

为了解决 HTTP 无状态的缺点，两种用于保持 HTTP 连接状态的技术就应运而生了，一个是 Cookie，而另一个则是 Session。Cookie 在客户端记录状态，比如登录状态。Session 在服务器记录状态。

## TCP 与 UDP 区别总结

1. TCP 面向连接（如打电话要先拨号建立连接）;UDP 是无连接的，即发送数据之前不需要建立连接
2. TCP 提供可靠的服务。也就是说，通过 TCP 连接传送的数据，无差错，不丢失，不重复，且按序到达; UDP 尽最大努力交付，即不保证可靠交付
3. TCP 面向字节流，实际上是 TCP 把数据看成一连串无结构的字节流;UDP 是面向报文的；UDP 没有拥塞控制，因此网络出现拥塞不会使源主机的发送速率降低（对实时应用很有用，如 IP 电话，实时视频会议等）
4. 每一条 TCP 连接只能是点到点的;UDP 支持一对一，一对多，多对一和多对多的交互通信
5. TCP 首部开销 20 字节;UDP 的首部开销小，只有 8 个字节
6. TCP 的逻辑通信信道是全双工的可靠信道，UDP 则是不可靠信道

## Comparator 接口与 Comparable 接口区别

1. 他们都是 java 的一个接口, 并且是用来对自定义的 class 比较大小的；
2. Comparable 定义在类的内部，Comparator 定义在类的外部,此时类的结构不需要有任何变化；
3. 实现 Comparable 接口要覆盖 compareTo 方法,在 compareTo 方法里面实现比较，然后用 Collections.sort(myList) 对其排序；
4. 实现 Comparator 需要覆盖 compare 方法，然后用 Collections.sort(myList , new MyComparator()) 对其排序；
5. 两种方法各有优劣, 用 Comparable 简单, 只要实现 Comparable 接口的对象直接就成为一个可以比较的对象, 但是需要修改源代码, 用 Comparator 的好处是不需要修改源代码, 而是另外实现一个比较器, 当某个自定义的对象需要作比较的时候,把比较器和对象一起传递过去就可以比大小了, 并且在 Comparator 里面用户可以自己实现复杂的可以通用的逻辑，使其可以匹配一些比较简单的对象,那样就可以节省很多重复劳动了。

## JVM ?

1. 虚拟机栈（Stack）:这里面就是一个栈，存放基础类型如 int，float 等等这种变量（这与 C++ 一样），同时对于对象，这里还存放着各个对象实例在堆（heap）中的地址。
2. 堆（heap）：这里面就是存放各个对象实例了，当用户 new 一个实例时，就会在堆里面开一块区域了，所以垃圾回收机制也是在这一块对内存进行回收的。
3. 方法区：又叫静态区，用于存储类结构信息的地方，包括常量池、静态变量、构造函数等。存储包括：
- 类信息：如该类的全名，访问修饰符，该类的类型（类还是接口），该类的常量池等类信息
- 方法信息：如方法名，方法返回类型，方法修饰符啊等信息
- 静态变量
- 常量池。存储了诸如符号常量、final 常量值、基本数据类型的字面值等内容。
- 方法表。为了能快速定位到类型中的某个方法。JVM 对每个装载的类型都会建立一个方法表，用于存储该类型对象可以调用的方法的直接引用，这些方法就包括从超类中继承来的。而这张表与 Java 动态绑定机制(参见《java 动态绑定机制实现多态》)的实现是密切相关的。 在 JVM 加载类的同时，会在方法区中为这个类存放很多信息。其中就有一个数据结构叫方法表。它以数组的形式记录了当前类及其所有超类的可见方法字节码在内存中的直接地址 。
4. 本地方法栈：与虚拟机栈基本类似，区别在于虚拟机栈为虚拟机执行的 java 方法服务，而本地方法栈则是为 Native 方法服务。
5. 程序计数器：学过计算机组成原理的应该对这个不陌生，是最小的一块内存区域，它的作用是当前线程所执行的字节码的行号指示器，在虚拟机的模型里，字节码解释器工作时就是通过改变这个计数器的值来选取下一条需要执行的字节码指令，分支、循环、异常处理、线程恢复等基础功能都需要依赖计数器完成。 堆和方法区都是线程共享的。

## sleep & wait

| 方法 | 所属类 | 方法类型 | 锁 | 解除方法 | 场景 | 用途 |
| :-:  | :-:  | :-: | :-: | :-: | :-: | :-: |
| sleep | Thread | 静态方法 | 不释放锁 | timeout, interrupt | 无限制 | 线程内的控制 |
| wait | Object | 非静态方法 | 释放锁 | timeout, notify, interrupt | 同步语句块 | 线程间的通信 |


-  这两个方法来自不同的类分别是 Thread 和 Object
- 最主要是 sleep 方法没有释放锁，而 wait 方法释放了锁，使得其他线程可以使用同步控制块或者方法。
- wait，notify 和 notifyAll 只能在同步控制方法或者同步控制块里面使用，而 sleep 可以在任何地方使用（使用范围）

```java
synchronized(x) {
  x.notify();
  //或者wait()
}
```
- sleep 必须捕获异常，而 wait，notify 和 notifyAll 不需要捕获异常

## Hibernate 缓存机制

- 一级缓存：一级缓存也叫 session 级缓存或事务级缓存，一级缓存的生命周期
和 Session 的生命周期一致，也就是当 session 关闭时缓存即被清除，一级缓存
在 Hibernate 中是不可配置的，即不能被卸载。
- 二级缓存：二级缓存也称进程级缓存或 SessionFactory 级缓存，二级缓存可以
被所有的 session 共享，二级缓存的生命周期和 SessionFactory 的生命周期一致。二级缓存在 Hibernate 中是可以配置的。

## 什么是 IOC （DI）

IoC（Inversion of Control，控制反转）是 Spring 核心，它将之前需要在业务中维护的对象依赖关系交给 Spring 容器去管理，开发人员不需要去创建对象，只要在需要调用的地方直接去从容器中取就可以了， 而这种原来由自己维护对象关系现在交给 Spring 容器来管理的方式就叫做 IOC。

## 单例模式

- 懒汉式，线程不安全

```java
public class Singleton {
  private static Singleton instance;
  private Singleton() {}
  public static Singleton getInstance() {
    if (instance == null) {
      instance = new Singleton();
    }
    return instance;
  }
}
```
- 饿汉式

```java
public class Singleton{
  //类加载时就初始化
  private static final Singleton instance = new Singleton();
  
  private Singleton() {}
  public static Singleton getInstance() {
    return instance;
  }
}
```
- 静态内部类（《Effective Java》上所推荐的）

```java
public class Singleton {
  private static class SingletonHolder {
    private static final Singleton INSTANCE = new Singleton();
  }
  private Singleton() {}
  public static final Singleton getInstance() {
    return SingletonHolder.INSTANCE;
  }
}
```
- 枚举

```java
public enum EasySingleton{
  INSTANCE;
}
```

## return 和 finally 语句块的顺序

- 参考答案：
finally 是在 return 语句之前被执行的,但是 finally 与 return 是相互独立的；return 语句位置会影响到返回值的结果，finally 中的计算将影响到其后 return 结果,不会影响到 try 里面 return 的结果。
- 个人理解：
碰到 try 语句中的 return，先把值储存到一个地方，然后寻找 finally 语句，如果语句中有新的算法，就从那个空间取出这个值进行运算，finally 中有 return 的话就就把「新值」覆盖那个空间的「旧值」，并最终返回；如果 finally 中没有 return 就直接将那个空间中的「旧值」取出来然后返还回去。

## 冒泡排序

```java
public static void bubbleSort(int input[]) {
  for (int i = 0; i < input.length - 1; i++) {
    for (int j = 0; j < input.length - i - 1; j++) {
      if (input[j] < input[j + 1]) {
        int temp = input[j];
        input[j] = input[j + 1];
        input[j + 1] = temp;
      }
    }
  }
  for (int a = 0; a < input.length; a++) {
    System.out.print(input[a] + " ");
  }
}
```
