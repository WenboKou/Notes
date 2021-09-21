# 8 Eigenvectors AND Anisotropic Gaussians

Theorem: if $v$ is eigenvector of A eigenvalue $\lambda$, then $v$ is eigenvector of $A^k$ eigenvalue of $\lambda^k$.

Theorem: if A is invertible, then $v$ is eigenvector of $A^{-1}$ eigenvalue $\frac{1}{\lambda}$

Spectral Theorem: every real, symmetric $n\times n$ matrix has real eigenvalues and $n$ eigenvectors that are mutually orthogonal. Denote the orthonormal basis of eigenvectors $q\_1,q\_2,\ldots,q\_n$ and their eigenvalues $\lambda\_1,\ldots,\lambda\_n.$ Let $Q$ be an orthogonal matrix with $q\_1,q\_2,\ldots,q\_n$ as its columns, and $\Lambda =$ diag\($\lambda\_1,\ldots,\lambda\_n$\). Since by definition $Aq\_i=\lambda\_i q\_i$ for every $i$, the following relationship holds:

$$
AQ = Q\Lambda
$$

Right-multiplying by $Q\_T$, we arrive at the decomposition:

$$
A = Q\Lambda Q^T
$$

Because of orthonormal we get $QQ^T = I$.

**Quadratic Forms** $\|\|z\|\|^2=z^Tz$ $\leftarrow$ quadratic; isosurfaces are spheres. $\|\|A^{-1}x\|\|^2=x^{T}A^{-2}x$$\leftarrow$ quadratic of $A^{-2}$; isosurfaces are ellipsoids. This is quite easy to understand, let's say that the z axis is the module of the vector $x$, using the plane with different height to cut, let's say the height is 1, we get $\|\|z\|\|^2=1$, this is a sphere. $A^{-1}x$ means we stretched the whole coordinate along some axises. Let's say along the original $x\_1, x\_2$ axises. For height equals 1 we get $\|\|A^{-1}x\|\|=\|\|\(ax\_1,bx\_2\)^T\|\|^2=1$, this is ellipsoid.

\[The matrix $A$ maps the circle on the left to the ellipses on the right. They're stretching along the direction with eigenvalue 2, and shrinking along the direction with eigenvalue -1/2.\]

Special case: $A$ is diagonal $\leftrightarrow$ eigenvectors are coordinate axes , ellipsoids are axis-aligned.

Another explanation: Suppose $\|\|x\|\|=1$, $A = Q\Lambda Q^T$, $A^{-1} = Q\Lambda^{-1} Q^T$. Because $Q$ is orthonormal we get $\|\|Q^T x\|\|=1$. Clearly it's a sphere. Because $\Lambda$ is diagonal. $\Lambda^{-1}Q^Tx$ is stretching points on sphere $\|\|Q^T x\|\|=1$. $Q\Lambda^{-1}Q^Tx$, $Q$ can spain the points. The new axises become the direction of the eigenvectors. Why? Suppose axis $e\_1 = \(1,0,\ldots,0\)$. $Qe\_1^T \rightarrow q\_1$.

A symmetric matrix $M$ is _positive definite_ if $\omega^T M \omega &gt; 0$ for all $\omega \neq 0 \leftrightarrow$ eigenvalues positive. ... is _positive semidefinite_ if $\omega^T M \omega \geq 0$ for all $\omega \leftrightarrow$ all eigenvalues nonnegative ... is _indefinite_ if there are positive eigenvalue and negative eigenvalue. ... invertible if no zero eigenvalue. We can analyze the shape of $\|\|A^{-1}x\|\|$ for the above cases.

**Building a Quadratic** \[Suppose you have an ellipsoid isosurface in mind. Suppose you pick the ellipsoid axes and the radius along each axis, and you want to create the matrix whose quadratic form will have isosurffaces matching the ellipsoid of your dreams.\]

Choose n mutually orthogonal unit n-vectors $v1,\cdots,v\_n$. Let $V=\[v\_1\;v\_2\;\cdots\;v\_n\]$\[This is a $n\times n$ matrix\] Observe: $V^TV=I\rightarrow V^T=V^{-1}\rightarrow VV^{T}=I$

Choose some radii $\lambda\_i$: Let $\Lambda=\begin{bmatrix} \lambda\_1 & 0 & \cdots & 0 0 & \lambda\_2 & \cdots & 0 \cdots  0 & 0 & \cdots & \lambda\_n \end{bmatrix}$

Define "eigenvectors" $AV=V\Lambda\Rightarrow AVV^T=V\Lambda V^T\Rightarrow A=V\Lambda V^T=\sum\_{i=1}^n\lambda\_iv\_iv\_i^T$

Observe:$A^2=V\Lambda V^TV\Lambda V^T=V\Lambda^2\Lambda^T$ $A^{-2}=V\Lambda V^TV\Lambda V^T=V\Lambda^{-2}\Lambda^T$ \[This is anothe way to see that squaring a matrix squares its eigenvalues without changing its eigenvectors.\]

Given $\Sigma$, we find a symmetric square root $A=\Sigma^{1/2}$:

* compute eigenvector/values of $\Sigma$
* take square root of eigenvalues
* reassemble matrix $A$.

## Anisotropic Gaussians

$X \sim \mathcal{N}\(\mu, \Sigma\)$ $f\(x\) = \frac{1}{\sqrt{\(2\pi\)^d\|\Sigma\|}}\operatorname{exp}\(-\frac{1}{2}\(x-\mu\)^T\Sigma^{-1}\(x-\mu\)\)$ $\Sigma$ is the $d \times d$ SPD covariance matrix. Write $f\(x\)=n\(q\(x\)\)$, where $q\(x\)=\(x-\mu\)^T\Sigma^{-1}\(x-\mu\)=\|\|\Sigma^{-\frac{1}{2}}\(x-\mu\)\|\|\_2^2$. Now $q\(x\)$ is a function —— it's kust a quadratic bowl centered at $\mu$. The other function $n\(\cdot\)$ is a simple, monotonic, convex function, an exponential of the negation of its argument.

Principle: given monotonic $n: \R \rightarrow \R$, isosurfaces of $n\(q\(x\)\)$ are same as $q\(x\)$. This is easy to understand, try to think it bu yourself. $q\(x\)$ is the squared distance from $\Sigma^{-1/2}x$ to $\Sigma^{-1/2}\mu$. Consider the metric: $d\(x,\mu\)=\|\|\Sigma^{-1/2}x-\Sigma^{-1/2}\mu\|\|=\sqrt{\(x-\mu\)^{T}\Sigma^{-1}\(x-\mu\)}=\sqrt{q\(x\)}$.

