# Vectors

An important result of linear algebra is that a subspace  $S$ can always be represented as the span of a set of vectors $x_i \in R^n, i=1,\dots,m$, that is, as a set of the form.
$$
S = span(x_1,\cdots,x_m):=\{\sum_{i=1}^m \lambda_ix_i:\lambda\in R^m\}.
$$

**Proof:** Get a nonzero vector from $S$ and get another nonzero vector, repeat the process until all other vectors can be represented by the vectors we already have. Assume these vectors are $x_i,i=1,\dots,m$, their span is $V$. For any vector in $S$, since the vector can be represented by $x_i$, this vector must be in $V$, so $S \subset V$. According to the definition  of space. Any linear combination of the vectors in $S$ still in it which means $V \subset S$. Thus $S = V$.
