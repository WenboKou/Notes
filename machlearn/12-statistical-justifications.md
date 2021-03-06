# 12 Statistical Justifications

Typical model of reality: sample points come from unknown prob. distribution:$X\_i \sim D$ y values are sum of unknown, non-random fn + random noise: $\forall X\_i, \; y\_i = g\(X\_i\) + \epsilon\_i, \; \epsilon\_i \sim D^{'},$ $D^{'}$ has mean zero.

Goal of regression: find $h$ that estimates $g$. Ideal approach: choose $h\(x\)=E\_Y\[Y\|X=x\]=g\(x\)+E\[\epsilon\]=g\(x\)$ \[We can retroactively define g to be this expectation.\]

## Least-Squares Regression from Maximum Likelihood

Suppose $\epsilon\_i \sim N\(0,\sigma^{2}\);y\_i \sim N\(g\(X\_i\),\sigma^2\)$ Recall that log of normal PDF & log likelihood is $lnf\(y\_i\)=-\frac{\(y\_i-\mu\)^2}{2\sigma^2}-constant\Leftarrow\mu = g\(X\_i\)$ $l\(g;X,y\)=ln\(f\(y\_1\)f\(y\_2\)\cdots f\(y\_n\)\)=lnf\(y\_1\)+\cdots + lnf\(y\_n\)=-\frac{1}{2\sigma^2}\sum\(y\_i-g\(X\_i\)\)^2-constant$

Max likelihood on "parameter" g $\Rightarrow$ estimate g by least-squares regression. If the noise is normally distributed, maximum likelihood justifies using the least-squares cost fn.

## Empirical Risk

The risk for hypothesis h is expected loss $R\(h\)=E\[L\]$ over all $x \in \R^d,y\in \R$ Discriminative model: we don't know $X's$ distribution $D$. We are going to approximate the distribution in a crude way: we pretend that the sample pts are the distribution. _Empirical distribution:_ the discrete uniform distribution over the sample pts. _Empirical risk:_ expected loss under empirical distribution

$$
\hat{R}(h)=\frac{1}{n}\sum_{i=1}^{n}L(h(X_i),y_i)
$$

This is why we \[usually\] minimize the sum of loss fns.

## Logistic Loss from Maximum Likelihood

What cost fn should we use for probabilities? Actual probability pt $X$ is in the class is $y_i$; predicted prob. is $h\(X\_i\).$ $\beta$ is big enough to make $y\_i \beta$ and $\(1-y\_i\)\beta$ integers. Likelihood is $L\(h;X,y\)=\prod_{i=1}^nh\(X\_i\)^{y\_i\beta}\(1-h\(X\_i\)\)^{\(1-y\_i\)\beta}$ Log likelihood is $\beta\sum\_i\(y\_ilnh\(X\_i\)+\(1-y\_i\)ln\(1-h\(X\_i\)\)\)= -\beta\sum$ logistic loss fn $L\(h\(X\_i\),y\_i\)$

Max likelihood $\Rightarrow$ minimize $\sum L\(h\(X\_i\),y\_i\)$

## The Bias-Variance Decomposition

There are 2 sources of error in a hypothesis $h$:

_bias:_ error due to inability of hypothesis $h$ to fit $g$ perfectly _variance:_ error due to fitting random noise in data. e.g., we fit linear $g$ with linear $h$, yet $h \not ={g}$.

Model: $X\_i \sim D,\epsilon\_i \sim D^{'},y\_i=g\(X\_i\)+\epsilon\_i,E\[\epsilon\_i\]=0$

Consider arbitrary pt $z \in \R^d$ & $\gamma = g\(z\)+\epsilon$ Note: $E\[\gamma\]=g\(z\);Var\(\gamma\)=Var\(\epsilon\)$

Risk fn when loss = squared error: $$R(h)=E[L(h(z),\gamma)]\\= E[(h(z)-\gamma)^2]\\= E[h(z)^2]+E[\gamma^2]-2E[\gamma h(z)]\\= Var(h(z))+E[h(z)]^2+Var(\gamma)+E[\gamma]^2 - 2E[\gamma]E[h(z)]\\= (E[h(z)]-E[\gamma])^2 + Var(h(z))+Var(\gamma)\\= (E[h(z)]-g(z))^2 + Var(h(z))+Var(\epsilon)$$ $\(E\[h\(z\)\]-g\(z\)\)^2$ is bias$^2$ of method. $Var\(h\(z\)\)$ variance of method. $Var\(\epsilon\)$ irreducible error ?????????????????????????????????????????????????????????????????????

\[a list of consequences of what we've learned.\]

* underfitting = too much bias
* most overfitting caused by too much variance
* training error reflects bias but not variance; test error reflects both
* For many distributions, variance $\rightarrow$ 0 as $n \rightarrow \infty$
* If $h$ can fit $g$ exactly, for many distributions bias $\rightarrow 0$ as $n \rightarrow \infty$
* If $h$ cannot fit $g$ well, bias is large at "most" points
* Adding a good feature reduces bias; adding a bad feature rarely increases it
* Adding a feature usually increases variance \[don't add a feature unless it reduces bias more\]
* Can't reduce irreducible error
* Noise in test set affects only bias & $Var\(\epsilon\)$;noise in training set affects only bias & $Var\(h\)$
* We can't precisely measure bias or variance of real-world data
* But we can test learning algs by choosing $g$ & making synthetic data

I don't know how to prove most of the statements above. Maybe later I will figure it out.

**Example: Least-Squares Linear Reg.** ???????????????????????????????????????????????????????????? ???????????? For simplicity, no fictitious dimension. Model: $g\(z\)=v^T z$ \[We could fit $g$ perfectly with a linear $h$ if not for the noise in the training set.\] Let $e$ be noise $n$-vector, $e\_i \sim \mathcal{N\(0,\sigma^2\)}$ Training labels: $y=Xv+e$, \[$X$ & $y$ are the inputs to linear regression. We don't know $v$ or $e$.\] Lin. reg.computes weights: $\omega = X^{+} y=X^{+}\(X v + e\) = v + X^{+} e$, ??????$X^{+}=\(X^T X\)^{-1}X^T$ \[set the derivative of risk fn to zero\] We want $\omega = v$, but the noise in $y$ becomes noise in $\omega$. BIAS is $E\[h\(z\)\]-g\(z\) = E\[\omega^T z\] - v^T z = E\[z^T X^{+} e\] = z^{T} E\[X\] E\[e\] = 0$ VARIANCE is $\operatorname{Var}\(h\(z\)\)=\operatorname{Var}\(\omega^T z\)=\operatorname{Var}\(z^T X^{+} e\)=\sigma^2 z^T\(X^T X\)^{-1}X^TX\(X^TX\)^{-1} z=\sigma^2 z^TX^TX z$

If we choose coordinate system so $E\[X\]=0$, then $X^T X \rightarrow n\operatorname{Cov}\(D\)$ as $n \rightarrow \infty$, so one can show that for $z \sim D$, \[**Still don't know what is D? What did I miss?**\] $Var\(h\(z\)\) \approx \sigma^2 \frac{d}{n}$. So adding features will increase variance, adding samples will decrease it.

