---
date: 2018-08-01
tags:
- Java
categories:
- Java
---
## MVC

MVC开始是存在于桌面程序中的，M是指业务模型，V是指用户界面，C则是控制器，使用MVC的目的是将M和V的实现代码分离，从而使同一个程序可以使用不同的表现形式。

比如一批统计数据可以分别用柱状图、饼图来表示。C存在的目的则是确保M和V的同步，一旦M改变，V应该同步更新

MVC(Model view controller) 也就是将应用分为了三个内容，model view 和 controller。
- Model
    - 封装应用程序的业务逻辑相关的数据
    - 实现对数据的处理方法
    - 通知视图改变
- View
     - 视图层负责数据的展示，
     - 与model层连接来实现数据的更新
- Controller
    - model层与view层的连接器
    - 应用程序中处理用户交互部分，
    - 通常控制器负责从试图读取数据，
    - 控制用户的输入
    - 向模型发送数据

![image](https://github.com/jccjd/jccjd.github.io/blob/master/images/mvc.PNG?raw=true)

##### MVC特点
MVC模式的特点在于实现关注点分离，即应用程序中的数据模型与业务和展示逻辑解耦。在客户端开发中，就是将model,view之间实现代码分离，松散耦合,成为一个更容易开发维护，和测试的客户端应用程序
 1. View传送指令到Controller；
 2. Controller完成业务逻辑后，要求Model改变状态
 3. Model将新的数据发送到View，用户得到反馈

#####  MVC优点
- **耦合性低，视图层和业务层分离**，这样就允许更改视图层代码而不用重新编译模型和控制器代码
- 重用性高
- 生命周期成本低
- mvc使开发和维护用户接口的技术含量降低
- **可维护性高**，分离视图层和业务逻辑层也使得web应用更易于维护和修改
- 部署快
##### MVC缺点
- **不适合小型，中等规模的应用程序**，花费大量时间将MVC应用到规模并不是很大的应用程序会得不偿失
- **视图与控制器间过于紧密连接**，视图与控制器是相互分离，但却是联系紧密的部件，视图没有控制器的存在，其应用是很有限的，反之亦然，这样就妨碍了他们的独立重用。
- **视图对模型数据的低效率访问**，依据模型操作接口的不同，视图可能需要调用多次才能获取足够的显示数据。对未变化的数据不必要的频繁访问，也将损害操作性能
#####  MVC应用：
在web app 流行之初， MVC 就应用在了java（struts2）和C#（ASP.NET）服务端应用中，后来在客户端应用程序中，基于MVC模式，AngularJS应运而生。

## MVP
MVP（Model-View-Presenter）是MVC的改良模式，由IBM的子公司Taligent提出。和MVC的相同之处在于：Controller/Presenter负责业务逻辑，Model管理数据，View负责显示只不过是将 Controller 改名为 Presenter，同时改变了通信方向。

![image](https://github.com/jccjd/jccjd.github.io/blob/master/images/mvp.PNG?raw=true)

#####  mvp的特点
- View与model之间不通信，view和model只与presenter进行通讯 ，presenter实现了View与model的完全解耦，主要的程序逻辑在presenter中
- View非常薄，不部署任何业务逻辑，称为被动视图，
- presenter与具体的view是没有直接关联，而是通过定义好的接口进行交互，从而使得在变更view的时候可以保持presenter的不变，这样就可以重用。不仅如此，还可以编写测试用的view，模拟用户的各种操作，从而实现对presenter的测试、
#####  MVP与MVC的区别
- **MVP**:View并不直接使用Model，它们之间的通讯是通过Presenter来进行，所有交互都发生在presenter内部
- **MVC**：View会直接从model中读取而不是通过Controller

##### MVP优点
1. 模型与视图完全分离，我们可以修改视图而不影响模型
2. 可以更高效的使用模型，因为所有的交互都发生在一个地方--Presenter
3. 我们可以将一个Presenter用于多个视图，而不需要改变Presenter的逻辑。这个特性非常的有用，因为视图的变化总是比模型的变化频繁
4. 如果我们把逻辑放在Presenter中，那么我们就可以脱离用户接口来测试这些逻辑
##### MVP缺点
视图和Presenter的交互会过于频繁，使得他们的联系过于紧密。也就是说，一但视图改变，present也要改变

## MVVM
MVVM(Model-View-ViewMode) 如果说MVP是对MVC的进一步改进，那么MVVM则是思想的完全变革。它是将“数据模型数据双向绑定”的思想作为核心.

因此在View和Model之间没有联系，通过ViewModel进行交互，而且Model和ViewModel之间的交互是双向的，因此视图的数据的变化会同时修改数据源，而数据源数据的变化也会立即反应到View上。


![image](https://github.com/jccjd/jccjd.github.io/blob/master/images/mvvm.PNG?raw=true)

##### MVVM优点：

MVVM模式和MVC模式类似，主要目的是分离视图（View）和模型（Model），有几大优点：

1. 低耦合，视图（View）可以独立于Model变化和修改，一个ViewModel可以绑定到不同的”View”上，当View变化的时候Model可以不变，当Model变化的时候View也可以不变。

2. 可重用性，可以把一些视图逻辑放在一个ViewModel里面，让很多view重用这段视图逻辑。

3. 独立开发，开发人员可以专注于业务逻辑和数据的开发（ViewModel），设计人员可以专注于页面设计，使用Expression Blend可以很容易设计界面并生成xml代码。

4. 可测试，界面向来是比较难于测试的，而现在测试可以针对ViewModel来写。

这方面典型的应用有.NET的WPF，js框架Knockout、AngularJS等。
