---
date: 2018-08-12
tags:
- Java
categories:
- Java
---
#### 什么是线程
> 线程是进程的一个实体，是CPU调度和分派的基本单位

它是比进程更小的能独立运行的基本单位。线程自己基本上不拥有系统资源，只拥有一点在运行中必不可少的资源（如程序计数器,一组寄存器和栈），但是它可与同属一个进程的其他的线程共享进程所拥有的全部资源，**线程也叫轻型进程**


> 提到线程那不得不说说进程
#### 线程与进程的区别
> 进程和线程的区别在于

1. 一个程序至少有一个进程，一个进程至少有一个线程。
2. 线程的划分尺度小于进程，使得多线程的并发性高。
3. 另外进程在执行过程中拥有独立的内存单元，而多个线程共享内存，从而极大地提高了程序的运行效率。
4. 每一个独立的线程有一个程序的入口，顺序执行序列和程序的出口。但线程不能独立执行，必须依存在应用程序中，由应用程序提供多个线程执行控制。
5. 进程和线程的**重要区别**:多线程的意义在于一个应用程序中，有多个执行部分可以同时执行。但**操作系统**并没有将多线程看做多个独立的应用，来实现线程的调度和管理以及资源分配。

#### 线程的实现
> Java中线程的实现有两种方式

1. 继承Thread类
2. 实现Runnale接口
##### Thread 类

创建好了自己的线程类之后，就可以创建线程对象了，然后通过start()方法去启动线程。

不是调用run()方法启动线程，run方法中只是定义需要执行的任务，如果调用run方法，即相当于在主线程中执行run方法，跟普通的方法调用没有任何区别，此时并不会创建一个新的线程来执行定义的任务。
```
class MyThread extends Thread{
    private static int num = 0;

    public MyThread(){
        num++;
    }

    @Override
    public void run() {
        System.out.println("主动创建的第"+num+"个线程");
    }
}
```


##### Runnable接口
Runnable的中文意思是“任务”，顾名思义，通过实现Runnable接口，我们定义了一个子任务，然后将子任务交由Thread去执行。

注意，这种方式必须将Runnable作为Thread类的参数，然后通过Thread的start方法来创建一个新线程来执行该子任务。如果调用Runnable的run方法的话，是不会创建新线程的，这跟普通的方法调用没有任何区别
```
public class Test {
    public static void main(String[] args)  {
        System.out.println("主线程ID："+Thread.currentThread().getId());
        MyRunnable runnable = new MyRunnable();
        Thread thread = new Thread(runnable);
        thread.start();
    }
}
class MyRunnable implements Runnable{
    public MyRunnable() {
    }

    @Override
    public void run() {
        System.out.println("子线程ID："+Thread.currentThread().getId());
    }
}
```
#### synchronized
Java语言的关键字，当它用来修饰一个方法或者一个代码块的时候，能够保证在同一时刻最多只有一个线程执行该段代码


> 大多数程序中，线程之间通常有信息流。比如在银行系统中 对一个Account进行存取操作

```
public class Account {
    String holderName;
    float amount;
    public Account(String name, float amt) {
        holderName = name;
        amount = amt;
    }
    public void deposit(float amt) {
        amount += amt;
    }
    public void withdraw(float amt) {
        amount -= amt;
    }
    public float checkBalance() {
        return amount;
    }
}

```
如果此类用于单线程应用则毫无问题，但在多线程环境下。不同的线程就有可能同时访问同一个Account对象，比如一个联合账户的所有者在不同的ATM上同时进行访问。

Account中的amount会同时被多个线程所访问，这就是一个竞争资源，通常称作竞态条件。在这种情况下，存入和支出就可能以这样的方式发生：一个事务被另一个事务覆盖。

这种情况将是灾难性的。但是，Java语言提供了一种简单的机制来防止发生这种覆盖。每个对象在运行时都有一个关联的锁。这个锁可以通过为方法添加关键字synchronized来获得。

这样修订过的Account对象将不会遭受像数据损坏这样的错误：

对一个银行中的多项活动进行同步处理

```
public class Account {
    String holderName;
    float amount;
    public Account(String name, float amt) {
        holderName = name;
        amount = amt;
    }
    public
        synchronized void deposit(float amt) {
        amount += amt;
    }
    public
        synchronized void withdraw(float amt) {
        amount -= amt;
    }
    public float checkBalance() {
        return amount;
    }
}
```

> synchronized关键字的作用域有二种：

1. 是某个对象实例内，synchronized aMethod(){}可以防止多个线程同时访问这个对象的synchronized方法（如果一个对象有多个synchronized方法，只要一个线程访问了其中的一个synchronized方法，其它线程不能同时访问这个对象中任何一个synchronized方法）。这时，不同的对象实例的synchronized方法是不相干扰的。也就是说，其它线程照样可以同时访问相同类的另一个对象实例中的synchronized方法；

2. 是某个类的范围，synchronized static aStaticMethod{}防止多个线程同时访问这个类中的synchronized static 方法。它可以对类的所有对象实例起作用。

3. 除了方法前用synchronized关键字，synchronized关键字还可以用于方法中的某个区块中，表示只对这个区块的资源实行互斥访问。用法是: synchronized(this){/*区块*/}，它的作用域是当前对象；

4. synchronized关键字是不能继承的，也就是说，基类的方法synchronized f(){} 在继承类中并不自动是synchronized f(){}，而是变成了f(){}。继承类需要你显式的指定它的某个方法为synchronized方法；



#### 线程的状态
- 创建（new）状态: 准备好了一个多线程的对象
- 就绪（runnable）状态: 调用了start()方法, 等待CPU进行调度
- 运行（running）状态: 执行run()方法
- 阻塞（blocked）状态: 暂时停止执行, 可能将资源交给其它线程使用
- 终止（dead）状态: 线程销毁

![image](http://incdn1.b0.upaiyun.com/2016/08/665f644e43731ff9db3d341da5c827e1.jpg)

当需要新建一个线程来执行某个子任务时，就会创建一个线程。但是线程创建之后，不会立即进入就绪状态，因为线程的运行需要一些条件（程序计数器，Java栈，本地方法栈都是线程私有的所以需要为线程分配一定的内存空间），只有线程运行需要的条件满足了，才进入就绪状态。

当线程进入就绪状态后，不代表立即就能获取CPU执行时间，当CPU被占用时，需要等待。当得到CPU执行时间之后，线程便真正进入运行状态。

线程在运行状态过程中，可能有多个原因导致当前线程不继续运行下去，比如用户主动让线程睡眠，等待，或者被同步块给阻塞了，此时就对应着多个状态：
- time waiting（睡眠或等待一定的事件）
- waiting（等待被唤醒）
- blocked（阻塞）

#### 上下文切换

对于单核CPU来说（对于多核CPU，此处就理解为一个核），CPU在一个时刻只能运行一个线程，当在运行以运行一个线程的过程中转去运行另外一个线程， 这个叫做线程上下文切换（对于进程也是类似）。

由于可能当前线程的任务并没有执行完毕，所以在切换时需要保存线程的运行状态，以便下次重新切换回来时能继续切换之前的状态运行。举个简单的例子：比如一个线程A正在读取一个文件的内容，正读到文件的一般，此时需要执行线程B，当再次切换回来执行线程A的时候，我们不希望线程A又从文件的开头来读取。

因此需要纪录线程A的运行状态，那么会记录哪些数据呢？因为下次恢复时需要知道在这之前当前线程已经执行到哪条指令了，所以需要记录程序计数器的值，另外比如说线程正在进行某个计算的时候被挂起了，那么下次继续执行的时候需要记录CPU寄存器的状态。所以一般来说，线程上下文切换过程中会记录程序计数器、CPU寄存器状态等数据。

说简单点的：对于线程的上下文切换实际上就是**存储和恢复CPU状态的过程，它使得线程执行能够从中断点恢复执行。**

虽然多线程可以使得任务执行的效率得到提升，但是由于在线程切换时同样会带来一定的开销代价，并且多个线程会导致系统资源占用的增加，所以在进行多线程时要注意这些因素。

> 上下文切换是非常耗效率的

通常的解决方法：
- 合理的创建线程，避免创建了一些线程但其中大部分都是处于waiting状态，因为每当从waiting状态切换到running状态都是一次上下文切换
- 采用无锁编程，比如将数据按照hash（id）进行取模分段，每个线程处理各自分段的数据，从而避免使用锁

#### 死锁
死锁是多线程程序中最常见的问题。当一个线程需要一个资源而另一个线程持有该资源的锁时，就会发生死锁

比如：在一条河上有一座桥，桥面较窄，只能容纳一辆汽车通过，无法让两辆汽车并行。如果有两辆汽车A和B分别由桥的两端驶上该桥，则对于A车来说，它走过桥面左面的一段路（即占有了桥的一部分资源），要想过桥还须等待B车让出右边的桥面，此时A车不能前进；对于B车来说，它走过桥面右边的一段路（即占有了桥的一部分资源），要想过桥还须等待A车让出左边的桥面，此时B车也不能前进。两边的车都不倒车，结果造成互相等待对方让出桥面，但是谁也不让路，就会无休止地等下去。这种现象就是死锁。

> 避免死锁的方式

- 让程序每次至多只能获得一个锁，当然，在多线程环境下，这种情况并不现实
- 设计时考虑清楚锁的顺序，尽量减少潜在的加锁交互数量
- 既然死锁的产生时两个线程无限等待对方持有的锁，那么可以设置等待时间上限。而synchronized不具备这个功能，可以使用Lock类中的tryLock方法去尝试获取锁，这个方法可以指定一个超时上限，超时时返回message

本文只做浅谈，对于一些关键内容今后还会在仔细的深入的研究
