# aka Risk Minimization

Multiple sample points with different classes could lie at same point: We want a probabilistic classifier. Suppose 10% of population has cancer, 90% doesn't/

| calories \(X\) | &lt; 1,200 | 1,200-1,600 | &gt;1,600 |
| :--- | :--- | :--- | :--- |
| cancer \(Y=1\) | 20% | 50% | 30% |
| no cancer \(Y=-1\) | 1% | 10% | 89% |

A guy who eating $x=1,400$ calories/day. Guess whether he has cancer? $p\(1,200\leq X \leq 1,600\)=0.5 \times 0.1 + 0.1 \times 0.9 = 0.14$ $P\(Y=1\|X\)=\frac{P\(X\|Y=1\)P\(Y=1\)}{P\(X\)}=\frac{0.05}{0.14}\approx0.64$ $P\(Y=-1\|X\)=\frac{P\(X\|Y=-1\)P\(Y=-1\)}{P\(X\)}=\frac{0.09}{0.14}\approx0.36$ So the guy has bigger chances doesn't have cancer. However, $0.36$ of having cancer is big enough.

A _loss function_ $L\(z,y\)$ specifies badness if classifier predicts $z$, true class is $y$.

E.g.,$$L(z,y)=\begin{cases} 1 \quad if \; z=1,y=-1 \qquad false\;positive\;is\;bad\\ 5 \quad if \; z=-1,y=1 \qquad false\;negative\;is\;BAAAAAD\\ 0 \quad if \; z=y. \end{cases}$$ false positive means someone doesn't have cancer but we diagnosis him as having cancer. This is less serious than false negative, because we cure a normal person won't make this guy die, we miss a sick person may make this guy die.

Defs: loss fn above is _asymmetrical_. the _0-1 loss function_ is 1 for incorrect loss\[symmetrical\], 0 for correct.

Let $r:\R \rightarrow \pm 1$ be _decision rule_, aka _classifier_: a fn that maps a features vector $x$ to 1\(in class\) or -1\(not in class\).

The risk for $r$ if the expected loss over all values of $x,y$:

$$
R(r)=E[L(r(x),Y)]\\
=\sum_{x}(L(r(x),1)P(Y=1|X=x)+L(r(x),-1)P(Y=-1|X=x))P(X=x) \\
=P(Y=1)\sum_{x}L(r(x),1)P(X=x|Y=1)+P(Y=-1)\sum_{x}L(r(x),-1)P(X=x|Y=-1)
$$

The _Bayes decision rule_ aka _Bayes classifier_ is the fn $r^\*$ that minimizes functional $R\(r\)$.

$$
r^*(x)=\begin{cases}
    1 \qquad if L(-1,1)P(Y=1|X=x)>L(1,-1)P(Y=-1|X=x), \\
    -1 \qquad otherwise
\end{cases}
$$

When $L$ is symmetric, pick the class with the biggest posterior probability.

Why this fn minimizes the _Bayes classifier_? Leave this question to you.

In cancer example, $r^_\(x\)=1$ for $x\leq 1,600;r^_\(x\)=-1$ for $x&gt;1,600$. The last expression for risk $R$ gives: $R\(r^_\)=0.1\(5\times 0.3\)+0.9\(1\times 0.01 + 1\times 0.01\)=0.249$ No decision rule gives a lower risk. \*I don't know why it is divided into three segments instead of considering the continuous x_

