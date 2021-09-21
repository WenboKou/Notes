# 9 Gaussian-Discriminant-Analysis

Assumption: Each class comes from normal distribution\(Gaussian\) $X \sim N\(\mu, \sigma^2\): f\(x\)=\frac{1}{\(\sqrt{2\pi\sigma}\)^d}e^{-\frac{\|\|x-\mu\|\|^2}{2\sigma^2}}$. Suppose for each class $C$ prior $\pi_C = P\(Y=C\)$. Given $x$, Bayes decisions rule $r^\*\(x\)$ predicts class $C$ that maximizes $f\(X=x\|Y=C\)\pi\_C$.\(minimize the risk function. the maximum value is the true value, then we can eliminate it in the risk function.\) It is equivalent to maximize $Q\_c\(x\)=ln\(\(\sqrt{2\pi}\)^df\_C\(x\)\pi_{C}\)=-\frac{\|\|x-\mu\_{C}\|\|^2}{2\sigma^2\_C}-dln\sigma\_C+ln\pi\_C$. We can incorporate the asymmetrical loss function the same way we incorporate the prior $\pi\_C$.

## Quadratic Discriminant Analysis\(QDA\)

Suppose only 2 class C,D. Then

$$
r^*=\begin{cases}
    C \quad if\; Q_C(x)-Q_D(x)>0\\
    D \quad otherwise.
\end{cases}
$$

\[Our goal is always to minimize the risk function, thus choose the right class when the weighted posterior estimation is bigger\]

One of the great things about QDA is that we can determine the probability that the classification is correct. Use Bayes in 2-class case. $P\(Y=C\|X\)=\frac{f\(X\|Y=C\)\pi\_C}{f\(X\|Y=C\)\pi\_Cf\(X\|Y=D\)\pi\_D}$ $P\(Y=C\|X=x\)=\frac{e^{Q\_C{\(x\)}}}{e^{Q\_C{\(x\)}}+e^{Q\_D{\(x\)}}}=\frac{1}{1+e^{Q\_D{\(x\)}-Q\_C{\(x\)}}}$ $s\(\gamma\)=\frac{1}{1+e^{-\gamma}}$ this is logistic fn aka sigmoid fn. $Q\_C{\(x\)}-Q\_D{\(x\)}$ is the decision fn.

**I still don't understand how to determine the probability? Guess: change the parameters My guess is right. Since we are computing probability.**

## Linear Discriminant Analysis\(LDA\)

\[LDA is a variant of QDA with linear decision boundaries. It's less likely to overfit than QDA.\] $Q\_C\(x\)-Q\_D\(x\)=\frac{\(\mu\_C-\mu\_D\)\cdot x}{\sigma^2}-\frac{\|\|\mu\_C\|\|^2-\|\|\mu\_D\|\|^2}{2\sigma^2}+ln\pi\_C-ln\pi\_D$ This can be written as $\omega\cdot x+\alpha$. It's a linear classifier! Choose C that maximizes linear discriminant fn $\frac{\mu\_C\cdot x}{\sigma^2}-\frac{\|\|\mu\_C\|\|^2}{2\sigma^2}+ln\pi\_C$ In 2-class case: decision boundary is $\omega \cdot x + \alpha=0$ posterior is $P\(Y=C\|X=x\)=s\(\omega \cdot x + \alpha\)$ The effort of $\omega \cdot x + \alpha$ is to scale and translate the sigmoid fn.

## MAXIMUM LIKELIHOOD ESTIMATION OF PARAMETERS

To use Gaussian discriminant analysis, we must first fit Gaussians to the sample points and estimate the class prior probabilities.

For QDA: estimate $\hat\mu$ and $\hat\sigma$ for each class separately and estimate the priors: $\hat\pi\_C = \frac{n\_C}{\sum\_Dn\_D}$ total sample points in all class.

For LDA: same means and priors as previous; one variance for all classes: $\hat\sigma^2 = \frac{1}{dn}\sum_C\sum_{i:y\_i=C}\|\|X\_i-\hat\mu\_C\|\|^{2}$.

