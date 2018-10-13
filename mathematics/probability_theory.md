# 概率论笔记

概率论是机器学习中用得非常多的一门数学学科.可以这么说:机器学习实际上就是在做统计分析.这个笔记记录了在机器学习中用得到的一些概率论基本知识.

## 随机变量

**随机变量**指的是可以随机地取不同值的变量.它可以是连续或者离散的.

例如,对于"抛一枚硬币"这个事件,"硬币哪个面朝上"就是一个随机变量,它只有两种取值:"正面朝上"和"反面朝上".显然,这是一个离散的随机变量.

## 概率分布

**概率分布**是用来描述随机变量或一簇随机变量在每个状态的可能性大小.对于离散和连续的随机变量,我们分别通过**概率质量函数**和**概率密度函数**来描述.

### 概率质量函数

概率质量函数是一群离散的取值,它表示了随机变量取某个值的概率.通常用$P(\mathbf{x})$来表示.用$\mathbf{x}\sim P$表示随机变量遵守一个分布.

假如随机变量有多个,则组成**联合概率分布**,例如$P(\mathbf{x}=x,\mathbf{y}=y)$表示二者同时发生的概率,简写为$P(x,y)$.

注意对于概率质量函数,有如下限制:

- $P$的定义域必须是$\mathbf{x}$所有可能状态的集合.
- $\forall x\in\mathbf{x},0\le P(x)\le1$.
- $\sum_{x\in \mathbf{x}}P(x)=1$.

### 概率密度函数

概率密度函数用于研究连续型随机变量,常用$p(x)$表示,概率密度函数有以下性质:

- $p$的定义域是$\mathbf{x}$所有可能状态的集合.
- $\forall x\in \mathbf{x},p(x)\ge0$注意不要求$p(x)\le1$.
- $\int p(x)\mathrm{d}x=1$

注意,概率密度的值$p(x)$并不是概率,概率是通过函数包括的面积给出的,需要通过积分去计算.

## 边缘概率

对于联合概率分布,有边缘概率的概念.指的是想了解多个随机变量中特定的某个变量的分布.

概率质量函数的边缘概率计算公式为:

$$\forall x\in \mathbf{x},P(x=\mathbf{x})=\sum_yP(\mathbf{x}=x,\mathbf{y}=y)$$

对于概率密度函数,计算公式如下:

$$p(x)=\int p(x,y)\mathrm{d}x$$

## 条件概率

在很多情况下,我们希望求出在给定其它事件发生的情况下发生某事件的概率.这叫做**条件概率**.条件概率通过下面的公式计算:

$$P(\mathbf{y}=y|\mathbf{x}=x)=\frac{P(\mathbf{y}=y,\mathbf{x}=x)}{P(\mathbf{x}=x)}$$

注意只有在$P(\mathbf{x}=x)>0$的时候,条件概率才是有意义的.

对于很多随机变量的条件概率,具有链式法则:

$$P(x^{(1)},\dots,x^{(n)})=P(x^{(1)})\prod^n_{i=2}P(x^{(i)}|x^{(1)},\dots,x^{(i-1)})$$

## 独立性

对两个随机变量,若它们的概率分布可以表示为两个因子的乘积形式,则这两个随机变量是**相互独立的**,即:

$$\forall x\in\mathbf{x},y\in\mathbf{y},p(\mathbf{x}=x,\mathbf{y}=y)=p(\mathbf{x}=x)p(\mathbf{y}=y)$$

如果关于另外一个随机变量的条件变量可以写成上述形式,则称为**条件独立**:

$$\forall x\in\mathbf{x},y\in\mathbf{y},z\in\mathbf{z},p(\mathbf{x}=x,\mathbf{y}=y|\mathbf{z}=z)=p(\mathbf{x}=x|\mathbf{z}=z)p(\mathbf{y}=y|\mathbf{z}=z)$$

可以用简化形式$\mathbf{x}\bot\mathbf{y}$表示独立,$\mathbf{x}\bot\mathbf{y}|\mathbf{z}$表示条件独立.

## 期望,方差和协方差

函数$f(x)$关于某个分布$P(\mathbf{x})$的期望记为$\mathbb{E}_{\mathbf{x}\sim P}$.

对于离散随机变量,期望的计算公式为:

$$\mathbb{E}_{\mathbf{x}\sim P} [ f(x)]=\sum_xP(x)f(x)$$

对于连续型随机变量,通过求积分计算:

$$\mathbb{E}_{\mathbf{x}\sim P} [ f(x)]=\int p(x)f(x)\mathrm{d}x$$

期望可以理解为均值.例如抛一枚硬币,我们知道结果是均匀分布.假设正面朝上得5分,反面朝上得2分,则可以算得得分的期望是:$5\times0.5+2\times0.5=3.5$,也就是说得分的均值为3.5分.

**方差**衡量我们对$x$依据它的概率分布采样时,随机变量$\mathbf{x}$的函数值会产生多大的差异:

$$\mathbf{V}ar(f(x))=\mathbb{E} [ (f(x)-\mathbb{E} [ f(x)])^2]$$

当方差比较小的时候,$f(x)$形成的簇比较接近它们的期望值.方差的平方根被称为**标准差**.

**协方差**在某种意义上给出了两个变量线性相关性的强度:

$$\mathbf{C}ov(f(x),g(y))=\mathbb{E} [ (f(x)-\mathbb{E} [ f(x)])(g(y)-\mathbb{E} [ g(y)])]$$

当协方差的绝对值比较大的时候,意味着两个变量的相关性较大.协方差为负数,则两个变量是负相关的(一个变量增大,另外一个变量减小).否则,是正相关的.

如果两个变量相互独立,则它们的协方差为0.但是协方差为0的两个变量并不一定相互独立.这只能保证两个变量没有线性关系,不保证它们没有非线性关系,而相互独立要求两个变量没有任何关系.

一个向量$x\in \mathbb{R}^n$的**协方差矩阵**是一个$n\times n$的矩阵,满足:

$$\mathbf{C}ov(x)_{i,j}=\mathbf{C}ov(x_i, x_j)$$

协方差矩阵的对角元素是方差:

$$\mathbf{C}ov(x_i,x_i)=\mathbf{V}ar(x_i)$$

## 常见的概率分布

下面的一些常见分布在机器学习中经常用到:

### Bernoulli分布

一个二值分布,有:

$$P(\mathbf{x}=1)=\phi$$

$$P(\mathbf{x}=0)=1-\phi$$

期望和方差是:

$$\mathbb{E}=\phi$$

$$\mathbf{V}=\phi(1-\phi)$$

### Multinoulli

这是一个多值分布,是Bernoulli的多值形式.也是一个离散随机分布.

### 高斯分布

一个非常重要的分布,也叫**正态分布**,这是一个连续的分布,在二维情况下,记为:

$$\mathcal{N}(x;\mu,\sigma^2)=\sqrt{\frac{1}{2\pi\sigma^2}}\exp(-\frac{1}{2\sigma^2}(x-\mu)^2)$$

$\frac{1}{2\sigma^2}$不利于在机器学习的时候进行求值,因此引入**精度**$\beta=\frac{1}{\sigma}$.这可以利于对密度函数的求导等操作.

正态分布由两个参数控制,$\mu\in\mathbb{R}$和$\sigma\in(0,\infty)$.$\mu$给出了中心峰值的坐标,因此高斯分布的均值$\mathbb{E}=\mu$.分布的标准差为$\sigma$,方差为$\sigma^2$.

根据**中心极限定理**,很多独立随机变量的和近似服从高斯分布.所以在机器学习中,我们在初始化参数时常常使用高斯分布.

高斯分布可以推广到$\mathbb{R}^n$空间,这时均值$\mu$变成了一个向量,而原来的方差变为了多个变量的协方差矩阵$\Sigma$:

$$\mathcal{N}(x;\mu,\Sigma)=\sqrt{\frac{1}{(2\pi)^2\det(\Sigma)}}\exp(-\frac{1}{2}(x-\mu)^T\Sigma^{-1}(x-\mu))$$

这里的$\Sigma$是一个正定对称矩阵,因此它是非奇异的,可以求逆操作,并且det不为0.

同样,这里也有**精度矩阵**,它就是$\Sigma$的逆矩阵.

### 指数分布

指数分布的定义为:

$$p(x;\lambda)=\lambda\mathbf{1}_{x\ge0}\exp(-\lambda x)$$

其中,$\mathbf{1}_{x\ge0}$表示指示函数,它用于让$x$取负值时概率为0.

一个联系紧密的概率分布是Laplace分布,它允许我们在任意一点$\mu$处设置概率质量的峰值:

$$\mathbf{Laplace}(x;\mu,\gamma)=\frac{1}{2\gamma}\exp(-\frac{|x-\mu|}{\gamma})$$

## 信息论

