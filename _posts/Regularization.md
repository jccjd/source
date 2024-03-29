---
date: 2018-11-10
tags:
	- Machine Learning
categories:
	- Machine Learning
---
### 过拟合问题
如下几个图可以直观的表示在线性回归问题中，过拟合，欠拟合，和正确拟合
![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week3/image/拟合1.PNG?raw=true)

分类问题中同样存在这样的问题：
![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week3/image/拟合2.PNG?raw=true)

防止过拟合的几种办法：
1. 减少特征
2. 增加数据量
3. 正则化(Regularized)

### 正则化

正则化代价函数 ：

L1正则化：

![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week3/image/拟合4.PNG?raw=true)

L2正则化：

![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week3/image/拟合3.PNG?raw=true)

### 逻辑回归函数(Sigmoid/Logistic Function)
我们定义逻辑回归的预测函数为 ℎ𝜃(𝑥) = 𝑔(𝜃𝑇𝑋)
其中g（x）函数是sigmoid函数
![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week3/image/拟合5.PNG?raw=true)



![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week3/image/拟合6.PNG?raw=true)


> 0.5可以作为分类的边界

    当z>=0的时候g(z) >=0.5
    当𝜃^𝑇𝑋>=0的时候g(𝜃^𝑇𝑋) >= 0.5

    当z =< 0的时候g(z) <= 0.5
    当𝜃^𝑇𝑋 =< 0的时候g(𝜃^𝑇𝑋) =< 0.5

### 决策边界
如图 该线性函数 当 -3 + x1 + x2 >= 0 则 y = 1

![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week3/image/拟合7.PNG?raw=true)


当函数为非线性时

![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week3/image/拟合8.PNG?raw=true)


### 逻辑回归的代价函数
逻辑回归与线性回归不同，其代价函数分段来表示：

![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week3/image/逻辑回归1.PNG?raw=true)

当 y = 1, h(x) = 1时 ，cost = 0

当 y = 1, h(x) = 0时 ，cost = 无穷

![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week3/image/逻辑代价1.PNG?raw=true)

当 y = 0, h(x) = 1时 ，cost = 无穷

当 y = 0, h(x) = 0时 ，cost = 0

![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week3/image/逻辑代价2.PNG?raw=true)

将其分段写成如下的形式，y = 1 或者当 y = 0 时都符合上面的分段情况

![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week3/image/逻辑代价3.PNG?raw=true)

然后对该代价函数进行梯度下降

gradient descent:

![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week3/image/逻辑代价4.PNG?raw=true)

然后不断求导迭代，下面是对其进行求导的过程

![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week3/image/逻辑代价5.PNG?raw=true)

### 逻辑回归正则化
逻辑回归也可以进行正则化，只要在普通的逻辑回归函数后面加正则化部分即可

普通的逻辑回归代价函数：

![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week3/image/逻辑代价4.PNG?raw=true)

下面对其进行L2型正则化

![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week3/image/逻辑正则化1.PNG?raw=true)

然后后对该函数进行求导：

![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week3/image/逻辑正则化2.PNG?raw=true)

### 正确率与召回率（Precision & Recall)
正确率与召回率是广泛应用于信息检索和统计学分类领域的两个度量值，用来评估结果的质量

一般来说，正确率就是检索出来的条目多少是正确的，召回率就是所有正确的条目有多少被检索出来了

```
F1值 = 2 * （正确率 * 召回率） / （正确率 + 召回率）
```
F1值是综合上面两个指标的评估指标，用于综合反映整体的指标

这几个指标的取值都在0 - 1 之间，数值越接近1，效果越好
如下例可以很好的说明它们之间的关系

![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week3/image/正确召回1.PNG?raw=true)


我们希望检索结果Precision越高越好，同时Recall也是越高越好，但实际上这两者在某些情况下有矛盾。比如极端情况下，我们只搜索出了一个结果，而且是准确的，那么Precision就是100%，但是Recall就很低，如果我们把所有结果都返回，那么比如Recall是100%，但是Precision就很低

因此在不同的场合中需要自己判断希望Precision比较高还是Recall比较高
