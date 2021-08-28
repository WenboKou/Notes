# 10 Regression

## Regression aka Fitting Curves to Data

Choose form of regression fn $h\(x;p\)$ with parameters $p$.\(h=hypothesis\) Choose a cost fn\(objective function\) to optimize

Some regression fns:

* linear:$h\(x;\omega;\alpha\)=\omega \cdot x + \alpha$
* polynomial \[with added polynomial features\]
* logistic:$h\(x;\omega;\alpha\)=s\(\omega \cdot x + \alpha\)$ \[logistic fn $s\(\gamma\)=\frac{1}{1+e^{-\gamma}}$\]

Some loss fns: let $z$ be prediction $h\(x\)$; y be true label

* $L\(z,y\)=\(z-y\)^2$ \[squared error\]
* $L\(z,y\)=\|z-y\|$ \[absolute error\]
* $L\(z,y\)=-ylnz - \(1-y\)ln\(1-z\)$ \[logistic loss, aka cross-entropy:$y\in \[0,1\],z\in \(0,1\)$\]

Some cost fns to minimize:

* $\frac{1}{n}\sum\_{i=1}^{n}L\(h\(X\_i\),y\_i\)$ \[mean loss, can leave out the $\frac{1}{n}$\]
* $max\_{i=1}^{n}L\(h\(X\_i\),y\_i\)$ \[maximum loss\]
* $\sum\_{i=1}^n\omega\_iL\(h\(X\_i\),y\_i\)$ \[weighted sum\]
* we can use regularized on the previous fns. $\lambda\|\|\omega\|\|^2$ or $\lambda \|\|\omega\|\|$

We can mix the three parts freely to get different regression algorithms.

## Least-Squares Linear Regression\(Gauss, 1801\)

Find $\omega,\alpha$ that minimizes $\sum\_{i=1}^n\(X\_i\cdot \omega + \alpha - y\_i\)^2$ Recall fictitious dimension trick: rewrite $h\(x\)=x\cdot \omega + \alpha$ as $\begin{bmatrix} x\_1&x\_2&1 \end{bmatrix}\cdot$ $\begin{bmatrix} \omega\_1 \ \omega\_2 \ \alpha \end{bmatrix}$

We can rewrite the optimization problem as $\|\|X\omega-y\|\|^2=RSS\(\omega\)$ \[Residual Sum of Squares\]

Optimize by calculus: minimize $RSS\(\omega\)=\omega^TX^TX\omega-2y^TX\omega+y^Ty$ $\nabla RSS=2X^TX\omega - 2X^Ty=0 \Rightarrow X^TX\omega=X^Ty$ \[we call this _normal equations_\] if $X^TX$ is singular, problem is underconstrained, which means we have multiple solutions for this problem.

We use a linear solver to find $\omega = \(X^TX\)^{-1}X^Ty$ $X$ is usually not square, so $X$ can't have an inverse. However, every $X$ has a pseudoinverse $X^+=\(X^TX\)^{-1}X^T$ and if $X^TX$ is invertible, then $X^{+}$ is a "left inverse."\(Observe: $X^{+}X=\(X^TX\)^{-1}X^TX=I$ \[which explains the name "left inverse"\]\)

It's worth mentioning that we actually use a linear solver to find $\omega$ instead of inverting the matrix.

Observe: the predicted values of $y$ are $\hat{y\_i} = X\omega=XX^+y=Hy$

Ideally, $H$ would be the identity matrix\[because all predictions are the true label\] and we'd have a perfect fit, but if n &gt; d + 1, the $H$ is singular.

Advantages:

* Easy to compute; just solve a linear system.
* Unique, stable solution \[except when the problem is undercontrained\]

Disadvantages:

* Very sensitive to outlies, because errors are squares!
* Fails if $X^TX$ is singular.\[Which means the problem is underconstrained, has multiple solutions. How to handle this case is mentioned in DIS6\].

## LOGISTIC REGRESSION

Usually used for classification. The input $y\_i's$ can be probabilities, but in most applications they're all 0 or 1.

QDA, LDA:generative models logistic regression: discriminative model \[In LDA, the posterior probabilities are often modeled well by a logistic function. Why not just try to fit logistic function directly to the data, skipping Gaussians?\]

With $X$ and $\omega$ including the fictitious dimension; $\alpha$ is $\omega's$ last component...

Find $\omega$ that minimizes: $J = \sum_{i=1}^{n}L\(X\_i\cdot \omega,y\_i\)=-\sum_{i=1}^{n}\(y\_ilns\(X\_i\cdot \omega\)+\(1-y\_i\)ln\(1-s\(X\_i\cdot \omega\)\)\)$ This is convex! Solve by gradient descent. To do gradient descent, we'll need to compute some derivatives. $s^{'}\(\gamma\)=\frac{d}{d\gamma}\frac{1}{1+e^{-\gamma}}=\frac{e^{-\gamma}}{\(1+e^{-\gamma}\)^2}=s\(\gamma\)\(1-s\(\gamma\)\)$

Let $s_i=s\(X\_i\cdot \omega\)$ $\nabla_{\omega}J=-\sum\(\frac{y\_i}{s\_i}\nabla s\_i - \frac{1-y\_i}{1-s\_i}\nabla s\_i\)=-\sum\(\frac{y\_i}{s\_i} - \frac{1-y\_i}{1-s\_i}\)s\_i \(1-s\_i\)X\_i=-\sum\(y\_i-s\_i\)X\_i=-X^{T}\(y-s\(X\omega\)\)$

Gradient descent rule: $\omega \leftarrow \omega + \epsilon X^T\(y-s\(X\omega\)\)$ Stochastic gradient descent: $\omega \leftarrow \omega + \epsilon \(y\_i-s\(X\_i\cdot \omega\)\)X\_i$

\[This looks a lot like the perceptron learning rule. The only difference is that "$-s\_{i}$" is new. Starting from $\omega=0$ works well in practice.\]

If sample pts are linearly separable and $\omega \cdot x = 0$ separates them\(with decision boundary touching no pt\), scaling $\omega$ to have infinite length causes $s\(X\_i\cdot\omega\) \rightarrow 1$ for a pt $i$ in class $C$, $s\(X\_i\cdot\omega\)\rightarrow 0$ for a pt not in class $C$, and $J\(\omega\)\rightarrow 0$\[in the limit as $\|\|\omega\|\|\rightarrow \infty$\]. That's because for pts belong to $C$, $X\_i\cdot \omega$ is positive, not in $C$ it's negative. This is the only way to get the cost function $J$ to approach zero. Therefore, logistic regression always separates linearly separable pts!

## Least-Squares Polynomial Regression

Replace each $X_i$ with feature vector $\Phi\(X\_i\)$ with all terms of degree 0 ... p e.g.,$\Phi\(X\_i\)=\begin{bmatrix} X_{i1}^2 &X_{i1}X_{i2}&X_{i2}^2&X_{i1}&X_{i2}&1 \end{bmatrix}^T$ \[We added fictitious dimension "1", so we don't need to add it again to do linear or logistic regression. The basis covers all polynomials quadratic in $X_{i1}$ and $X\_{i2}$\]

Logistic Regression + quadratic features = same form of posteriors as QDA.

## Weight Least-Squares Regression

\[The idea of weighted least-squares is that some sample pts might be more trusted than others, or there might be certain pts you want to fit particularly well. Assign more trusted pts a higher weight and a lower weight to outliers.\]

Assign each sample pt a wight $\omega\_i$; collect $\omega\_i$'s in $n\times n$ diagonal matrix $\Omega$.

Greater $\omega_i \rightarrow$ work harder to minimize $\|\hat{y\_i}-y\_i\|^2$. Find $\omega$ that minimizes $\(X\omega - y\)^T\Omega\(X\omega - y\)=\sum_{i=1}^{n}\omega\_i\(X\_i\omega-y\_i\)^2$ \[As with ordinary regression, find the minimum by setting the gradient to zero, which leads to normal equations: $X^{T}\Omega X\omega = X^{T}\Omega y$\]

