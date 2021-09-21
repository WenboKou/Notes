# 4 Soft-Margin-SVM

Hard-margin SVMs fail if data not linearly separable. It's also sensitive to outliers. **Draw pic to illustrate this**

## Idea: Allow some points to violate the margin, with slack variables.

$y_i\(X\_i\cdot\omega+\alpha\)\geq1-\xi\_i,\quad\xi\_i\geq 0$ Re-define "margin" to be $\frac{1}{\|\|\omega\|\|}$. To prevent abuse of slack, we add a loss term to objective fn. Optimization problem: Find $\omega,\alpha$ and $\xi\_i$ that minimize $\|\|\omega\|\|^2+C\sum_{i=1}^{n}\xi\_i$ subject to $y\_i\(X\_i\cdot\omega+\alpha\)\geq 1-\xi\_i,\quad \xi\_i\geq 0$ $C\geq0$ is a scalar _regularization hyperparameter_ that trades off:

|  | small $C$ | big $C$ |
| :--- | :--- | :--- |
| desire | maximize margin | keep most slack variables zero or small |
| outliers | less sensitive | very sensitive |
| danger | underfitting\(beacuse slack v can be big\) | overfitting |
| boundary | flat | sinuous |

## Features

Q:How to do nonlinear decision boundaries? A:High-$d$ linear classifier $\rightarrow$ low-$d$ nonlinear classifier.

**Example: The parabolic lifting map** $\Phi$ : $\R \rightarrow \R^{d+1}$ $\Phi\(x\)=\begin{bmatrix} x \|\|x\|\|^2 \end{bmatrix}$ This function lifts $x$ onto paraboloid $x\_{d+1}=\|\|x\|\|^2$. Find a linear classifier in $\Phi$-space. It induces a sphere classifier in $x$-space. Proof: $\|\|x-c\|\|^2&lt;\rho^2 \|\|x\|\|^2 - 2c\cdot x + \|\|c\|\|^2&lt;\rho^2  \begin{bmatrix} -2c^{T}&1 \end{bmatrix} \begin{bmatrix} x \|\|x\|\|^2 \end{bmatrix}&lt;\rho^2-\|\|c\|\|^2 $ $\omega x + \alpha &lt; 0$ means linearly separable. This example implies that we can add more features to get higher dimension. If dataset is linearly separable in high dimension, then it lies in or out of the corresponding geometry in low dimension. The proof is the same.

