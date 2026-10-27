## Goal

One of the fundamental results of AdaBoost is the following training-error bound:

$$
\boxed{
E_{\mathrm{train}}(H_M)
\leq
\prod_{m=1}^{M}
2\sqrt{\epsilon_m(1-\epsilon_m)}
}
$$

where $\epsilon_m$ is the weighted error of the $m$-th weak learner.

This result explains why the training error can decrease **exponentially fast** when the weak learners are better than random guessing.

We will derive this result using **unnormalized sample weights**. The weights do **not** need to sum to $1$.

---

# 1. Setup

Consider a binary classification problem:

$$
(x_i,y_i),\qquad i=1,\ldots,N
$$

where

$$
y_i\in\{-1,+1\}.
$$

Each weak classifier produces

$$
h_m(x_i)\in\{-1,+1\}.
$$

After $M$ boosting rounds, the additive classifier is

$$
F_M(x)
=
\sum_{m=1}^{M}\alpha_m h_m(x).
$$

The final prediction is

$$
H_M(x)
=
\operatorname{sign}(F_M(x)).
$$

---

# 2. Exponential Loss

AdaBoost can be derived by minimizing the exponential loss

$$
L_M
=
\sum_{i=1}^{N}
e^{-y_iF_M(x_i)}.
$$

Substituting

$$
F_M(x_i)
=
\sum_{m=1}^{M}\alpha_mh_m(x_i),
$$

we obtain

$$
L_M
=
\sum_{i=1}^{N}
e^{-y_i\sum_{m=1}^{M}\alpha_mh_m(x_i)}.
$$

Using

$$
e^{a+b}=e^ae^b,
$$

we get

$$
L_M
=
\sum_{i=1}^{N}
\prod_{m=1}^{M}
e^{-\alpha_my_ih_m(x_i)}.
$$

---

# 3. AdaBoost Sample Weights

Define the sample weights as

$$
\boxed{
w_i^{(1)}=1
}
$$

and, for $m>1$,

$$
\boxed{
w_i^{(m)}
=
e^{-y_iF_{m-1}(x_i)}
}
$$

Therefore,

$$
w_i^{(m+1)}
=
w_i^{(m)}
e^{-\alpha_my_ih_m(x_i)}.
$$

Notice that there is **no requirement that**

$$
\sum_i w_i^{(m)}=1.
$$

The weights are simply positive numbers representing the contribution of each sample to the current exponential loss.

In particular,

$$
w_i^{(M+1)}
=
e^{-y_iF_M(x_i)}.
$$

Therefore,

$$
\boxed{
L_M
=
\sum_{i=1}^{N}w_i^{(M+1)}
}
$$

and the average exponential loss is

$$
\boxed{
\frac{L_M}{N}
=
\frac1N\sum_{i=1}^{N}w_i^{(M+1)}.
}
$$

---

# 4. Relating Training Error to Exponential Loss

The training error is

$$
E_{\mathrm{train}}(H_M)
=
\frac1N
\sum_{i=1}^{N}
\mathbf{1}
\left[
H_M(x_i)\neq y_i
\right].
$$

Consider a misclassified sample.

If

$$
H_M(x_i)\neq y_i,
$$

then

$$
y_iF_M(x_i)\leq0.
$$

Therefore,

$$
-y_iF_M(x_i)\geq0
$$

and hence

$$
e^{-y_iF_M(x_i)}\geq1.
$$

Thus, for every training sample,

$$
\boxed{
\mathbf{1}
\left[
H_M(x_i)\neq y_i
\right]
\leq
e^{-y_iF_M(x_i)}
}
$$

because:

* for a misclassified sample, the right-hand side is at least $1$;
* for a correctly classified sample, the left-hand side is $0$.

Summing over all samples:

$$
E_{\mathrm{train}}(H_M)
\leq
\frac1N
\sum_{i=1}^{N}
e^{-y_iF_M(x_i)}.
$$

Therefore,

$$
\boxed{
E_{\mathrm{train}}(H_M)
\leq
\frac{L_M}{N}
}
$$

So it is enough to find an upper bound on the exponential loss.

---

# 5. How the Total Weight Changes at One Boosting Round

Define the total weight before round $m$ as

$$
W_m
=
\sum_{i=1}^{N}w_i^{(m)}.
$$

Initially,

$$
w_i^{(1)}=1,
$$

so

$$
\boxed{
W_1=N.
}
$$

The weight update is

$$
w_i^{(m+1)}
=
w_i^{(m)}
e^{-\alpha_my_ih_m(x_i)}.
$$

Therefore,

$$
W_{m+1}
=
\sum_{i=1}^{N}
w_i^{(m)}
e^{-\alpha_my_ih_m(x_i)}.
$$

Now separate the samples into correctly and incorrectly classified samples.

---

# 6. Correctly Classified Samples

If $h_m$ correctly classifies sample $i$, then

$$
y_ih_m(x_i)=1.
$$

Therefore,

$$
e^{-\alpha_my_ih_m(x_i)}
=
e^{-\alpha_m}.
$$

Their contribution to $W_{m+1}$ is

$$
e^{-\alpha_m}
\sum_{y_i=h_m(x_i)}
w_i^{(m)}.
$$

---

# 7. Incorrectly Classified Samples

If $h_m$ incorrectly classifies sample $i$, then

$$
y_ih_m(x_i)=-1.
$$

Therefore,

$$
e^{-\alpha_my_ih_m(x_i)}
=
e^{\alpha_m}.
$$

Their contribution is

$$
e^{\alpha_m}
\sum_{y_i\neq h_m(x_i)}
w_i^{(m)}.
$$

Thus,

$$
W_{m+1}
=
e^{-\alpha_m}
\sum_{y_i=h_m(x_i)}
w_i^{(m)}
+
e^{\alpha_m}
\sum_{y_i\neq h_m(x_i)}
w_i^{(m)}.
$$

---

# 8. Introduce the Weighted Error

The weighted error of $h_m$ is defined as

$$
\boxed{
\epsilon_m
=
\frac{
\sum_{y_i\neq h_m(x_i)}
w_i^{(m)}
}{
\sum_{i=1}^{N}w_i^{(m)}
}
}
$$

Since

$$
W_m=\sum_{i=1}^{N}w_i^{(m)},
$$

we have

$$
\sum_{y_i\neq h_m(x_i)}
w_i^{(m)}
=
\epsilon_mW_m.
$$

Similarly,

$$
\sum_{y_i=h_m(x_i)}
w_i^{(m)}
=
(1-\epsilon_m)W_m.
$$

Therefore,

$$
W_{m+1}
=
(1-\epsilon_m)W_me^{-\alpha_m}
+
\epsilon_mW_me^{\alpha_m}.
$$

Factor out $W_m$:

$$
\boxed{
W_{m+1}
=
W_m
\left[
(1-\epsilon_m)e^{-\alpha_m}
+
\epsilon_me^{\alpha_m}
\right].
}
$$

---

# 9. Find the Optimal $\alpha_m$

AdaBoost chooses

$$
\boxed{
\alpha_m
=
\frac12
\ln
\left(
\frac{1-\epsilon_m}{\epsilon_m}
\right)
}
$$

Therefore,

$$
e^{\alpha_m}
=
\sqrt{
\frac{1-\epsilon_m}{\epsilon_m}
}
$$

and

$$
e^{-\alpha_m}
=
\sqrt{
\frac{\epsilon_m}{1-\epsilon_m}
}.
$$

Substitute these into the expression for $W_{m+1}$:

$$
W_{m+1}
=
W_m
\left[
(1-\epsilon_m)
\sqrt{
\frac{\epsilon_m}{1-\epsilon_m}
}
+
\epsilon_m
\sqrt{
\frac{1-\epsilon_m}{\epsilon_m}
}
\right].
$$

Simplify the first term:

$$
(1-\epsilon_m)
\sqrt{
\frac{\epsilon_m}{1-\epsilon_m}
}
=
\sqrt{\epsilon_m(1-\epsilon_m)}.
$$

Similarly,

$$
\epsilon_m
\sqrt{
\frac{1-\epsilon_m}{\epsilon_m}
}
=
\sqrt{\epsilon_m(1-\epsilon_m)}.
$$

Therefore,

$$
W_{m+1}
=
W_m
\left[
2\sqrt{\epsilon_m(1-\epsilon_m)}
\right].
$$

Hence,

$$
\boxed{
W_{m+1}
=
W_m
\,2\sqrt{\epsilon_m(1-\epsilon_m)}
}
$$

This is the key recurrence.

---

# 10. Apply the Recurrence Repeatedly

For the first round,

$$
W_2
=
W_1
\,2\sqrt{\epsilon_1(1-\epsilon_1)}.
$$

For the second round,

$$
W_3
=
W_2
\,2\sqrt{\epsilon_2(1-\epsilon_2)}.
$$

Substituting $W_2$:

$$
W_3
=
W_1
\prod_{m=1}^{2}
2\sqrt{\epsilon_m(1-\epsilon_m)}.
$$

Continuing this process gives

$$
\boxed{
W_{M+1}
=
W_1
\prod_{m=1}^{M}
2\sqrt{\epsilon_m(1-\epsilon_m)}
}
$$

and since

$$
W_1=N,
$$

we obtain

$$
\boxed{
W_{M+1}
=
N
\prod_{m=1}^{M}
2\sqrt{\epsilon_m(1-\epsilon_m)}.
}
$$

But we already established that

$$
W_{M+1}
=
\sum_{i=1}^{N}
e^{-y_iF_M(x_i)}.
$$

Therefore,

$$
\frac1N
\sum_{i=1}^{N}
e^{-y_iF_M(x_i)}
=
\boxed{
\prod_{m=1}^{M}
2\sqrt{\epsilon_m(1-\epsilon_m)}
}.
$$

---

# 11. Final Training-Error Bound

Recall that

$$
E_{\mathrm{train}}(H_M)
\leq
\frac1N
\sum_{i=1}^{N}
e^{-y_iF_M(x_i)}.
$$

From the previous section,

$$
\frac1N
\sum_{i=1}^{N}
e^{-y_iF_M(x_i)}
=
\prod_{m=1}^{M}
2\sqrt{\epsilon_m(1-\epsilon_m)}.
$$

Therefore,

$$
\boxed{
E_{\mathrm{train}}(H_M)
\leq
\prod_{m=1}^{M}
2\sqrt{\epsilon_m(1-\epsilon_m)}
}
$$

This is the desired AdaBoost training-error bound.

---

# 12. Why Does This Decrease Exponentially?

Suppose every weak learner is better than random guessing:

$$
\epsilon_m<\frac12.
$$

Then

$$
2\sqrt{\epsilon_m(1-\epsilon_m)}<1.
$$

Therefore every factor in

$$
\prod_{m=1}^{M}
2\sqrt{\epsilon_m(1-\epsilon_m)}
$$

is smaller than $1$.

For example, suppose every learner has the same weighted error

$$
\epsilon_m=\epsilon<\frac12.
$$

Then

$$
E_{\mathrm{train}}(H_M)
\leq
\left[
2\sqrt{\epsilon(1-\epsilon)}
\right]^M.
$$

Let

$$
c=2\sqrt{\epsilon(1-\epsilon)}.
$$

Since

$$
0<c<1,
$$

we have

$$
E_{\mathrm{train}}(H_M)
\leq c^M.
$$

Since

$$
c^M=e^{M\ln c}
$$

and

$$
\ln c<0,
$$

we can write

$$
\boxed{
E_{\mathrm{train}}(H_M)
\leq
e^{-CM}
}
$$

where

$$
C=-\ln c>0.
$$

Thus the upper bound decreases **exponentially with the number of boosting rounds**.

---

# 13. Important Subtlety: The Bound Is an Upper Bound

The result is

$$
E_{\mathrm{train}}(H_M)
\leq
\prod_{m=1}^{M}
2\sqrt{\epsilon_m(1-\epsilon_m)}.
$$

It does **not** say that the actual training error equals the product.

The product is an upper bound obtained through

$$
\mathbf{1}[H_M(x_i)\neq y_i]
\leq
e^{-y_iF_M(x_i)}.
$$

Therefore the actual training error can be much smaller than the bound.

In particular, it is possible to have

$$
E_{\mathrm{train}}(H_M)=0
$$

while the exponential-loss bound is still strictly positive.

---

# 14. Why $\epsilon_m<0.5$?

The usual AdaBoost weak-learning assumption is

$$
\boxed{
\epsilon_m<\frac12.
}
$$

This gives

$$
\alpha_m
=
\frac12
\ln
\frac{1-\epsilon_m}{\epsilon_m}
>0.
$$

Thus the weak learner receives a positive coefficient in the final ensemble.

At

$$
\epsilon_m=\frac12,
$$

we have

$$
\alpha_m=0
$$

and

$$
2\sqrt{\epsilon_m(1-\epsilon_m)}=1.
$$

Therefore that learner provides no improvement to the bound.

Interestingly, if

$$
\epsilon_m>\frac12,
$$

then

$$
\alpha_m<0.
$$

The factor

$$
2\sqrt{\epsilon_m(1-\epsilon_m)}
$$

is still less than $1$. This is because a learner with error greater than $0.5$ is negatively correlated with the labels and can equivalently be viewed by reversing its predictions.

The conventional weak-learning assumption chooses the orientation for which

$$
\epsilon_m<\frac12
$$

and therefore

$$
\alpha_m>0.
$$

---

# 15. The Entire Proof in One Chain

The whole argument can be compressed into the following chain:

$$
\boxed{
\begin{aligned}
E_{\mathrm{train}}(H_M)
&\leq
\frac1N
\sum_i e^{-y_iF_M(x_i)}
\\[4pt]
&=
\frac{W_{M+1}}{N}
\\[4pt]
&=
\frac{W_1}{N}
\prod_{m=1}^{M}
2\sqrt{\epsilon_m(1-\epsilon_m)}
\\[4pt]
&=
\prod_{m=1}^{M}
2\sqrt{\epsilon_m(1-\epsilon_m)}.
\end{aligned}
}
$$

because

$$
W_1=N.
$$

The crucial recurrence behind the entire result is

$$
\boxed{
W_{m+1}
=
W_m
\,2\sqrt{\epsilon_m(1-\epsilon_m)}.
}
$$

And this recurrence follows directly from the AdaBoost weight update

$$
\boxed{
w_i^{(m+1)}
=
w_i^{(m)}
e^{-\alpha_my_ih_m(x_i)}
}
$$

together with

$$
\boxed{
\alpha_m
=
\frac12
\ln
\frac{1-\epsilon_m}{\epsilon_m}.
}
$$

---

# Key Intuition

The exponential loss has a special property:

$$
e^{-\sum_m y_i\alpha_mh_m(x_i)}
=
\prod_m
e^{-y_i\alpha_mh_m(x_i)}.
$$

Therefore, the effect of adding weak learners becomes **multiplicative** rather than additive.

At every boosting round, the total exponential loss is multiplied by

$$
2\sqrt{\epsilon_m(1-\epsilon_m)}.
$$

If each weak learner has

$$
\epsilon_m<\frac12,
$$

then this multiplier is strictly smaller than $1$.

Repeated multiplication by numbers smaller than $1$ produces exponential decay:

$$
\boxed{
\text{weak learners better than chance}
\quad\Longrightarrow\quad
\text{exponentially decreasing exponential loss}
\quad\Longrightarrow\quad
\text{exponentially decreasing upper bound on training error}.
}
$$
