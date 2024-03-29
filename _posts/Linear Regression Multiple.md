---
date: 2018-10-15
tags:
- Machine Learning

categories:
- Machine Learning
---
#### Multiple Features(多维特征)
如果我们对房价模型增加更多的特征，如房间数楼层等，构成一个含有多个变量的模型，模型中的特征为（x1,x2,x3....xn）。


![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week-2/tu/week2_4.1.PNG?raw=true)


其中：
1. n代表特征的数量；
2. x（i）代表第i个训练实例，是特征矩阵中的第i行，是一个向量。如上

![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week-2/tu/44.PNG?raw=true)
3. 𝑥𝑗 (𝑖)代表特征矩阵中第 𝑖 行的第 𝑗 个特征，也就是第 𝑖 个训练实例的第 𝑗 个特征。

支持多变量的假设h表示为:![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week-2/tu/4.1_44.PNG?raw=true)


这个公式中有n+1个参数和n个变量，公式简化将x0 = 1 则公式为：![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week-2/tu/week2_44.PNG?raw=true)
此时模型中的参数是一个n+1维的向量，任何一个训练实例也都是n+1维的向量，特征矩阵X的维度是m * （n+1）。因此公式可以简化为：：ℎ𝜃(𝑥) = 𝜃𝑇𝑋
 #### 多变量梯度下降

 我们构建一个代价函数，则这个代价函数是所有建模误差的平方和：

 ![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week-2/tu/tu_45.PNG?raw=true)



 多变量线性回归的批量梯度下降算法为：

 ![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week-2/tu/tu_45_2.PNG?raw=true)

 求导：
 ![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week-2/tu/tu_45_3.PNG?raw=true)

 当n>=1时

![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week-2/tu/tu_45_4.PNG?raw=true)


 代价函数代码（octave）
 ```
 function J = computeCost(X, y, theta)
 m = length(y);
 J = 0;
 A = (X*theta-y).^2(:);
 J = sum(A)/(2*m);
 ```
#### 正规方程法
对于某些线性回归问题，可以使用正规方程法，正规方程法是直接求解出代价函数的最小值
![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week-2/tu/正规方程_1.PNG?raw=true)

对于上图的数据，其代价函数为：
![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week-2/tu/正规方程_2.PNG?raw=true)

用矩阵相乘来表示代价函数，那么将其和矩阵进行转换：
![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week-2/tu/正规方程_3.PNG?raw=true)

然后对该矩阵求导：

![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week-2/tu/正规方程_4.PNG?raw=true)

![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week-2/tu/正规方程_5.PNG?raw=true)


再令求导结果 等于零：

![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week-2/tu/正规方程_6.PNG?raw=true)

矩阵不可逆情况：

1. 线性相关的特征（多重共线性）如：

> x1为房子的面积，单位是平方英尺
x2为房子的面积，单位为平方米
预测房价
1平方英尺~0.0929平方米

2. 特征数据太多（样本数<特征数）

#### 梯度下降法vs标准方程法

梯度下降 | 正规方程
---|---
缺点：1. 需要选择合适的学习率，2. 迭代周期长，3. 只能求近似值  | 特征多时时间复杂度高O（n^3）（n是特征数）
优点： 可以处理多特征 | 不用学习率，和迭代，可以得到最优解


#### 特征缩放
 以房价问题为例，假设我们使用两个特征，房屋的尺寸和房间的数量，尺寸的值为0-2000平方英尺，而房间数量的值是0-5，以两个参数分别为横纵坐标，绘制代价函数的登高线图，如下看起来会比较扁，梯度下降算法需要非常多次的迭代才能收敛
![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week-2/tu/4.3_46.PNG?raw=true)

##### 数据归一化
数据归一化就是把数据的取值范围处理为0-1或者-1到1之间:

> 任意数据转换0-1之间：

    newValue = (oldValue - min)/(max - min)

    数据：(1,3,5,7,9)

    (1 - 1)/(9 - 1) = 0
    (3 - 1)/(9 - 1) = 1/4
    (5 - 1)/(9 - 1) = 1/2
    (7 - 1)/(9 - 1) = 3/4
    (9 - 1)/(9 - 1) = 1
> 任意数据转化为-1 到 1 之间

    newValue = ((oldValue - min)/(max - min) - 0.5) * 2

##### 均值标准化
> x 为特征数据， u为数据的平均值，s为数据的方差

    newValue = (oldValue - u) / s

    数据：(1,3,5,7,9)

    u = (1 + 3 + 5 + 7 + 9)/5 = 5
    s = ((1 - 5)^2 + (3 - 5)^2 + (5 - 5)^2 + (7 - 5)^2 + (9 - 5)^2)/5 = 8

    (1 - 5)/8 = -1/2
    (3 - 5)/8 = -1/4
    (5 - 5)/8 = 0
    (7 - 5)/8 = 1/4
    (9 - 5)/8 = 1/2
