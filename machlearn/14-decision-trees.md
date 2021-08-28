# 14 Decision Trees

Nonlinear method for classification and regression.

Let $S \sube {1, 2, \ldots,n}$ be set of sample point indices. Top-level call: $S = {1, 2, \ldots, n}$. GrowTree\($S$\)

* if \($y\_i = C$ for all $i \in S$ and some class $C$\) then {
  * return new leaf\($C$\)
* } else {
  * choose best splitting feature $j$ and splitting value $\beta$
  * $S_l = {i\in S:X_{ij}\leq\beta}$
  * $S_r = {i\in S:X_{ij}&gt;\beta}$
  * return new node\($j$,$\beta$, GrowTree\(S\_l\), GrowTree\($S\_r$\)\)
* }

How to choose best split?

* Try all splits.\[All splits within a feature and all features.\]
* For a set $S$, let $J\(S\)$ be the cost of $S$.
* Choose the split that minimizes $J\(S\_l\) + J\(S\_r\)$ or the split that minimizes weighted average $\frac{\|S\_l\|J\(S\_l\)+\|S\_r\|J\(S\_r\)}{\|S\_l\|+\|S\_r\|}$

How to choose cost $J\(S\)$? Idea 1\(bad\): Label $S$ with the class $C$ that labels the most pts in $S$. $J\(S\) \leftarrow \#$ of points in $S$ not in class $C$. $S$: 20C 10D $\rightarrow$ $S\_l$: 10C 9D $J\(S\_l\)=9$; $S\_r$: 10C 1D $J\(S\_r\)=1$ $S$: 20C 10D $\rightarrow$ $S\_l$: 10C 5D $J\(S\_l\)=5$; $S\_r$: 10C 5D $J\(S\_r\)=5$ Problem:$J\(S\_l\) + J\(S\_r\) = 10$ for both splits, but left split much better. Weighted avg prefers right split! \[There are many different splits that all have the same total cost. We want a cost function that better distinguishes between them.\]

Idea2\(good\): Measure the entropy. Let $Y$ be a random class variable, and suppose $P\(Y=C\)=p\_c$. The surprise of $Y$ being class $C$ is $-\operatorname{log}\_2p\_c$

* 1 gives us zero surprise.
* 0 gives us infinite surprise!

The entropy of an index set $S$ is the average surprise

$$
H(S) = -\sum_{C}p_c\operatorname{log}_2p_c\quad p_c = \frac{|\{i\in S:y_i=C\}|}{|S|}
$$

\[The proportion of pts in $S$ that are in class $C$\] If all pts in $S$ belong to same class? $H\(S\) = -1\operatorname{log}\_2 1 =0$. Half class $C$, half class $D$? $H\(S\) = -0.5\operatorname{log}\_2{0.5}=1$. $n$ pts, all different classes? $H\(S\) = -\operatorname{log}\_2{\frac{1}{n}}$.

When there are only two classes. The probability of the second class is $p\_D=1-p\_C$, so we can plot the entropy with just one dependent variable. It's concave. If you have $&gt; 2$ classes, you would need a multidimensional chart to plot the entropy, but it's still strictly concave.

Weighted avg entropy after split is $H_{\operatorname{after}}=\frac{\|S\_l\|H\(S\_l\)+\|S\_r\|H\(S\_r\)}{\|S\_l\|+\|S\_r\|}$. Choose split that maximizes information gain $H\(S\)-H_{\operatorname{after}}$ Info gain always positive except when one child is empty or for all $C$, $P\(y\_i=C\|i\in S\_l\)=P\(y\_i=C\|i\in S\_r\)$. **There is a figure illustrated why info gain is positive except ..., May be one day add this figure**

If $x\_i$ is quantitative: sort $x\_i$ values in $S$; try splitting between each pair of _unequal_ consecutive values.\[We can radix sort the pts in linear time\] Clear bit: As you scan sorted list from left to right, you can update entropy in $O\(1\)$ time per pt!\[**There is a figure illustrated this.**\]

Running time analysis:**不知道是不是还没理解这个算法，没看懂，以后补上吧**

