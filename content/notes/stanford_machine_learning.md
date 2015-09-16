Title: Machine Learning
Date: 2015-08-29 20:20
Modified: 2015-08-29 20:20
Slug: machine-learning
Authors: Joey Huang
Summary: Notes of Stanford Machine Learning, by Andrew Ng, on www.coursera.org
Status: draft

## 机器学习

课程在 [Coursera][1] 上, 讲师是 Andrew Ng。PDF 格式的课件在 [Stanford 网站][2]上。课程讨论组在[这里][3]可以找到。

## Week 1 机器学习介绍

### What is Machine Learning?

Two definitions of Machine Learning are offered. Arthur Samuel described it as: "the field of study that gives computers the ability to learn without being explicitly programmed." This is an older, informal definition.

Tom Mitchell provides a more modern definition: "A computer program is said to learn from experience E with respect to some class of tasks T and performance measure P, if its performance at tasks in T, as measured by P, improves with experience E."

Example: playing checkers.

* E = the experience of playing many games of checkers
* T = the task of playing checkers.
* P = the probability that the program will win the next game.

### Supervised learning

> In supervised learning, we are given a data set and already know what our correct output should look like, having the idea that there is a relationship between the input and the output.

> Supervised learning problems are categorized into "regression" and "classification" problems. In a regression problem, we are trying to predict results within a continuous output, meaning that we are trying to map input variables to some continuous function. In a classification problem, we are instead trying to predict results in a discrete output. In other words, we are trying to map input variables into discrete categories.

1. Supervised learning: 结果形式己知的机器学习。比如，从过往销售数据，预测未来三个月的销售数据。
1. Classfication learning: 输出结果是离散的。
2. Regression learning: 输出结果是连续的。

### Unsupervised learning

> Unsupervised learning, on the other hand, allows us to approach problems with little or no idea what our results should look like. We can derive structure from data where we don't necessarily know the effect of the variables.

> With unsupervised learning there is no feedback based on the prediction results, i.e., there is no teacher to correct you. It’s not just about clustering.

数据挖掘，从给定的数据集合里去发现规律，进行模式匹配。结果形式不可知。计算结果无法对数据进行反馈。

**例子：声音处理**
从一个有背景音乐的吵杂的会议中演讲的录音文件中，通过数据挖掘和特征匹配来处理这段录音，最终分离出演讲录音和音乐。

* Supervised learning: Given email labed as spam/not spam; learn a email filter.
* Unsupervised learning: Given as set of news articles found on web, group them as a set of articles about the same story.
* Unsupervised learning: Given a set of customer data, automatically discover the market segment and group customers into different market segment.
* Supervised learning: Given a dataset of patients diagnosed as either having diabets or not, learn to classify new patients as having diabets or not.

### 线性回归算法

* Cost Function: 成本函数，用来测量模型的准确度。成本函数把把建模问题转换为求成本函数的极小值。
* Contour plots: 等高线。多参数的成本函数里，有一组参数的值会有相同的成本。这些参数联接起来就是成本函数的等高线。
* Gradient Descent: 阶梯下降，假设的模型逐步逼近真实数据的过程

REF:
1. [Linear Regression with One Variable][4]
2. [Partial derivative in gradient descent for two variables][5]

根据上面两个链接推导出阶梯下降函数。

### 数学

* [微积分][5] 四个最简单的规则
	* 针对 $F(x) = cx^n$，其导函数是 $F'(x) = cn\times{x^{(n-1)}}$
	* 常数的导数是 0
	* 导函数可以穿透累加器，即 $\displaystyle\frac{\partial}{\partial x_0}\sum_{i=0}^nF(x_i) = \sum_{i=0}^n\frac{\partial}{\partial x_0}F(x_i)$
	* 微分传导机制，即$\displaystyle\frac{\partial}{\partial x}g(f(x)) = g'(f(x))\times f'(x)$
* [线性代数][6]
* [最小二阶乘数拟合数据][7]
* 概率论复习

### TODO

* 使用 markdown + MathJax 来书写数学公式
	* [LaTex 教程][8]
	* [LaTex 支持的所有符号列表][9]
* 推导出模型参数的梯度下降公式 (Gradient Descent)
* 推导出 LSM (Widrow-Hoff学习算法)

### 术语

* Calculus: 微积分
* Partial derivatives: 偏导数
* Derivatives: 导数
* Gradient Descent: 梯度下降
* Cost Function: 成本函数
* Contour plots: 等高线
* Least Mean Squares: LSM, 最小均方

## Week 2 多变量梯度下降算法

### 多变量梯度下降算法

预测函数：
$$
h(\theta) = \theta_0 + \theta_1 x_1 + \theta_2 x_2 + ... + \theta_n + x_n = \theta^T x^{(i)}
$$
其中，$x_0 = 1$，$x^{(i)}$ 是训练数据集里的第 i 个数据。$\theta_T$ 是 n + 1 维列向量；$x^{(i)}$ 是 n + 1 维行向量。

成本函数：
$$
J(\theta) = \frac{1}{2m} \sum_{(i=0)}^n \left( h(\theta) - y^{(i)} \right)^2
$$

迭代函数：
$$
\theta_j = \theta_j - \alpha \sum_{i=0}^m \left(\left(h(x^{(i)}) - y^{(i)}\right) x_j^{(i)}\right)
$$

### 变量缩放 Feature Scaling

当变量在 [-1, 1] 这个范围内时，梯度下降算法能较快地收敛。可以使用下面的公式来缩放变量，以让变量在快速收敛的范围内：

$$
x_i := \frac{x_i - \mu_i}{s_i}
$$

其中，$\mu_i$ 是 $x_i$ 的平均值，即 $\mu_i = \frac{1}{n} \sum_{i=1}^n x_i$， $s_i$ 是 $x_i$ 的范围，即 $s_i = max(x_i) - min(x_i)$。

经过这样的转换，变量的范围全部落在 [-0.5, 0.5] 之间。

#### TODO

1. 如何从数学上证明变量绽放后能较快收敛？
2. 可以使用 `pylab` 的等高线在二维平面上画出成本函数和两个参数的关系图

### 学习率

使用 $\alpha$ 来表示学习率，值太高会导致无法收敛，太低收敛又太慢。一个好的办法是画出成本函数 $J(\theta)$ 随着迭代次数不断变化的曲线。这样可以直观地观察到随着迭代地不断进行，成本函数的值的变化情况。在实际情况中，可以从几个经验值里去偿试，比如 0.0001, 0.0003, 0.001, 0.003, 0.01, 0.03, 0.1, 0.3, 1。

#### TODO

1. 找一个数据集，选择不同的学习率来实现，画出不同学习率时的成本函数随着迭代次数的变化情况

### 标准方程 Normal Equalation

通过微分公式可以知道，我们要求成本函数 $J(\theta)$ 的最小值，只需要令其偏导数为零，即：
$$
\frac\partial{\partial{\theta_j}}J(\theta) := 0
$$

把 $J(\theta)$ 用矩阵来表示，并根据矩阵运算定律最终可以推导出下面的方程式：

$$
\theta = \left( X^T X \right)^{-1} X^T y
$$

推导过程可参阅 [cs229-notes1.pdf][10]。推导过程会用到大量的矩阵运算知识。其中 X 是训练数据集，y 是结果数据向量。这样我们就可以通过直接计算的方式，而不是线性回归的方式来求得参数 $\theta$ 的值。


[1]: https://www.coursera.org/learn/machine-learning/home/welcome
[2]: http://cs229.stanford.edu/materials.html
[3]: https://www.coursera.org/learn/machine-learning/discussions?sort=lastActivityAtDesc&page=1
[4]: https://www.coursera.org/learn/machine-learning/supplement/Mc0tF/linear-regression-with-one-variable
[5]: http://math.stackexchange.com/questions/70728/partial-derivative-in-gradient-descent-for-two-variables/189792#189792
[6]: https://www.coursera.org/learn/machine-learning/supplement/NMXXL/linear-algebra-review
[7]: https://en.wikipedia.org/wiki/Linear_least_squares_%28mathematics%29#Derivation_of_the_normal_equations
[8]: http://www.forkosh.com/mathtextutorial.html
[9]: http://mirrors.ctan.org/info/symbols/math/maths-symbols.pdf
[10]: http://cs229.stanford.edu/notes/cs229-notes1.pdf
