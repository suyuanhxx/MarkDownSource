title: "Dependency Inject"
date: 2015-04-09 17:57:45
tags:
---

**控制反转**（Inversion of Control，英文缩写为IoC）是一个重要的面向对象编程（OOP）的法则来削减计算机程序的耦合问题，也是轻量级的Spring框架的核心。   
控制反转一般分为两种类型，依赖注入（Dependency Injection，简称DI）和依赖查找（Dependency Lookup）。
Spring的核心是控制反转（IoC）和面向切面（AOP），Spring是一个分层的JavaSE/EEfull-stack(一站式) 轻量级开源框架，贯穿表现层、业务层及持久层。
<blockquote></blockquote>
**轻量**，从大小与开销两方面而言Spring都是轻量的。完整的Spring框架可以在一个大小只有1MB多的JAR文件里发布。并且Spring所需的处理开销也是微不足道的。此外，Spring是非侵入式的：典型地，Spring应用中的对象不依赖于Spring的特定类。
<blockquote></blockquote>
**控制反转**，Spring通过控制反转（IoC）技术达到低耦合。当应用了IoC，一个对象依赖的其它对象会通过被动的方式传递进来，而不是这个对象自己创建或者查找依赖对象。你可以认为IoC与JNDI相反，不是对象从容器中查找依赖，而是容器在对象初始化时不等对象请求就主动将依赖传递给它。  
<blockquote></blockquote>
**面向切面**，Spring提供了面向切面编程的丰富支持，允许通过分离应用的业务逻辑与系统级服务（例如审计（auditing）和事务（transaction）管理）进行内聚性的开发。应用对象只实现它们应该做的，完成业务逻辑仅此而已。它们并不负责（甚至是意识）其它的系统级关注点，例如日志或事务支持。
<blockquote></blockquote>
**容器**，Spring包含并管理应用对象的配置和生命周期，在这个意义上它是一种容器，可以配置每个bean如何被创建，基于一个可配置原型（prototype），bean可以创建一个单独的实例或者每次需要时都生成一个新的实例，以及它们是如何相互关联的。传统的重量级的EJB容器经常是庞大与笨重的，难以使用。
<blockquote></blockquote>
**框架**，Spring可以将简单的组件配置、组合成为复杂的应用。在Spring中，应用对象被声明式地组合，典型地是在一个XML文件里。Spring也提供了很多基础功能（事务管理、持久化框架集成等等），将应用逻辑的开发留给了你。
<blockquote></blockquote>
MVC——Spring的作用是整合，但不仅仅限于整合，Spring框架可以被看做是一个企业解决方案级别的框架。客户端发送请求，服务器控制器（由DispatcherServlet实现的)完成请求的转发，控制器调用一个用于映射的类HandlerMapping，该类用于将请求映射到对应的处理器来处理请求。HandlerMapping 将请求映射到对应的处理器Controller（相当于Action）在Spring当中如果写一些处理器组件，一般实现Controller 接口，在Controller 中就可以调用一些Service 或DAO 来进行数据操作 ModelAndView 用于存放从DAO 中取出的数据，还可以存放响应视图的一些数据。 如果想将处理结果返回给用户，那么在Spring 框架中还提供一个视图组件ViewResolver，该组件根据Controller 返回的标示，找到对应的视图，将响应response 返回给用户。
所有Spring的这些特征使你能够编写更干净、更可管理、并且更易于测试的代码。它们也为Spring中的各种模块提供了基础支持。