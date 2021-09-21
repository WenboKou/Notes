# 11 Newton's Method and ROC

## Newton's Method

Idea: At point $v$. Approximate $J\(\omega\)$ near $v$ by quadratic fn. Jump to its unique critical pt. Repeat until bored.

Iterative optimization method for smooth fn $J\(\omega\).$ Taylor series about $v$: $\nabla J\(\omega\)=\nabla J\(v\)+\(\nabla^2J\(v\)\)\(\omega - v\)+O\(\|\|\omega - v\|\|^2\)$ Where $\nabla^2J\(v\)$ is the Hessian matrix of $J$ at $v$. Find critical pt $\omega$ by setting $\nabla J\(\omega\)=0$: $\omega = v - \(\nabla^2J\(v\)\)^{-1}\nabla J\(v\)$ Usually, we don't compute a matrix inverse directly. It is faster to solve a linear system of equations.

Another way to interpret this: Second Order Taylor series: $J\(\omega\) = J\(v\) + \nabla J\(v\)\(\omega - v\) + \(\omega - v\)^T\(\nabla^2J\(v\)/2\)\(\omega - v\)$. We only need to jump to its unique pt.

Pick starting pt $\omega$ repeat until convergence:

* $e \leftarrow$ solution to linear system $\(\nabla^2 J\(\omega\)\)e=-\nabla J\(\omega\)$
* $\omega \leftarrow \omega + e$

Warning: Doesn't know difference between minima, maxima, saddle pts. Starting pt must be close enough to desired critical pt. Computing Hessian can be expensive.

## Logistic regression with Newton's Method

Recall: $s'\(\gamma\) = s\(\gamma\)\(1-s\(\gamma\)\)$ $\nabla_{\omega}J = -\sum_{i=1}^n \(y_i-s\_i\)X\_i=-X^T\(y-s\)$ Hessian: $\nabla_{\omega}^2J\(\omega\) = \sum\_{i=1}^ns\_i\(1-s\_i\)X\_iX\_i^{T}=X^T\Omega X$ $\Omega$ is +ve definite $\Rightarrow$ $X^T\Omega X$ is +ve semidefinite $\Rightarrow$ $J\(\omega\)$ is convex. \(二阶海塞矩阵半正定则是凸函数\)

Newton's Method:

* $\omega \leftarrow$ 0
* repeat until convergence
  * $e \leftarrow$ solution to normal equations $\(X^T\Omega X\)e=X^T\(y-s\)$
  * $\omega \leftarrow \omega + e$ 

## LDA vs. Logistic Regression

Advantages of LDA:

* for well-separated classes, LDA stable; log. reg. unstable.
* $&gt;$ 2 class easy & elegant; log. reg. needs modifying\(e.g.,softmax regression\)
* LDA slightly more accurate when classes nearly normal, especially if $n$ is small

Advantage of log. reg:

* More emphasis on decision boundary; always separates linearly separable pts.
* More robust on some non-Gaussian distributions.
* Naturally fits labels between 0 and 1.

## ROC CURVES

放张图解释一下。 不过我还不是很懂这个部分。

