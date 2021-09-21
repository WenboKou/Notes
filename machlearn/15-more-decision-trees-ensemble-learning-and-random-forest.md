# Decision Tree Variations

There are many variations on basic decision trees alg.

## Multivariate Splits

Find non-axis-aligned splits with other classification algs or by generating them randomly. You can use other classification algs such as SVMs, logistic regression, and Gaussian discriminant analysis. Decision trees permit these algs to find more complicated decision boundaries by making them hierarchical. If there are hundreds of features, and you have to check all of them at every level of the tree to classify a point, it slows down classification a lot. So it sometimes pays to consider methods like stepwise selection. Can limit $\#$ of features per split: forward stepwise selection, Lasso.

## Decision Tree Regression

Cost $J\(S\)=\frac{1}{\|S\|}\sum\_{i \in S}\(y\_i - \mu\_s\)^2$, where $\mu\_s$ is the mean label $y\_i$ for sample pts $i \in S$. \[So if all pts in a node have same y-value, then cost is zero.\] \[We choose the split that minimizes the weighted average of the costs of the children after split.\]

## Stopping Early

\[The basic version of the decision tree alg keeps subdividing treenodes until every leaf is pure. We don't have to do that; sometimes we prefer to stop subdividing treenodes earlier.\] Why?

* Limit tree depth\(for speed\)
* Limit tree size\(big data sets\)不懂tree size是什么？
* Complete tree may overfit
* Given noise or overlapping distributions, purity of leaves is counterproductive; better to estimate posterior probs\(不懂这句话什么意思,下面的话可以解释\)

  \[When you have overlapping class distributions, refining the tree down to one sample point per leaf is absolutely guaranteed to overfit. Alternatively, you can use the pts to estimate a posterior probability for each leaf, and return that.\]

How? Select stopping condition\(s\):

* Next split doesn't reduce entropy\error enough\(dangerous; pruning is better\)PS: I think that's because next next split may be better. By pruning we can avoid this situation.
* Most of node's pts\(e.g.,$&gt;95\%$\) have same class
* Node contains few sample pts\(e.g., $&lt;10$\)
* Cell's edges are tiny
* Depth too great \[risky if there are still many pts in the cell\]
* Use validation to compare

Leaves with multiple pts return

* a majority vote or class posterior probs\(classification\) or 
* an average \(regression\).

## Pruning

Grow tree too large; greedily remove each split whose removal improves validation performance. More reliable than stopping early. \[We have to do validation once for each split from bottom to top that we're considering removing. But you can do that cheaply. You keep track of which pts in the validation set end up at each leaf. When you are deciding whether to remove a split, you just look at the validation pts in the two leaves you're thinking of removing, and see how they will be reclassified and how they will change the error rate.\]

\[The reason why pruning often works better than stopping early is because often a split that doesn't seem to make much progress is followed by a split that makes a lot of progress. Pruning is highly recommended when you have enough time to build and prune the tree.\]

## Ensemble Learning

Decision trees are high variance\[Though we can achieve very low bias.\] \[For example, suppose we take a training date set, split it into two halves, and train two decision trees, one on each half of the data. In particular, if the two trees pick different features for the very first split at the top of the tree, then it's quite common for the trees to be completely different. So decision trees tend to have high variance.\]**I don't know how to prove this in math**

\[Let's think how to fix this. As an analogy, imagine that you are generating random numbers from some distribution. If you generate just one number, it might have high variance. But if you generate $n$ random numbers and take their average, the variance is n times smaller. So you might ask yourself, can we reduce the variance of decision tree by taking average of a bunch of decision trees? Yes we can!\]

We call a learning algorithm a weak learner if it does better than guessing randomly. And we combine a bunch of weak learners to get a strong one.

We can take average of output of

* different learning algs
* same learning alg on many training sets
* bagging: same learning alg on many random subsamples of one training set
* random forests: randomized decision trees on random subsamples.

\[These last two are the most common ways to use averaging, because usually we don't have enough training data to use fresh data for every learner. Averaging is not specific to decision trees; it can work with many different learning algorithms. But it works particular well with decision trees.\]

Regression algs: take median or mean output Classification algs: take majority vote OR average posterior probs

## Bagging = Bootstrap AGGreatING

Given $n$ - point training sample, generate random subsample of size $n'$ by sampling with replacement. Some points chosen multiple times; some not chosen. Repeat until $T$ learners. Metalearner takes test point, feeds it into all $T$ learners, returns average/majority output.

## Random Forests

Random sampling isn't random enough! \[With bagging, often the decision trees look very similar. One really strong predictor $\rightarrow$ same feature split at top of every tree. For example, if you're building decision trees to identify spam, the first split might always be "viagra." If the trees are very similar, then taking their average doesn't reduce the variance much.\]

Idea: At each treenode, take random sample of $m$ features\(out of $d$\). Choose best split from $m$ fratures.

