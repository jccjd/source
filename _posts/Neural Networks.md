---
date: 2019-01-10
tags:
- Machine Learning
categories:
- Machine Learning
---
### 单层感知器

单层感知器通过模拟神经元的结构如下：

![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week-4/image/神经网络1.PNG?raw=true)


输入节点：x1，x2，x3

输出节点：y

权向量：w1，w2,w3

偏置因子：b

激活函数：

![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week-4/image/神经网络2.PNG?raw=true)


### 感知器学习规则
如下的一个模型

![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week-4/image/神经网络3.PNG?raw=true)

假设：
    t = 1, n = 1, x1 = 1, w1 = -5, b = 0

Step1:
    y = sign(1 * (-5)) = -1
    △w = 1 * (1 - (-1))* 1 = 2
    w1 = w1 + △w = -3

Step2:
    y = sign(1 * (-3)) = -1
    △w = 1 * (1 - (-1))* 1 = 2
    w1 = w1 + △w = -1

Step3:
    y = sign(1 * (-1)) = -1
    △w = 1 * (1 - (-1))* 1 = 2
    w1 = w1 + △w = 1

y = sign(1*1 ) = 1 = t
然后迭代结束 预测值 = 真实值
    n取值一般在0-1之间
    学习率太大容易造成权值调整不稳定
    学习率太小，权值调整太慢，迭代次数太多

不同学习率会导致的问题如下：

![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week-4/image/神经网络4.PNG?raw=true)

### 模型收敛条件
误差小于某个预先设定的较小的值

两次迭代之间的权值变化已经很小

设定最大迭代次数，当迭代超过最大次数就停止

### 单层感知器程序
题目：
    假设平面坐标系上有四个点
    （3,3），（4,3）这两个点的标签为1，
    （1,1），（0,2）这两个点的的标签为-1，
    构建神经网络来分类。  

思路：
    我们要分类的数据是2维数据，所以只要2个输出节点
    我们可以吧神经元的偏执值也设置成一个节点，这样我们需要3个输入节点

输入数据有4个：
    （1,3,3）,(1,4,3),(1,1,1),(1,0,2)
数据对应的标签为(1,1,-1)

初始化权值w0，w1，w2取-1到1的随机数

学习率（learning rate）设置为0.11

激活函数为sign函数

### 线性神经网络

线性神经网络在结构上与感知器非常相似，只是激活函数不同，在
训练模型时把原来的sign函数改为了purelin()函数:y = x

### Delta学习规则

1986年，认知心理学家McClelland和Rumelhart 在神经网络训练中引入了该规则，该规则也可以称为连续感知器学习规则

δ学习规则是一种利用梯度下降法的一般性的学习规则

代价函数（损失函数）(Cost function,Lost Function)

二次代价函数：

![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week-4/image/代价函数1.PNG?raw=true)

误差E是权向量W的函数，我们可以使用梯度下降法来最小化E的值：

![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week-4/image/代价函数2.PNG?raw=true)
