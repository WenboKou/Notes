### Ridge Regression
Find $\omega$ that minimizes $||X\omega-y||^2 + \lambda||\omega^{'}||^2=J(\omega)$
where $\omega^{'}$ is $\omega$ with component $\alpha$ replaced by 0.
$X$ has fictitious dimension but we DON'T penalize $\alpha$. [**Can you explain why?**]
Adds a regularization term, aka a penalty term, for shrinkage: to encourage small $||\omega^{'}||$. **Why?**
* Guarantees positive definite norm eq'ns; always unique solution.
take derivative of the risk fn and set it equals to 0. 
  * Without penalty. We get:
$X^T X \omega = X^T y$, $X^T X$ is semi pos-definite. this may have multiple solution, especially when features $d$ are more than samples pts $n$
  * With penalty. We gat:
$(X^T X + \lambda I) \omega = X^T y$, $X^T X + \lambda I$ is pos-definite. this only has one unique minimum.


Above is the original motivation, but the next has become more important in machine learning.
* Reduces overfitting by reducing variance. Why?
  Imagine: 500$x_1$ - 500$x_2$ is best for well-separated points with $y_i \in [0,1]$. Small change in $x \Rightarrow$ big change in $y$! If $y$ values in the data are small, it's a sure sign of overfitting So we penalize large weights.
  
**I don't know why $\mathcal{l}_2$ makes variance low mathematically. I think it can be worked out by the same procedure in 12, but I failed. Maybe later I will figure it out.** The following is the answer, don't have to actually compute it.

Setting $\nabla J = 0$ gives normal eq'ns:
$(X^T X + \lambda I)\omega = X^T y$ = $X^T(Xv + e)$ = $X^T X v$ + $X^T e$
$\operatorname{Var}(h(z))=\operatorname{Var}(\omega^T z)=\operatorname{Var}(z^T(X^T X + \lambda I)^{-1}X^T e)$. As $\lambda \rightarrow \infty$, variance $\rightarrow 0$

### Bayesian Justification for Ridge Reg.
Assign a prior probability on $\omega^{'}$: $\omega^{'} \sim \mathcal{N} (0, \sigma^2)$. Apply MLE to the posterior prob.
这块儿我看不懂，先空着吧

### Feature Subset Selection
All features increase variance , but not all features reduce bias.
Idea: 
* Identify poorly predictive features, ignore them(weight zero).
* Less overfitting, smaller test errors.
* 2nd motivation: Inference. Simpler models convey interpretable wisdom.

Alg: Best subset selection. Try all $2^d - 1$ nonempty subsets[every features has a selection between leave it or not] of features.
Obviously, best subset selection isn't feasible if we have a lot of features.

Heuristic 1: Forward stepwise selection.
Start with null model(0 features); repeatedly add best features until validation errors start increasing(due to overfitting) instead of decreasing. At each outer iteration, inner loop tries every features & choose the best by validation. Requires training $O(d^2)$ models.
Not perfect: e.g., won't find the best 2-feature model if neither of those features yields the best 1-features model.

Heuristic 2: Backward stepwise selection.
Start with all $d$ features; repeatedly remove feature whose removal gives best reduction in validation error. Also trains $O(d^2)$ models.

Forward stepwise is a better choice when you suspect only a few features will be good predictors; e.g., spam. Backward stepwise is better when most features are important. If you're lucky, you'll stop early.

### LASSO(Robert Tibshirani, 1996)
Find $\omega$ that minimizes $||X \omega - y||^2 + \lambda ||\omega^{'}||_1$ where $||\omega^{'}||_1 = \sum_{i=1}^d |\omega_i|$
Recall ridge regr.: isosurfaces of $||\omega^{'}||^2$ are hyperspheres. The isosurfaces of $||\omega^{'}||_1$ are cross-polytopes.
Sometimes sets some weights to zero, especially for large $\lambda$.
There are many figures illustrating the features of $l_1$ penalty. Maybe I will add them one day.