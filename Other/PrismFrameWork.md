Prism框架学习总结
目录	1
1.	Prism框架概述	2
2.	Prism框架引入和使用	2
3.	Prism依赖注入	2
3.1	依赖注入简介	3
3.2	依赖注入方式	3
3.3	Prism框架中的依赖注入	3
4.	Prism事件	4
5.	Prism之MVVM	5
5.1	MVVM介绍	5
5.2	MVVM在SilverLight上的使用	5
6.	总结	7

##Prism框架概述
Prism是由微软Patterns & Practices团队开发的项目，目的在于帮助开发人员构建松散耦合的、更灵活、更易于维护并且更易于测试的WPF应用或是Silverlight应用以及Windows Phone 7应用。使用Prism可以使程序开发更趋于模块化，整个项目将由多个离散的、松耦合的模块组成，而各个模块又可以又不同的开发者或团队进行开发、测试和部署。目前Prism的最新版本是Prism 5，Prism有很完整的文档以及丰富的示例程序。在这里我们使用Prism 4开发Silverlight应用程序。
 Prism框架通过功能模块化的思想，来将复杂的业务功能和UI耦合性进行分离，通过模块化，来最大限度的降低耦合性。Prism中的几大模块：Modules，ModuleCatalog，Shell，Views，ViewModel，Model，Regions，EventAggregator，Dependency Injection container等。Prism主要设计思想为MVVM（Model-View-ViewModel）模式。

##Prism框架引入和使用
Prism只是由几个dll组成，对WPF而言是6个，对Silverlight而言是5个 。在项目中添加相应的dll（动态链接库），使用using指令导入命令空间，即可使用Prism框架
Microsoft.Practice.Prism.dll 本程序集包含了模块化、日志记录服务、通信服务和几个核心接口的定义的实现。它也包含了Prism组件，目标Silverlight应用程序，包括命令，内容区域，和事件。
Microsoft.Practice.Prism.MefExtension.dll 与下面的组件功能类似，容器不同，公司采用这种容器。
Microsoft.Practice.Prism.UnityExtension.dll 该组件包含基础和实用程序类，你可以在应用程序构建的应用程序中使用的基础和实用程序集来使用该应用程序块来使用。例如，它包含一个基础的bootstrapper 类，当应用程序启动时，UnityBootstrapperclass能够使用Prism库服务创建和配置一个Unity容器。
Microsoft.Practice.ServiceLocation.dll 该组件包含由Prism提供控制反转一个抽象的普遍服务定位器接口（IOC）容器和服务定位器；因此，你可以轻松地改变容器实现的。
Microsoft.Practice.Unity.Silverlight.dll 该程序集允许你在应用程序中使用统一应用程序块。默认情况下，应用程序使用Prism统一应用程序块。然而，开发者们更倾向于使用不同的容器实现，可以使用在Prism库中提供的可扩展性点构建适配器。   
##Prism依赖注入
Prism中大量使用到依赖注入（控制反转）的思想，其主要是为了消减计算机程序的糅合性问题。
3.1	依赖注入简介
A（调用者）需要B（被调用者）协助时，传统方法是由A创建B的实例，即调用者创建被调用者，现在A不再创建B的实例，由spring等容器来创建B的实例，这就是控制反转（IoC），将A的控制权反转给IoC容器。
IoC容器用来管理对象的生命周期，依赖关系等，实现程序配置、依赖性规范与代码的的分离。IoC是工厂模式的升级，基本技术为反射机制——根据类名生成类对象。
A类引用B类（A类中有B的对象），这是一种依赖关系，如果由传统的方法A创建B类实例，为强糅合关系，不利于A类的组件化编程，这时引入容器（C类），C类（容器）负责A类中B类的实例化并将之注入到A类中，即依赖注入，注入A对B类的依赖。
依赖注入核心思想，即单一功能原则，每一个类只实现一个功能，分工协作。
依赖注入应该遵守以下两条原则：
1）解除组件之间的强依赖关系（编译器依赖，依赖推迟）
2）运行时提供依赖关系和所需正确实例。
==》运行时产生依赖和实例对象，注入依赖关系。
3.2	依赖注入方式
构造器注入，Setter注入，接口注入。
1）构造器注入：构造器是指A类的构造器，在构造A类实例时把B类的实例传给A类（将A类中B类对象初始化）。依赖关系并没有消失，A和B的依赖关系延迟到容器C被构建的时刻。
2）Setter注入：通过配置文件完成。
3）接口注入：B类提供一个接口，A类实现这个接口。
3.3	Prism框架中的依赖注入
Prism常用术语1.Shell 主程序容器2.Region 内容区域3.Module 模块。
IoC容器：Bootstrapper容器，用来管理对象的生命周期，依赖关系等。处理相关的配置信息。自定义Bootstraper容器继承于Microsoft.Practices.Prism.Bootstrapper。
依赖：Module与IRegionManager之间的依赖（Module依赖于IRegionManager），以MyPrism项目为例——HelloWorldModule依赖于IRegionManager。
注入方式：构造器注入。在构造Modules时实例化IRegionManager，注入依赖。
以下是Bootstrapper工作流程图：
##Prism事件
Prism的事件机制采用消息的发布订阅模式。Prism由事件聚合器定义事件类型，不同类型的事件分别监听不同类型的消息。CompositePresentationEvent<Object>可以实现不同类型的消息事件。包括字符串，自定义类型等。
消息发布者可以发布消息很多类型的消息，消息订阅者能够订阅自己想要获取的消息类型，这样订阅者就能够获取正确的消息。
string为常用消息类型
Object为自定义消息类型
##Prism之MVVM
5.1	 MVVM介绍
MVVM即Model-View-ViewModel是Prism上应用非常广泛的一种设计模式。Model、View、ViewModel三者之间的关系如图所示：
 
View与ViewModel采用双向绑定，View的变动，自动反映在 ViewModel，反之亦然。
5.2	MVVM在SilverLight上的使用   
在SilverLight中绑定模式分三种：OneTime，OneWay，TwoWay。
View层与界面上显示的TextBox采用双向绑定模式，核心代码如下   

MVVMDemo.xaml  

    <TextBlock Grid.Row="0" Grid.Column="0" Text="姓名"/>
    <TextBox x:Name="lname" Grid.Row="0" Grid.Column="1" Text="{Binding Name,Mode=TwoWay }"/>
    <TextBlock x:Name="lname2" Grid.Row="0" Grid.Column="2" Text="{Binding Name,Mode=OneWay }"/>
    <TextBlock Grid.Row="1" Grid.Column="0" Text="年龄"/>
    <TextBox x:Name="lage" Grid.Row="1" Grid.Column="1" Text="{Binding Age,Mode=TwoWay }"/>
    <TextBlock Grid.Row="2" Grid.Column="0" Text="性别"/>
    <TextBox x:Name="lsex" Grid.Row="2" Grid.Column="1" Text="{Binding Sex,Mode=TwoWay }"/>
    <Button rid.Row="3" Grid.Column="2" Width="100" Height="Auto" ontent="Update" Click="Button_Click"/>


ViewModel与MVC中的Controller功能相似，在这里，它具有更多的功能——不但具有Controller的功能还能承担部分Model功能。   
想要实现这种双向改变的功能，Model需要继承INotifyPropertyChanged接口，在Prism中可以直接引入Microsoft.Practices.Prism.ViewModel，继承NotificationObject这个接口，这里给出Prism中使用ViewModel旳部分示例代码。
UserViewModel.cs（注意使用using Microsoft.Practices.Prism.ViewModel;）

    public class UserViewModel : NotificationObject
    {
        private string _name;
        public string Name
        {
            get { return _name; }
            set
            {
                _name = value;
                this.RaisePropertyChanged(() => this.Name);
            }
        }
    }


MVVMDemo.xaml.cs   

    private UserVM us = new UserVM();
    public void init()
    {
        us.Name = "huangxiaoxu";
        us.Age = 22;
        us.Sex = "男";
        lname.DataContext = us;
        lname2.DataContext = us;
        lage.DataContext = us;
        lsex.DataContext = us;
    }

6.	总结
1).Prism框架安装只需引入相应的dll文件（5-6个）即可（这个我开始还摸索了半天）
2).Prism依赖注入需要自己实现IoC容器，公司采用继承MefBootstrapper模式，网上大多数例子采用继承UnityBootstrapper，这两者之间的区别我目前还没有研究。
3).依赖注入思想是降低程序之间的糅合性，需要时才创建依赖。
4).MVVM是一种设计模式，实现方式看个人理解。总体思想是，View和ViewModel之间的双向绑定，改变其中一个另一个也随之改变。
5).Prism事件处理机制
