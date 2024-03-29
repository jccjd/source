---
date: 2018-10-20
tags:
- Machine Learning
categories:
- Machine Learning
---
#### 矩阵和向量
 ![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week-1/tu/image37.PNG?raw=true)
 矩阵的维数即行数x列数
 Aij指第i行第j列。
 向量是一种特殊的矩阵，列向量![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week-1/tu/image37.2.PNG?raw=true)

#### 加法和标量乘法
1. 矩阵的加法：行列数相等的可以加。
![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week-1/tu/image38.PNG?raw=true)
2. 矩阵的乘法：每个元素都要乘。
![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week-1/tu/image38.2.PNG?raw=true)
#### 矩阵向量乘法
矩阵和向量的乘法如图：
![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week-1/tu/image39.PNG?raw=true)
#### 矩阵乘法
1. m x n 矩阵乘于n x o 矩阵，变成m x o 矩阵。
如下两个矩阵A，B ：
![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week-1/tu/image40.PNG?raw=true)
#### 乘法的性质
1. 矩阵的乘法不满足交换律
2. 矩阵的乘法满足结合律
3. 单位矩阵：从左上角到右下角的主对角线上的元素都为1其他全是0, 表示为I或E
4. AA-1 = A-1A=I
5. AI = IA = A
#### 矩阵的逆，转置
1. 矩阵的逆：如果矩阵A（m * m）有逆矩阵则：AA-1=A-1A=I
2. 转置：
![image](https://github.com/jccjd/Coursera-Machine-Learning/blob/master/week-1/tu/image42.PNG?raw=true)
3.矩阵的转置基本性质:
(𝐴 ± 𝐵)𝑇 = 𝐴𝑇 ± 𝐵𝑇  
(𝐴 × 𝐵)𝑇 = 𝐵𝑇 × 𝐴𝑇  
(𝐴𝑇)𝑇 = 𝐴  
(KA)T = KAT
