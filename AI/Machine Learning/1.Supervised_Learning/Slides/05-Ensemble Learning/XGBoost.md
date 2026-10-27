## 1. Main Idea

XGBoost builds an additive model consisting of decision trees.

$$
\large
\hat{y}_i^{(t)}
=
\hat{y}_i^{(t-1)}
+
\eta f_t(x_i)
$$

where:

* $f_t$ is the new decision tree.
* $\eta$ is the learning rate.
* $\hat{y}_i^{(t-1)}$ is the prediction before adding the new tree.

Therefore, each new tree is essentially learning a **correction to the current predictions**.

---

# 2. Objective Function

At iteration $t$, XGBoost minimizes:

$$
\large
\mathcal{L}^{(t)}
=
\sum_{i=1}^{n}
l\left(y_i,\hat{y}_i^{(t-1)}+f_t(x_i)\right)
+
\Omega(f_t)
$$

where:

* $l(y_i,\hat y_i)$ is the training loss.
* $\Omega(f_t)$ is the regularization term for the new tree.

The regularization term is:

$$
\large
\Omega(f_t)
=
\gamma T
+
\frac{1}{2}\lambda\sum_{j=1}^{T}w_j^2
$$

where:

* $T$ = number of leaves.
* $w_j$ = value assigned to leaf $j$.
* $\gamma$ = penalty for creating additional leaves.
* $\lambda$ = L2 regularization on leaf values.

---

# 3. Second-Order Taylor Approximation

Let the current prediction be

$$
\large
\hat y_i=\hat y_i^{(t-1)}.
$$

Define the gradient:

$$
\large
g_i
=
\frac{\partial l(y_i,\hat y_i)}
{\partial \hat y_i}
$$

and the Hessian:

$$
\large
h_i
=
\frac{\partial^2 l(y_i,\hat y_i)}
{\partial \hat y_i^2}.
$$

XGBoost approximates the loss after adding $f_t(x_i)$ using a second-order Taylor expansion:

$$
\large
l(y_i,\hat y_i+f_t(x_i))
\approx
l(y_i,\hat y_i)
+
g_i f_t(x_i)
+
\frac{1}{2}h_i f_t(x_i)^2.
$$

The first term, $l(y_i,\hat y_i)$, does not depend on the new tree, so it can be ignored when optimizing the new tree.

Therefore, the simplified objective is:

$$
\large
\tilde{\mathcal L}^{(t)}
=
\sum_{i=1}^{n}
\left[
g_i f_t(x_i)
+
\frac12 h_i f_t(x_i)^2
\right]
+
\Omega(f_t).
$$

---

# 4. Representing the Tree

Suppose the tree has $T$ leaves.

Each sample is assigned to exactly one leaf, and every sample belonging to leaf $j$ receives the same value $w_j$.

Let

$$
\large
I_j
=
\{i:\text{sample }i\text{ belongs to leaf }j\}.
$$

Therefore,

$$
\large
f_t(x_i)=w_j
\qquad
\text{if }i\in I_j.
$$

Define the sum of gradients and Hessians in leaf $j$:

$$
\large
G_j
=
\sum_{i\in I_j}g_i
$$

$$
\large
H_j
=
\sum_{i\in I_j}h_i.
$$

The objective can then be grouped by leaves:

$$
\large
\tilde{\mathcal L}^{(t)}
=
\sum_{j=1}^{T}
\left[
G_jw_j
+
\frac12H_jw_j^2
\right]
+
\gamma T
+
\frac12\lambda\sum_{j=1}^{T}w_j^2.
$$

Combining the quadratic terms:

$$
\large
\boxed{
\tilde{\mathcal L}^{(t)}
=
\sum_{j=1}^{T}
\left[
G_jw_j
+
\frac12(H_j+\lambda)w_j^2
\right]
+
\gamma T
}
$$

This is the key expression used to derive the optimal leaf values and split criterion.

---

# 5. Optimal Value of a Leaf

For a fixed tree structure, consider one leaf:

$$
\large
F_j(w_j)
=
G_jw_j
+
\frac12(H_j+\lambda)w_j^2.
$$

To find its optimal value, differentiate with respect to $w_j$:

$$
\large
\frac{\partial F_j}{\partial w_j}
=
G_j+(H_j+\lambda)w_j.
$$

Set the derivative to zero:

$$
\large
G_j+(H_j+\lambda)w_j=0.
$$

Therefore:

$$
\large
\boxed{
w_j^*
=
-\frac{G_j}{H_j+\lambda}
}
$$

This is the **optimal value assigned to leaf $j$**.

It tells us the best prediction/update that this leaf should produce according to the current gradients and Hessians, while considering L2 regularization.

---

# 6. Optimal Contribution of a Leaf

The optimal leaf value $w_j^*$ is **not** the same thing as the optimal contribution.

The objective contribution of leaf $j$ is:

$$
\large
F_j(w_j)
=
G_jw_j
+
\frac12(H_j+\lambda)w_j^2.
$$

Now substitute the optimal value:

$$
\large
w_j^*
=
-\frac{G_j}{H_j+\lambda}.
$$

Therefore:

$$
\large
F_j(w_j^*)
=
G_j
\left(
-\frac{G_j}{H_j+\lambda}
\right)
+
\frac12(H_j+\lambda)
\left(
\frac{G_j^2}{(H_j+\lambda)^2}
\right).
$$

Simplifying:

$$
\large
\boxed{
F_j(w_j^*)
=
-\frac12
\frac{G_j^2}{H_j+\lambda}
}
$$

This is the **optimal contribution of the leaf** to the objective.

### Important distinction

The optimal leaf value is:

$$
\large
\boxed{
w_j^*
=
-\frac{G_j}{H_j+\lambda}
}
$$

whereas the optimal objective contribution is:

$$
\large
\boxed{
-\frac12\frac{G_j^2}{H_j+\lambda}
}
$$

The $G_j^2$ appears because we substitute the optimal $w_j^*$ back into a quadratic function.

---

# 7. Optimal Contribution of a Node

The same mathematics applies to a node before it is split.

For a node containing samples $I$, define:

$$
\large
G=\sum_{i\in I}g_i
$$

and

$$
\large
H=\sum_{i\in I}h_i.
$$

If the node becomes a leaf, its optimal value is:

$$
\large
\boxed{
w^*
=
-\frac{G}{H+\lambda}
}
$$

and its optimal objective contribution is:

$$
\large
\boxed{
-\frac12\frac{G^2}{H+\lambda}
}
$$

So the **optimal contribution of a node** means:

> The minimum value that this node contributes to the regularized objective when it is given its optimal leaf value.

It is **not another prediction value**.

---

# 8. How XGBoost Chooses a Split

Suppose a node is split into a left child and a right child.

For the parent:

$$
\large
G=G_L+G_R
$$

$$
\large
H=H_L+H_R.
$$

The optimal contribution before splitting is:

$$
\large
-\frac12
\frac{G^2}{H+\lambda}.
$$

After splitting, the two children have optimal contributions:

$$
\large
-\frac12
\frac{G_L^2}{H_L+\lambda}
$$

and

$$
\large
-\frac12
\frac{G_R^2}{H_R+\lambda}.
$$

Because creating an additional leaf costs $\gamma$, the split gain is:

$$
\large
\boxed{
\text{Gain}
=
\frac12
\left(
\frac{G_L^2}{H_L+\lambda}
+
\frac{G_R^2}{H_R+\lambda}
-
\frac{G^2}{H+\lambda}
\right)
-\gamma
}
$$

XGBoost searches for the feature and threshold that produce the largest gain.

---

# 9. Role of $\gamma$

The term

$$
\large
\gamma T
$$

penalizes the number of leaves.

Every additional leaf costs:

$$
\large
\boxed{\gamma}
$$

Therefore, when considering a split, XGBoost effectively asks:

$$
\large
\boxed{
\text{Is the improvement produced by this split greater than }\gamma?
}
$$

If:

$$
\large
\text{Gain}>0
$$

the split improves the regularized objective and is worthwhile.

If:

$$
\large
\text{Gain}\leq0
$$

the split is not worthwhile.

Therefore:

$$
\large
\gamma\uparrow
\quad\Longrightarrow\quad
\text{splits become harder to justify}
$$

and consequently:

$$
\large
\gamma\uparrow
\quad\Longrightarrow\quad
\text{simpler trees and stronger regularization}.
$$

---

# 10. Role of $\lambda$

The parameter $\lambda$ controls the L2 penalty on leaf values:

$$
\large
\frac12\lambda\sum_jw_j^2.
$$

It appears directly in the optimal leaf value:

$$
\large
w_j^*
=
-\frac{G_j}{H_j+\lambda}.
$$

Increasing $\lambda$ makes the denominator larger:

$$
\large
\lambda\uparrow
\quad\Longrightarrow\quad
|w_j^*|\downarrow.
$$

Thus, $\lambda$ discourages large leaf predictions/updates.

It also affects the split gain through:

$$
\large
\frac{G_j^2}{H_j+\lambda}.
$$

Therefore, $\lambda$ regularizes both **leaf values** and the **attractiveness of splits**.

---

# 11. Simple Example: Squared Error

For regression with squared-error loss:

$$
\large
l(y_i,\hat y_i)
=
\frac12(y_i-\hat y_i)^2.
$$

The gradient is:

$$
\large
g_i
=
\hat y_i-y_i
$$

and the Hessian is:

$$
\large
h_i=1.
$$

Therefore:

$$
\large
G_j
=
\sum_{i\in I_j}(\hat y_i-y_i)
$$

and

$$
\large
H_j=|I_j|.
$$

The optimal leaf value becomes:

$$
\large
\boxed{
w_j^*
=
-\frac{\sum_{i\in I_j}(\hat y_i-y_i)}
{|I_j|+\lambda}
}
$$

or equivalently:

$$
\large
\boxed{
w_j^*
=
\frac{\sum_{i\in I_j}(y_i-\hat y_i)}
{|I_j|+\lambda}
}
$$

So for squared-error regression, the new tree is learning **corrections to the current predictions**.

---

# 12. Overall Picture

At each boosting iteration:

$$
\large
\boxed{
\text{Current predictions}
\rightarrow
g_i,h_i
\rightarrow
\text{find best tree splits}
\rightarrow
w_j^*
\rightarrow
\text{add tree}
}
$$

More mathematically:

### Step 1 — Calculate derivatives

$$
\large
g_i=
\frac{\partial l}{\partial\hat y_i},
\qquad
h_i=
\frac{\partial^2l}{\partial\hat y_i^2}.
$$

### Step 2 — Evaluate possible splits

Using:

$$
\large
\text{Gain}
=
\frac12
\left(
\frac{G_L^2}{H_L+\lambda}
+
\frac{G_R^2}{H_R+\lambda}
-
\frac{G^2}{H+\lambda}
\right)
-\gamma.
$$

### Step 3 — Choose the best tree structure

Choose splits that maximize the regularized gain.

### Step 4 — Calculate each leaf's optimal value

$$
\large
\boxed{
w_j^*
=
-\frac{G_j}{H_j+\lambda}
}
$$

### Step 5 — Add the tree

$$
\large
\boxed{
\hat y_i^{(t)}
=
\hat y_i^{(t-1)}
+
\eta f_t(x_i)
}
$$

and repeat.

---

# Core Formulas to Remember

$$
\large
\boxed{
\hat y_i^{(t)}
=
\hat y_i^{(t-1)}
+
\eta f_t(x_i)
}
$$

$$
\large
\boxed{
G_j=\sum_{i\in I_j}g_i,
\qquad
H_j=\sum_{i\in I_j}h_i
}
$$

$$
\large
\boxed{
w_j^*
=
-\frac{G_j}{H_j+\lambda}
}
$$

$$
\large
\boxed{
\text{Optimal contribution}
=
-\frac12
\frac{G_j^2}{H_j+\lambda}
}
$$

$$
\large
\boxed{
\text{Gain}
=
\frac12
\left(
\frac{G_L^2}{H_L+\lambda}
+
\frac{G_R^2}{H_R+\lambda}
-
\frac{G^2}{H+\lambda}
\right)
-\gamma
}
$$

$$
\large
\boxed{
\Omega(f_t)
=
\gamma T+
\frac12\lambda\sum_jw_j^2
}
$$

The central idea is:

$$
\large
\boxed{
\text{XGBoost finds the tree that gives the largest regularized improvement}
}
$$

using both the **gradient** and **Hessian** of the loss.
