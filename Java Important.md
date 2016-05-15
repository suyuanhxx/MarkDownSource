title: "Java基础"
date: 2016-05-15 10:18:47
tags:
---


###1.基础
1. **抽象类和接口有什么区别？**  
    1.`abstract class`在 Java 语言中表示的是一种继承关系，一个类只能使用一次继承关系。但是，一个类却可以实现多个`interface`。  
    2.在`abstract class`中可以有自己的数据成员，也可以有非`abstarct`的成员方法，而在`interface`中，只能够有静态的不能被修改的数据成员（也就是必须是static final的，不过在 interface中一般不定义数据成员），所有的成员方法都是abstract的。  
    3.`abstract class`和`interface`所反映出的设计理念不同。其实`abstract class`表示的是"is-a"关系，`interface`表示的是"like-a"关系。    
    4.实现接口的类必须实现其中的所有方法，继承抽象类必须实现父类中的抽象方法。抽象类中可以有非抽象方法。接口中则不能有实现方法。  
    5.接口中定义的变量默认是`public static final` 型，且必须给其初值，所以实现类中不能重新定义，也不能改变其值。  
    6.抽象类中的变量默认是`friendly` 型，其值可以在子类中重新定义，也可以重新赋值。  
    7.接口中的方法默认都是 `public abstract` 类型的。  
    8.抽象类和接口都不能直接实例化
        AbstractDemo a = new Demo();//正确,AbstractDemo为抽象父类，Demo为AbstractDemo子类
        InterfaceDemo d = new InterfaceDemo() {//正确，使用匿名类实现化
            public void run() {
            }
        };
2. **在java中怎样实现多线程？**  
    1.`extends Thread`继承 Thread 类，覆盖方法 run()，在创建的 Thread 类的子类中重写 run() ,加入线程所要执行的代码即可。下面是一个例子：
        public class MyThread extends Thread
        {
            int count= 1, number;
            public MyThread(int num)
            {
                number = num;
                System.out.println("创建线程 " + number);
            }
            public void run() {
                while(true)
                {
                    System.out.println("线程 " + number + ":计数 " + count);
                    if(++count== 6) return;
                }
            }
            public static void main(String args[])
            {
                for(int i = 0;i<5; i++)
                    new MyThread(i+1).start();
            }
        }
这种方法简单明了,但是，它也有一个很大的缺点，如果类已经从一个类继承（如小程序必须继承自 Applet 类），则无法再继承 Thread 类，这时如果我们又不想建立一个新的类，应该怎么办呢？  
我们不妨来探索一种新的方法：我们不创建Thread类的子类，而是直接使用它，那么我们只能将我们的方法作为参数传递给 Thread 类的实例，有点类似回调函数。但是 Java 没有指针，我们只能传递一个包含这个方法的类的实例。
那么如何限制这个类必须包含这一方法呢？当然是使用接口！（虽然抽象类也可满足，但是需要继承，而我们之所以要采用这种新方法，不就是为了避免继承带来的限制吗？）  
Java提供了接口`java.lang.Runnable`来支持这种方法。    
    2.`implement Runnable` Runnable接口只有一个方法run()，我们声明自己的类实现Runnable接口并提供这一方法，将我们的线程代码写入其中，就完成了这一部分的任务。但是Runnable接口并没有任何对线程的支持，我们还必须创建Thread类的实例，这一点通过Thread类的构造函数 public Thread(Runnable target);来实现。下面是一个例子：
        public class MyThread implements Runnable
        {
            int count= 1, number;
            public MyThread(int num)
            {
                number = num;
                System.out.println("创建线程 " + number);
            }
            public void run()
            {
                while(true)
                {
                    System.out.println("线程 " + number + ":计数 " + count);
                    if(++count== 6) return;
                }
            }
            public static void main(String args[])
            {
                for(int i = 0; i<5;i++) 
                    new Thread(new MyThread(i+1)).start();
            }
        }
严格地说，创建Thread子类的实例也是可行的，但是必须注意的是，该子类必须没有覆盖 Thread 类的 run 方法，否则该线程执行的将是子类的 run 方法，而不是我们用以实现Runnable 接口的类的 run 方法，对此大家不妨试验一下。  
使用 Runnable 接口来实现多线程使得我们能够在一个类中包容所有的代码，有利于封装，它的缺点在于，我们只能使用一套代码，若想创建多个线程并使各个线程执行不同的代码，则仍必须额外创建类，如果这样的话，在大多数情况下也许还不如直接用多个类分别继承Thread来得紧凑。  
3. **线程的四种状态**  
    1.新状态：线程已被创建但尚未执行（start() 尚未被调用）。  
    2.可执行状态：线程可以执行，虽然不一定正在执行。CPU 时间随时可能被分配给该线程，从而使得它执行。  
    3.死亡状态：正常情况下 run() 返回使得线程死亡。调用 stop()或 destroy() 亦有同样效果，但是不被推荐，前者会产生异常，后者是强制终止，不会释放锁。  
    4.阻塞状态：线程不会被分配 CPU 时间，无法执行。  
4. **用过哪种设计模式？**
总共23种，分为三大类：创建型，结构型，行为型。
    *A.创建模式*    
    1.**Factory(工厂模式)，使用工厂模式就象使用new一样频繁。工厂方法和抽象工厂**  
    2.Prototype(原型模式)，用原型实例指定创建对象的种类，并且通过拷贝这些原型创建新的对象。  
    3.Builder，汽车由车轮 方向盘 发动机很多部件组成，同时，将这些部件组装成汽车也是一件复杂的工作，Builder模式就是将这两种情况分开进行。  
    4.**Singleton(单例模式)，保证一个类只有一个实例,并提供一个访问它的全局访问点。注意线程安全和非线程安全。**  
        //懒汉模式，instance不初始化加载快
        public class Singleton {
            private static Singleton instance=null;
            private  Singleton(){ }
            public static synchronized Singleton getInstance(){
                if(null==instance){
                    instance = new Singleton();
                }
                return instance;
            }
        }
        //饿汗模式，instance初始化加载慢，获取对象速度快
        public class Singleton {
            private static Singleton instance = new Singleton();
            private  Singleton(){ }
            public static  Singleton getInstance(){//静态，不同步，类加载时已初始化，不会有线程问题
                return instance;
            }
        }
    *B.结构模式*      
    1.Facade（外观模式），可扩展的使用JDBC针对不同的数据库编程,Facade提供了一种灵活的实现。    
    2.Proxy（代理模式），以Jive为例,剖析代理模式在用户级别授权机制上的应用。    
    3.Adapter（适配器模式），使用类再生的两个方式:组合(new)和继承(extends),这个已经在"thinking in java"中提到过。  
    4.Composite（），就是将类用树形结构组合成一个单位.你向别人介绍你是某单位，你是单位中的一个元素，别人和你做买卖，相当于和单位做买卖。文章中还对Jive再进行了剖析。  
    5.Decorator（装饰者模式），Decorator是个油漆工,给你的东东的外表刷上美丽的颜色。  
    6.Bridge（桥接模式），将"牛郎织女"分开(本应在一起,分开他们,形成两个接口),在他们之间搭建一个桥(动态的结合)。  
    7.Flyweight，提供Java运行性能,降低小而大量重复的类的开销。  
    *C.行为模式*    
    1.Template，实际上向你介绍了为什么要使用Java 抽象类,该模式原理简单,使用很普遍。  
    2.Memento，很简单一个模式,就是在内存中保留原来数据的拷贝。  
    3.**Observer（观察者模式），介绍如何使用Java API提供的现成Observer。**  
    4.Chain of Responsibility，各司其职的类串成一串,好象击鼓传花,当然如果自己能完成,就不要推委给下一个。  
    5.Command，什么是将行为封装,Command是最好的说明。  
    6.State，状态是编程中经常碰到的实例,将状态对象化,设立状态变换器,便可在状态中轻松切换。  
    7.**Strategy（策略模式），不同算法各自封装,用户端可随意挑选需要的算法。**  
    8.Mediator，Mediator很象十字路口的红绿灯,每个车辆只需和红绿灯交互就可以。  
    9.Interpreter，主要用来对语言的分析,应用机会不多。  
    10.Visitor，访问者在进行访问时,完成一系列实质性操作,而且还可以扩展。  
    11.Iterator（迭代器模式），这个模式已经被整合入Java的Collection.在大多数场合下无需自己制造一个Iterator,只要将对象装入Collection中，直接使用Iterator进行对象遍历。  
5. **软件架构-MVC架构**  
MVC (Model View Controler模型-视图-控制器)   
MVC设计模式是一个很好创建软件的途径，它所提倡的一些原则，内容和显示互相分离。隔离模型、视图和控制器的构件。  
7. java中存在内存泄漏问题吗？请举例说明？  
会 `int i,i2;return (i-i2);//when i为足够大的正数,i2为足够大的负数。结果会造成溢位，导致错误。`
8. List, Set, Map是否继承自Collection接口?  
List，Set是，Map不是  
**Collection**  
├List*元素有放入顺序，元素可重复*    
│├LinkedList  
│├ArrayList  
│└Vector  
│　└Stack  
└Set*元素无放入顺序，元素不可重复*  
**Map** *元素按键值对存储，无放入顺序*    
├Hashtable  
├HashMap  
└WeakHashMap  
ArrayList和LinkedList之间的区别：  
    1)ArrayList是实现了基于动态数组的数据结构，LinkedList基于链表的数据结构。    
    2)对于随机访问get和set，ArrayList觉得优于LinkedList，因为LinkedList要移动指针。  
    3)对于新增和删除操作add和remove，LinedList比较占优势，因为ArrayList要移动数据。  
    4)对ArrayList和LinkedList而言，在列表末尾增加一个元素所花的开销都是固定的。对ArrayList而言，主要是在内部数组中增加一项，指向所添加的元素，偶尔可能会导致对数组重新进行分配；而对LinkedList而言，这个开销是统一的，分配一个内部Entry对象。  
    5)在ArrayList的中间插入或删除一个元素意味着这个列表中剩余的元素都会被移动；而在LinkedList的中间插入或删除一个元素的开销是固定的。  
    6)LinkedList不支持高效的随机元素访问。  
    7)ArrayList的空间浪费主要体现在在list列表的结尾预留一定的容量空间，而LinkedList的空间花费则体现在它的每一个元素都需要消耗相当的空间。    
顺带提一下`Collections`类，`Colletions`类是一个`Colletion`的一个工具类，构造函数为私有，不能被实例化，不能被继承。该类提供了大量的集合类操作方法，包括排序、反转、二分搜索等。     
9. String s = new String("xyz");创建了几个String Object?  
两个对象，一个是"xyx",一个是指向"xyx"的引用对象s。  
10. 是否可以继承String类?  String类是final类故不可以继承。  
11. Java接口的修饰符可以为哪些？    
接口作用：  
（1）接口用于描述系统对外提供的所有服务，因此接口中的成员常量和方法都必须是公开(public)类型的,确保外部使用者能访问它们；  
（2）接口仅仅描述系统能做什么，但不指明如何去做，所以接口中的方法都是抽象(abstract)方法；  
（3）接口不涉及和任何具体实例相关的细节，因此接口没有构造方法,不能被实例化,没有实例变量，只有静态（static）变量；  
（4）接口的中的变量是所有实现类共有的，既然共有，肯定是不变的东西，因为变化的东西也不能够算共有。所以变量是不可变(final)类型，也就是常量了。  
接口的方法默认是public abstract；  
接口中不可以定义变量即只能定义常量(加上final修饰就会变成常量)。所以接口的属性默认是public static final 常量，且必须赋初值。  
注意：final和abstract不能同时出现。  
12. Java创建对象有哪几种方式  
(1) 用new语句创建对象，这是最常见的创建对象的方法。  
(2) 运用反射手段,调用java.lang.Class或者java.lang.reflect.Constructor类的newInstance()实例方法。  
(3) 调用对象的clone()方法。  
(4) 运用反序列化手段，调用java.io.ObjectInputStream对象的 readObject()方法。  
(1)和(2)都会明确的显式的调用构造函数 ；(3)是在内存上对已有对象的影印，所以不会调用构造函数 ；(4)是从文件中还原类的对象，也不会调用构造函数。  
        Person s1 = new Person();
        // 2.第二种方式 静态方式 java.lang.InstantiationException
        Object s2 = (Person)Class.forName("Person").newInstance();
        //第三种方式 用对象流来实现 前提是对象必须实现 Serializable
        ObjectOutputStream objectOutputStream = new ObjectOutputStream(
                new FileOutputStream(filename));
        objectOutputStream.writeObject(s2);
        ObjectInput input=new ObjectInputStream(new FileInputStream(filename));
        Person s3 = (Person)input.readObject();
        //第四种 clone必须实现Cloneable接口和clone()方法 否则抛出CloneNotSupportedException
        Person obj=new Person();
        Person s4= (Person)obj.clone();
13. Java中StringBuilder和StringBuffer区别  
  1.`StringBuilder`是一个可变的字符序列（String不是）  
  2.`StringBuffer`是一个线程安全可变的字符序列，`StringBuilder`不是线程安全，两者方法基本相同，主要为`Append()`和`Insert()`方法  
  3.`StringBuilder`提供了兼容`StringBuffer`的API，被设计成`StringBuffer`的一个简易替换类  
  4.单线程（情况普遍）`StringBuilder`要比`StringBuffer`要快  
  5.大部分情况下效率：`StringBuilder`>`StringBuffer`>`String`（对`String`的'+'操作是转换成`StringBuffer`来进行的）  
  
14. java List初始化和数组初始化对比  
List有三种初始化方式（Map可以使用前两种方式初始化）：  
1.使用List的add方法
        List a = new ArrayList();
        a.add(1);
        a.add(2);
        a.add(3);
2.双括号初始化`List b = new ArrayList(){{add(1);add(2);add(3);}};`  
3.利用Array和ArrayList相互转化初始化`List c = new ArrayList(Arrays.asList(1,2,3,4));`  
数组初始化`int[] d = new int[]{1,2,3,};`//注意区分数组和List
***
###2.高级
1. JVM加载机制？  
2. GC垃圾回收机制和回收算法？  
**引用计数（Reference Counting)**   
**跟踪（trace）**使用跟踪对象的关系图，然后进行收集。使用跟踪方式的垃圾收集算法主要有以下几种：    
**标记清扫（Mark-Sweep）**   
**标记压缩（Mark-Compact）**    
**标记拷贝（Mark-Copy，也有叫节点复制）**   
3. JDK和JRE的区别？  
JRE(Java Runtime Enviroment)是Java的运行环境。面向Java程序的使用者，而不是开发者。如果你仅下载并安装了JRE，那么你的系统只能运行Java程序。JRE是运行Java程序所必须环境的集合，包含JVM标准实现及Java核心类库。它包括Java虚拟机、Java平台核心类和支持文件。它不包含开发工具（编译器、调试器等）。  
JDK(Java Development Kit)又称J2SDK(Java2 Software Development Kit)，是Java开发工具包，它提供了Java的开发环境（提供了编译器javac等工具，用于将java文件编译为class文件）和运行环境（提供了JVM和Runtime辅助包，用于解析class文件使其得到运行）。如果你下载并安装了JDK，那么你不仅可以开发Java程序，也同时拥有了运行Java程序的平台。JDK是整个Java的核心，包括了Java运行环境(JRE)，一堆Java工具tools.jar和Java标准类库(rt.jar)。  

