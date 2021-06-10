### Regression aka Fitting Curves to Data

Choose form of regression fn $h(x;p)$ with parameters $p$.(h=hypothesis)
Choose a cost fn(objective function) to optimize

Some regression fns:
* linear:$h(x;\omega;\alpha)=\omega \cdot x + \alpha$
* polynomial [with added polynomial features]
* logistic:$h(x;\omega;\alpha)=s(\omega \cdot x + \alpha)$ [logistic fn $s(\gamma)=\frac{1}{1+e^{-\gamma}}$]

Some loss fns: let $z$ be prediction $h(x)$; y be true label
* $L(z,y)=(z-y)^2$ [squared error]
* $L(z,y)=|z-y|$ [absolute error]
* $L(z,y)=-ylnz - (1-y)ln(1-z)$ [logistic loss, aka cross-entropy:$y\in [0,1],z\in (0,1)$]
  
Some cost fns to minimize:
* $\frac{1}{n}\sum_{i=1}^{n}L(h(X_i),y_i)$ [mean loss, can leave out the $\frac{1}{n}$]
* $max_{i=1}^{n}L(h(X_i),y_i)$ [maximum loss]
* $\sum_{i=1}^n\omega_iL(h(X_i),y_i)$ [weighted sum]
* we can use regularized on the previous fns. $\lambda||\omega||^2$ or $\lambda ||\omega||$
  
We can mix the three parts freely to get different regression algorithms.

### Least-Squares Linear Regression(Gauss, 1801)
Find $\omega,\alpha$ that minimizes $\sum_{i=1}^n(X_i\cdot \omega + \alpha - y_i)^2$
Recall fictitious dimension trick: rewrite $h(x)=x\cdot \omega + \alpha$ as $\begin{bmatrix}
    x_1&x_2&1
\end{bmatrix}\cdot$
$\begin{bmatrix}
    \omega_1 \\
    \omega_2 \\
    \alpha
\end{bmatrix}$

We can rewrite the optimization problem as $||X\omega-y||^2=RSS(\omega)$ [Residual Sum of Squares]

Optimize by calculus:
minimize $RSS(\omega)=\omega^TX^TX\omega-2y^TX\omega+y^Ty$
$\nabla RSS=2X^TX\omega - 2X^Ty=0 \Rightarrow X^TX\omega=X^Ty$ [we call this *normal equations*]
if $X^TX$ is singular, problem is underconstrained, which means we have multiple solutions for this problem.

We use a linear solver to find $\omega = (X^TX)^{-1}X^Ty$
$X$ is usually not square, so $X$ can't have an inverse. However, every $X$ has a pseudoinverse $X^+=(X^TX)^{-1}X^T$ and if $X^TX$ is invertible, then $X^{+}$ is a "left inverse."(Observe: $X^{+}X=(X^TX)^{-1}X^TX=I$ [which explains the name "left inverse"])

It's worth mentioning that we actually use a linear solver to find $\omega$ instead of inverting the matrix.

Observe: the predicted values of $y$ are $\hat{y_i} = X\omega=XX^+y=Hy$

Ideally, $H$ would be the identity matrix[because all predictions are the true label] and we'd have a perfect fit, but if n > d + 1, the $H$ is singular.

Advantages:
* Easy to compute; just solve a linear system.
* Unique, stable solution [except when the problem is undercontrained]

Disadvantages:
* Very sensitive to outlies, because errors are squares!
* Fails if $X^TX$ is singular.[Which means the problem is underconstrained, has multiple solutions. How to handle this case is mentioned in DIS6].