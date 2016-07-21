# Java能力提升计划
主要以J2EE为主线，摆脱迷茫和随波逐流   
这篇文章一定要好好维护，不能copy网上的内容，专表达自己的见解

# TODO List
- Learning English
- 阅读spring源码
- 提高Java知识（基础知识和J2EE相关）
- 读书
- 目前急需提高的技术能力：DI，多线程，ORM映射框架

## Java语言基础
### 1. 集合框架  
    集合框架主要包括  
**Collection**   
├List*元素有放入顺序，元素可重复*    
│├LinkedList*双向链表，使用LinkedList可以实现队列`Queue`（包括优先级队列）和栈`Stack`*，删除和插入时间复杂度O(1)，查询时间复杂度O(n)  
│├ArrayList*数组列表，使用频率最高，插入和删除时间复杂度O(n)，查询时间复杂为O(1)*  
│└Vector*线程安全，其他非线程安全*  
│　└Stack  
└Set*元素无放入顺序，元素不可重复，元素去重时可以使用借助set集合操作完成*  
**Map** *元素按键值对存储，无放入顺序*    
├HashMap*最常使用的一种键值对映射数据结构，HashMap内部维护一个线性数组和链表，key为数组，value为链表存储，采用hash算法计算key值，故查询时间复杂度为O(1)，扩容方式要注意*  
├Hashtable*HashMap的线程安全模式，该数据结构已弃用，使用ConcurrentHashMap替代*  
├ConcurrentHashMap*HashMap的线程安全模式，采用分段锁的概念实现Hash线程安全，且在效率上优于‘全局锁’*    
集合框架中非常重要的两个工具类`Collections`和`Arrays`  
### 2. Java泛型和反射 


### 3. 多线程，高并发。线程池技术`ThreadPool`  
进程和线程之间的区别。

### 4. IO，NIO    
### 5. JVM虚拟机  
### 6. java垃圾回收机制  
---
## J2EE
- Servlet和Servlet容器
- EJB
- Tomcat JBoss Jetty热部署
- Spring依赖注入DI Lookup
---
## 数据结构&&数据库
- 常用数据结构，列表，链表，队列，堆，二叉树
- mysql数据引擎，mysql锁机制
- 数据库表设计范式
---
## 软件架构
- 设计模式
- Spring框架，SpringAOP Spring DI
- SpringMVC
- ORM映射框架，mybatis
- Redis缓存
- 远程调用框架Hessian
- 分布式Dubbo和zookeeper
---
## 操作系统&&网络编程
- TCP/IP
- Socket编程
