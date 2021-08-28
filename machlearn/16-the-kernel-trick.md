# Kernels

Recall: with $d$ input features, degree-$p$ polynomials blow up to $O\(d^p\)$ features. Magically we use those features without computing them!

Observation: In many learning algs,

* the weights can be written as a linear combo of sample pts, &
* we can use inner products of $\Phi\(x\)$ 's only $\Rightarrow$ don't need to compute $\Phi\(x\)$!

Suppose $\omega = X^T a = \sum\_{i=1}^{n}a\_iX\_i$ for some $a\in \R^{n}$. \[This is an observation. Is there a rigorous way to get this?\] Substitute this identity into alg. and optimize $n$ dual weights $a$ instead of $d+1$\(or $d^p$\) primal weights $\omega$.

## Kernel Ridge Regression

Center $X$ and $y$ so their means are zero: $X_i \leftarrow X\_i - \mu\_X$, $y\_i \leftarrow y\_i - \mu\_y$, $X_{i,d+1}=1$ \[don'e center the 1's!\] This lets us replace $I'$ with $I$ in normal equations:

$$
(X^TX + \lambda I)\omega = X^Ty
$$

\[Can you remember where we get this?\]

\[To dualize ridge regression, we need the weights to be a linear combination of the sample points. Unfortunately, that only happens if we penalize the bias term $\omega\_{d+1}=\alpha$, as these normal equations do. Fortunately, when we center $X$ and y, the "expected" value of the bias is zero. The actual bias won't usually be exactly zero, but it wil often be close enough that we won't do much harm by penalizing the bias.\] 这句话大概是说$l\_2$ penalize时没有算偏置，为了把偏置偏置算进去又不影响它，可以中心化。\[如果数据集中在中心附近的话那只需一条将近过原点的直线就能分了。\]**这块还不太懂，之后再看的话再补上理解吧**

Suppose $a$ is a solution to

$$
(XX^T+\lambda I)a = y
$$

Then $X^Ty = X^T X X^T a + \lambda X^T a = \(X^TX + \lambda I\)X^T a$. Therefore, $\omega = X^T a$ is a solution to the normal equations, and $\omega$ is a linear combo of sample pts! $a$ is a dual solution; solves the dual form of ridge regression: Find $a$ that minimizes $\|\|XX^Ta - y\|\|^2 + \lambda\|\|X^T a\|\|^2$ \[We obtain this dual form by substituting $\omega = X^T a$ into original ridge regression cost function.\] Training: Solve $\(XX^T + \lambda I\)a=y$ for $a$. Testing: Regression fn is

$$
h(z)=\omega^Tz=a^TXz=\sum_{i=1}^{n}a_i(X_i^Tz)
$$

Let $k\(x,z\)=x^Tz$ be kernel fn. Let $K=XX^T$ be $n \times n$ kernel matrix. Note $K\_{ij}=k\(X\_i,X\_j\)$. $K$ is singular if $n &gt; d + 1$. \[And sometimes even if it's not.\] In that case, probably no solution if $\lambda = 0$. \[Then we must choose a positive $\lambda$. But that's okay\]Because when $\lambda$ is positive we have a positive definite matrix.

Dual ridge reg. alg:

* $\forall i,j,\qquad K\_{ij}\leftarrow k\(X\_i,X\_j\) \Leftarrow O\(n^2d\)$ because we have $d$ features and $n^2$ positions.
* Solve $\(K+\lambda I\)a = y$ for $a \Leftarrow O\(n^3\)$ \[I don't know why, since I don't know how to solve this.\] 
* for each test pt $z$
  * $h\(z\)\leftarrow \sum\_{i=1}^na\_ik\(X\_i,z\) \Leftarrow O\(nd\)$ \[d features and n times.\]

Dual: solve $n\times n$ linear system, $O\(n^3 + n^2d\)$ time Primal: $d \times d$, $O\(d^3 + d^2n\)$ time We prefer dual when $d &gt; n$.

## The Kernel Trick\(aka Kernelization\)

The polynomial kernel of degree $p$ is $k\(x,z\)=\(x^Tz+1\)^p$ Theorem: $\(x^Tz + 1\)^p = \Phi\(x\)^T\Phi\(z\)$ where $\Phi\(x\)$ contains every monomial in $x$ of degree $0 \ldots p$. Example for $d=2,p=2$:

$$
(x^Tz+1)^2=x_1^2z_1^2+x_2^2z_2^2+2x_1z_1x_2z_2+2x_1z_1+2x_2z_2+1
\\=\begin{bmatrix}
    x_1^2 & x_2^2 & \sqrt{2}x_1x_2 & \sqrt{2}x_1 & \sqrt{2}x_2 & 1
\end{bmatrix}
\begin{bmatrix}
    z_1^2 & z_2^2 & \sqrt{2}z_1z_2 & \sqrt{2}z_1 & \sqrt{2}z_2 & 1
\end{bmatrix}^T
$$

\[Notice the factors of $\sqrt{2}$. If you try a higher polynomial degree $p$, you'll see a wider variety of these constants. We have no control of the constants, but they don't matter excessively much, because the primal weights $\omega$ will scale themselves to compensate.\]

Key wim: compute $\Phi\(x\)^T\Phi\(z\)$ in $O\(d\)$ time instead of $O\(d^p\)$, even though $\Phi\(x\)$ has length $O\(d^p\)$. Kernel ridge regression replaces $X\_i$ with $\Phi\(X\_i\)$: Let $k\(x,z\)=\Phi\(x\)^T\Phi\(z\)$. But don't compute $\Phi\(x\)$ or $\Phi\(z\)$; compute $k\(x,z\)=\(x^Tz+1\)^p$!

## Kernel Perceptrons

Featurized perceptron alg:

* $\omega \leftarrow y\_1 \Phi\(X\_1\)$ \[starting point is arbitrary, but can't be zero\]
* while some $y\_i\Phi\(X\_i\)\cdot \omega &lt; 0$
  * $\omega \leftarrow \omega + \epsilon y\_i \Phi\(X\_i\)$
* for each test pt $z$
  * $h\(z\) \leftarrow \omega \cdot \Phi\(z\)$

$\Phi\(X\_i\)\cdot \omega = \(\Phi\(X\)\omega\)\_i = \(\Phi\(X\)\Phi\(X\)^Ta\)\_i = \(Ka\)\_i$ Dual perceptron alg:

* $a \leftarrow \begin{bmatrix}

    y\_1 & 0 & \cdots 0

  \end{bmatrix}^T$ \[starting point is arbitrary, but can't be zero\]

* $\forall i,j,\quad K\_{ij} \leftarrow k\(X\_i,X\_j\) \Leftarrow O\(n^2d\)$
* while some $y\_i\(Ka\)\_i &lt; 0$
  * $a\_i \leftarrow a\_i + \epsilon y\_i \Leftarrow O\(1\)$ update $Ka$ in $O\(n\)$ time
* for each test pt $z$
  * $h\(z\) \leftarrow \sum\_{j=1}^na\_jk\(X\_j,z\) \Leftarrow O\(nd\)$

\[A big deal is that running times depend on the original dimension $d$, not on the length $D$ of $\Phi\(\cdot\)$!\]

## Kernel Logistic Regression

Stochastic gradient descent step:

* $a\_i \leftarrow a\_i + \epsilon\(y\_i - s\(\(Ka\)\_i\)\)$

Batch gradient descent step:

* $a \leftarrow a + \epsilon\(y-s\(Ka\)\)$

For each test pt $z$:

* $h\(z\) \leftarrow s\(\sum\_{j=1}^na\_jk\(X\_j,z\)\)$

不懂这个batch是怎么做的，是如何把数据弄成batch的呢？ \[If you're using logistic regression as classifier and you don't care about posterior probabilities, you can skip the logistic function and just compute the summation.\]

## Gaussian Kernel

不太懂，以后再说吧

