---
date: 2019-02-14
tags:
- Machine Learning
categories:
- Machine Learning
---

### 主成分分析
PCA（Principal Component Analysis）


### 数据压缩
数据压缩可以加快算法的运行时间，占用部分空间（但占用的空间极少），即是以空间换时间。

> 2D->1D

![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week-8/image/数据压缩1.PNG?raw=true)

> 3D->2D

![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week-8/image/数据压缩2.PNG?raw=true)

### 数据可视化

### 降维分析
找到数据中最重要的方向（方差最大的方向）

![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week-8/image/数据压缩3.PNG?raw=true)


第一个主成分就是从数据差异性最大（方差最大）的方向提取出来的，第二个主成分则是来自于数据差异性次的方向，并且要与第一个主成分方向正交

![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week-8/image/数据压缩4.PNG?raw=true)

### PCA与线性回归的差异

![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week-8/image/PCA1.PNG?raw=true)


### PCA算法流程

1. 数据预处理：中心化X - avg（X）
2. 求样本的协方差矩阵1/m * X *X^T
3. 对协方差 1/m * X *X^T 矩阵做特征值分解
4. 选出最大的k个特征值对应的k个特征向量
5. 将原始数据投影到选取的特征向量上
6. 输出投影后的数据集


### 协方差

方差描述一个数据的离散程度：

![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week-8/image/协方差1.PNG?raw=true)

协方差描述两个数据的相关性，接近1即是正相关，接近-1即是负相关，接近0即是不相关

![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week-8/image/协方差2.PNG?raw=true)

### 协方差矩阵

协方差只能处理二维问题，那维度多了自然需要计算多个协方差，我们可以使用矩阵来组织这些数据。

协方差矩阵是一个对称的矩阵，而且对角线是各个维度的方差。

二维：

![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week-8/image/协方差3.PNG?raw=true)

三维：

![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week-8/image/协方差4.PNG?raw=true)

n个特征，m个样本，n行m列

![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week-8/image/协方差矩阵1.PNG?raw=true)

n行m列乘m行n列-> n行n列

![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week-8/image/协方差矩阵2.PNG?raw=true)

![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week-8/image/协方差矩阵3.PNG?raw=true)

### 特征值与特征向量

通过数据集的协方差矩阵及其特征值分析，我们可以得到协方差矩阵的特征向量和特征值。我们需要保留k个维度的特征就选取最大的k个特征值
