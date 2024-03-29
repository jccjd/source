---
date: 2019-02-07
tags:
- Machine Learning
categories:
- Machine Learning
---

### K-Nearest Neighbor
1. 为了判断未知实例的类别，以所有已知类别的实例作为参考选择参数K
2. 计算未知实例与所有已知实例的距离
3. 选择最近K个已知实例
4. 根据少数服从多数的投票法则（majority-voting)，让未知实例归类为K个最邻近样本中最多数的类别

### 欧式距离
欧式距离也称为欧几里得距离具体如下：

![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week3/image/欧式距离1.PNG?raw=true)

其他距离衡量：余弦值（cos）,相关度（correlation）,曼哈顿距离（Manhattan distance）

#### k值的选取
k = 1 与未知分类相邻的一个点的类型

![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week3/image/k值1.PNG?raw=true)

k = 5 与未知分类相邻的5个点中，取相同点数最多的类型

![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week3/image/k值2.PNG?raw=true)

> K的选取一般为奇数


### 算法缺点

![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week3/image/算法1.PNG?raw=true)

    - 算法的复杂度较高（需要比较所以已知实例与要分类的实例）

    - 当其样本分布不平衡时，比如其中一类样本过大（实例数量
      过多）占主导的时候，新的未知实例容易被归类为这个主导
      样本，因为这类样本实例的数量过大，但这个新的未知实例
      实际并没有接近目标样本
