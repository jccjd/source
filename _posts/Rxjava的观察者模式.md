---
date: 2018-05-28
tags:
- Android
---
- 观察者模式面向的需求是：A 对象（观察者）对B对象（被观察者）的某种变化高度敏感，需要在B变化的一瞬间做出反应。经典例子：警察抓小偷，警察需要在小偷伸手作案的时候实施抓捕。警察是观察者，小偷是被观察者，警察需要时刻盯着小偷的一举一动，才能保证不会漏过任
何瞬间。

- RxJava有四个基本概念：Observable（可观察者，即被观察者），Observer（观察者），subscribe（订阅），事件。

- Observable和Observer 通过subscribe()方法实现订阅关系，从而Observable可以在需要的时候发出事件来通知Observer。

**Rxjava基本实现**

1. 创建Observer
   - observer即观察者，它决定事件触发的时候将有怎样的行为。Rxjava中的Observer接口的实现方式：

2. 创建Observable
   - Observable即被观察者，它决定什么时候触发事件以及触发怎样的事件。Rxjava使用create()方法来创建一个Observable，并为它定义事件触发规则：
3. Subscribe(订阅)
   - 创建了Observable和Observer之后，在用subscribe()方法将他们联结起来，整条链子就可以工作了

**在异步模型中创建观察者**
- 定义一个方法，它完成某些任务，然后从异步调用中返回一个值，这个方法是观察者的一部分
- 将这个异步调用本身定义为一个Observable

- 观察者通过订阅（Subscribe）操作关联到那个Observable
- 继续业务逻辑，等方法返回时，Observable会发射结果，观察者的方法会开始处理结果或结果集
