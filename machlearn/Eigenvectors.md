Theorem:
if $v$ is eigenvector of A eigenvalue $\lambda$,
then $v$ is eigenvector of $A^k$ eigenvalue of  $\lambda^k$.

Theorem:
if A is invertible, then $v$ is eigenvector of $A^{-1}$ eigenvalue $\frac{1}{\lambda}$

Spectral Theorem: every real, symmetric $n\times n$ matrix has real eigenvalues and $n$ eigenvectors that are mutually orthogonal.

**Quadratic Forms**
$||z||^2=z^Tz$ $\leftarrow$ quadratic; isosurfaces are spheres.
$||A^{-1}x||^2=x^{T}A^{-2}x$$\leftarrow$ quadratic of $A^{-2}$; isosurfaces are ellipsoids.
This is quite easy to understand, let's say that the z axis is the module of the vector $x$, using the plane with different height to cut, let's say the height is 2, we get $||z||^2=1$, this is a sphere. $A^{-1}x$ means we stretched the whole coordinate along some axises. Let's say along the original $x_1, x_2$ axises. For height equals 1 we get $||A^{-1}x||=||(ax_1,bx_2)^T||^2=1$, this is ellipsoid.

[The matrix $A$ maps the circle on the left to the ellipses on the right. They're stretching along the direction with eigenvalue 2, and shrinking along the direction with eigenvalue -1/2.]

Special case: $A$ is diagonal $\leftrightarrow$ eigenvectors are coordinate axes , ellipsoids are axis-aligned.

A symmetric matrix $M$ is *positive definite* if $\omega^T M \omega > 0$ for all $\omega \neq 0 \leftrightarrow$ eigenvalues positive.
... is *positive semidefinite* if $\omega^T M \omega \geq 0$ for all $\omega \leftrightarrow$ all eigenvalues nonnegative
... is *indefinite* if there are positive eigenvalue and negative eigenvalue.
... invertible if no zero eigenvalue.
We can analyze the shape of $||A^{-1}x||$ for the above cases.

**Building a Quadratic**
[Suppose you have an ellipsoid isosurface in mind. Suppose you pick the ellipsoid axes and the radius along each axis, and you want to create the matrix whose quadratic form will have isosurffaces matching the ellipsoid of your dreams.]

Choose n mutually orthogonal unit n-vectors $v1,\cdots,v_n$. Let $V=[v_1\;v_2\;\cdots\;v_n]$[This is a $n\times n$ matrix]
Observe: $V^TV=I\rightarrow V^T=V^{-1}\rightarrow VV^{T}=I$

Choose some radii $\lambda_i$:
Let $\Lambda=\begin{bmatrix}
    \lambda_1 & 0 & \cdots & 0\\
    0 & \lambda_2 & \cdots & 0\\
     \cdots \\
    0 & 0 & \cdots & \lambda_n\\
\end{bmatrix}$

Define "eigenvectors" $AV=V\Lambda\Rightarrow AVV^T=V\Lambda V^T\Rightarrow A=V\Lambda V^T=\sum_{i=1}^n\lambda_iv_iv_i^T$

Observe:$A^2=V\Lambda V^TV\Lambda V^T=V\Lambda^2\Lambda^T$
$A^{-2}=V\Lambda V^TV\Lambda V^T=V\Lambda^{-2}\Lambda^T$
[This is anothe way to see that squaring a matrix squares its eigenvalues without changing its eigenvectors.]

Given $\Sigma$, we find a symmetric square root $A=\Sigma^{1/2}$:
compute eigenvector/values of $\Sigma$
take square root of eigenvalues
reassemble matrix $A$.