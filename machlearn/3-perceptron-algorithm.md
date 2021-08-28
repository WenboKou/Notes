# 3 Perceptron-Algorithm

Suppose we have sample points $X_1,X\_2,...,X\_N$ which are represented as row vectors. For each sample point, the label $y\_i = \begin{cases} 1\quad if\,X\_i\in classC,and\ -1\quad if\, X\_i\notin classC. \end{cases}$ Goal: find the weights $\omega$ such that $ X\_i \cdot \omega \geq 0 \qquad if \qquad y\_i = 1$ $X\_i \cdot \omega \leq 0 \qquad if \qquad y\_i = -1. $ \[$X\_i\cdot\omega$ is the inner product which is the signed distance\] Equivalently: $y\_iX\_i\cdot\omega \geq0.$ Define the loss function $ L\(z,y\_i\)=\begin{cases} 0\quad if\quad y\_iz\geq0, and\ -y\_iz\quad otherwise. \end{cases} $ Define risk function \(aka objective function or cost function\) $ R\(\omega\)=\frac{1}{n}\sum_{i=1}^{n}L\(X_i\cdot\omega,y\_i\)=\frac{1}{n}\sum_{i\in V}-y\_iX\_i\cdot\omega $ where$V$is the set of indices $i$ for which $y\_iX\_i\cdot\omega&lt;0$, essentially $V$ contains the indices of samples which are incorrectly classified.

Point $x$ lies on hyperplane {$z:\omega\cdot z=0$} $\leftrightarrows \omega\cdot x=0 \leftrightarrows \omega $ lies on hyperplane {$z:x\cdot z = 0$} **Draw a pic to illustrate this** For a sample point $x$ in class C, $\omega$ and $x$ must be on same side of the hyperplane that $x$ transforms into. For a point not in class C, $\omega$ and $x$ must be on opposite sides of the hyperplane that x transforms into. **Draw a pic to illustrate this** We get an optimization problem; We need a optimization algorithm to solve it.

## Gradient descent

balabalabala ==I will fill in this part later.==

$\omega \leftarrow$ arbitrary nonzero starting point while $R\(\omega\)&gt;0$

* $V \leftarrow$ set of indices $i$ for which $y\_iX\_i\cdot \omega &lt; 0$
* $\omega \leftarrow \omega + \epsilon\sum\_{i\in V}y\_iX\_i$

return $\omega$ $\epsilon$ is step size aka learning rate. Problem: Slow! We can use Stochastic gradient descent\(only choose on point from $V$\)

## Maximum Margin Classifiers

The margin of a linear classifier is the distance from the decision boundary to the nearest sample point. Our goal is to make the margin as wide as possible. We enforce the **constraints**

* $y\_i\(\omega\cdot X\_i+\alpha\)\geq1$

_I don't know why the right-hand side is 1, but I think since we have_ $\alpha$ _it can be set to any value_

$\|\|\omega\|\|=1$, signed distance from hyperplane to $X_i$ is $\omega\cdot X\_i + \alpha$. Otherwise, it's$\frac{\omega}{\|\|\omega\|\|}\cdot X\_i + \frac{\alpha}{\|\|\omega\|\|}$. **There are two ways to illustrate why this is signed distance, I will draw two pic to illustrate this later.** Hence the margin is $\min_{i}\frac{1}{\|\|\omega\|\|}\|\omega\cdot X\_i+\alpha\|\geq\frac{1}{\|\|\omega\|\|}$, consider the constraints we can easily get this inequality. To maximize the margin $\rightarrow$ maximize $\frac{1}{\|\|\omega\|\|}$ $\rightarrow$ minimize$\|\|\omega\|\|$. We have optimization problem:

**Find $\omega$ and $\alpha$ that minimize $\|\|\omega\|\|^2$ subject to $y\_i\(X\_i\cdot \omega\)\geq 1$ for all $i \in \[1,n\]$**

 MathJax.Hub.Config\({ tex2jax: {inlineMath: \[\['$', '$'\]\]}, messageStyle: "none" }\);

