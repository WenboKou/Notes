# 20 Unsupervised Learning and Principal Components Analysis

## Unsupervised Learning

We have sample points, but no labels! Goal: Discover structure in the data.

Examples:

* Clustering: partition data into groups of similar/nearby pts.
* Dimensionality reduction
* Density estimation

## Principal Components Analysis\(PCA\)\(Karl Pearson, 1901\)

Goal: Given sample pts in $\R^d$, find $k$ directions that capture most of the variation. \(Dimensionality reduction\)

Why?

* Reducing \# of dimensions makes some computations cheaper, e.g., regression.
* Remove irrelevant dimensions to reduce overfitting in learning algs.
* Find a small basis for representing variations in complex things, e.g., faces, genes.

Let $X$ be $n \times d$ design matrix. \[No fictitious dimension.\] From now on, assume $X$ is centered: $\mu\_X = 0$

Let $\omega$ be a unit vector. The orthogonal projection of point $x$ onto vector $\omega$ is $\hat{x} = \(x\cdot\omega\)\omega$. If $\omega$ not unit, $\hat{x}=\frac{x \cdot \omega}{\|\|\omega\|\|^2}\omega$. Given orthonormal directions $v_1,\ldots,v\_k,\hat{x}=\sum_{i=1}^k\(x\cdot v\_i\)v\_i$.

Often we want just the $k$ principal coordinates $x\cdot v\_i$ in principal component space. $X^TX$ is square, symmetric, positive semidefinite, $d\times d$ matrix. \[Symmetric, eigenvalues are real.\] Let $0 \leq \lambda\_1 \leq \lambda\_2 \ldots \leq \lambda\_d$ be its eigenvalues. \[sorted\]. Let $v\_1,v\_2,\ldots,v\_d$ be corresponding orthogonal unit eigenvectors. These are the principal components.

PCA derivation 1: Fit a Gaussian to data with maximum likelihood estimation. Choose $k$ Gaussian axes of greatest variance.

Recall that MLE estimates a covariance matrix $\hat{\sum}=\frac{1}{n}X^TX$. \[Presuming $X$ is centered.\]

PCA Alg:

* Center $X$.
* Optional: Normalize $X$. Units of measurement different?
  * Yes: Normalize.
  * No: Usually don't.
* Compute unit eigenvectors/values of $X^TX$.
* Optional: choose $k$ based on the eigenvalue sizes.
* For the best $k$-dimensional subspace, pick eigenvectors $v\_{d-k+1},\ldots,v\_d$.
* Compute the principal coordinates $x \cdot v\_i$ of training/test data.\[Remember to un-center the input training data or translate the test data the same way we translate the training data.\]

\[If you are using PCA as a preprocess for a supervised learning alg, there's a more effective way to choose $k$: \(cross-\)validation.\] 我不知道这到底解释了个啥，感觉只是给出了步骤。是省略了什么负责的数学吗？希望以后的学习中能理解。

PCA derivation 2:

