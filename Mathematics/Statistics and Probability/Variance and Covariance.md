# Variance and Covariance

> [!summary] Core idea
> **Variance** measures how much a variable spreads around its mean.
>
> **Covariance** measures how two variables vary together relative to their means.
>
> The key relationship:
>
> $$\boxed{\operatorname{Var}(X)=\operatorname{Cov}(X,X)}$$
---

## 1. Why do we need variance?

Suppose we have a random variable $X$.

The **Mean** tells us the center of the distribution:

$$
\mu = E[X]
$$

But the mean doesn't tell us how spread out the values are.

Consider:

$$
A=\{49,50,51,50,50\}
$$

and

$$
B=\{10,90,20,80,50\}
$$

Both have mean:

$$
\mu=50
$$

but their distributions are very different.

So we need a quantity that answers:

> **How much do the values tend to deviate from their mean?**

This is what **variance** measures.

---

# 2. Deviation from the mean

For an observation $x$, its deviation from the mean is:

$$
x-\mu
$$

For example, if:

$$
\mu=50,\qquad x=60
$$

then:

$$
x-\mu=10
$$

If:

$$
x=40
$$

then:

$$
x-\mu=-10
$$

The deviation tells us both:

* **how far** the value is from the mean
* **which direction** it is from the mean

However, there is a problem.

If we take the expected deviation:

$$
E[X-\mu]
$$

we always get zero:

$$
E[X-\mu]
=
E[X]-\mu
=
\mu-\mu
=
0
$$

Positive and negative deviations cancel.

---

# 3. Why square the deviation?

To prevent cancellation, we square the deviation:

$$
(X-\mu)^2
$$

Now both positive and negative deviations become positive:

$$
(-10)^2=100
$$

$$
10^2=100
$$

So both contribute to the amount of variation.

There is another important consequence.

A large deviation receives disproportionately more weight:

$$
2^2=4
$$

while:

$$
10^2=100
$$

Although $10$ is only $5$ times larger than $2$, its squared contribution is $25$ times larger.

So variance also strongly penalizes large deviations.

---

# 4. Variance

The variance of a random variable $X$ is defined as:

$$
\boxed{
\operatorname{Var}(X)=E[(X-\mu_X)^2]
}
$$

where:

$$
\mu_X=E[X]
$$

### Intuition

> **Variance is the expected squared distance from the mean.**

Or more simply:

$$
\boxed{
\text{Variance}
=
\text{average squared deviation from the mean}
}
$$

---

# 5. Example

Suppose:

$$
X=\{48,49,50,51,52\}
$$

The mean is:

$$
\mu=50
$$

The deviations are:

$$
-2,-1,0,1,2
$$

Squaring them:

$$
4,1,0,1,4
$$

Taking their average:

$$
\operatorname{Var}(X)
=
\frac{4+1+0+1+4}{5}
=
2
$$

Therefore:

$$
\boxed{\operatorname{Var}(X)=2}
$$

---

# 6. Alternative formula for variance

Starting from:

$$
\operatorname{Var}(X)=E[(X-\mu)^2]
$$

expand the square:

$$
(X-\mu)^2
=
X^2-2\mu X+\mu^2
$$

Taking expectation:

$$
E[(X-\mu)^2]
=
E[X^2]-2\mu E[X]+\mu^2
$$

Since:

$$
E[X]=\mu
$$

we get:

$$
E[X^2]-2\mu^2+\mu^2
$$

Therefore:

$$
\boxed{
\operatorname{Var}(X)
=
E[X^2]-E[X]^2
}
$$

### Important distinction

$$
E[X^2]
$$

means:

> **Square first, then average.**

While:

$$
E[X]^2
$$

means:

> **Average first, then square.**

Therefore:

$$
\boxed{
\operatorname{Var}(X)
=
\text{average of squares}
-
\text{square of average}
}
$$

---

# 7. What does the magnitude of variance mean?

If:

$$
X_i\approx\mu
$$

then:

$$
(X_i-\mu)^2\approx0
$$

and therefore:

$$
\operatorname{Var}(X)\approx0
$$

So:

$$
\boxed{
\text{small variance}
\Rightarrow
\text{values are concentrated around the mean}
}
$$

Conversely, if the values are widely spread:

$$
|X_i-\mu|\gg0
$$

then:

$$
\operatorname{Var}(X)
$$

becomes large.

Thus:

$$
\boxed{
\text{large variance}
\Rightarrow
\text{values are widely spread around the mean}
}
$$

---

# 8. From variance to covariance

Variance deals with **one variable**.

Now suppose we have two variables:

$$
X=\text{hours studied}
$$

and:

$$
Y=\text{exam score}
$$

We may want to ask:

> When $X$ is above its average, does $Y$ tend to be above its average too?

Or:

> When $X$ is below its average, does $Y$ tend to be below its average?

This is the fundamental intuition behind **covariance**.

---

# 9. Deviations of two variables

Let:

$$
\mu_X=E[X]
$$

and:

$$
\mu_Y=E[Y]
$$

For an observation $(x,y)$, calculate the two deviations:

$$
x-\mu_X
$$

and:

$$
y-\mu_Y
$$

Now multiply them:

$$
(x-\mu_X)(y-\mu_Y)
$$

The sign of this product tells us whether the two variables deviate in the same direction or opposite directions.

---

## 9.1 Both above their means

If:

$$
x-\mu_X>0
$$

and:

$$
y-\mu_Y>0
$$

then:

$$
(x-\mu_X)(y-\mu_Y)>0
$$

because:

$$
\text{positive}\times\text{positive}
=
\text{positive}
$$

---

## 9.2 Both below their means

If:

$$
x-\mu_X<0
$$

and:

$$
y-\mu_Y<0
$$

then:

$$
(x-\mu_X)(y-\mu_Y)>0
$$

because:

$$
\text{negative}\times\text{negative}
=
\text{positive}
$$

So when both variables deviate from their means in the **same direction**, their product is positive.

---

## 9.3 Opposite directions

Suppose:

$$
x-\mu_X>0
$$

but:

$$
y-\mu_Y<0
$$

Then:

$$
(x-\mu_X)(y-\mu_Y)<0
$$

because:

$$
\text{positive}\times\text{negative}
=
\text{negative}
$$

So when one variable is above its mean while the other is below its mean, their product is negative.

---

# 10. Covariance

Covariance is the expected value of these products:

$$
\boxed{
\operatorname{Cov}(X,Y)
=
E[(X-\mu_X)(Y-\mu_Y)]
}
$$

### Intuition

> **Covariance measures whether two variables tend to deviate from their means in the same direction or in opposite directions.**

---

# 11. Positive covariance

Suppose:

$$
\operatorname{Cov}(X,Y)>0
$$

This generally means:

* when $X$ is above its mean, $Y$ tends to be above its mean
* when $X$ is below its mean, $Y$ tends to be below its mean

In other words:

$$
\boxed{
X\uparrow \Rightarrow Y\uparrow
}
$$

in terms of their deviations from their means.

The variables tend to **move together**.

---

# 12. Negative covariance

If:

$$
\operatorname{Cov}(X,Y)<0
$$

then:

* when $X$ is above its mean, $Y$ tends to be below its mean
* when $X$ is below its mean, $Y$ tends to be above its mean

So:

$$
\boxed{
X\uparrow \Rightarrow Y\downarrow
}
$$

relative to their means.

The variables tend to move in **opposite directions**.

---

# 13. Zero covariance

If:

$$
\operatorname{Cov}(X,Y)\approx0
$$

then positive and negative products tend to cancel:

$$
E[(X-\mu_X)(Y-\mu_Y)]\approx0
$$

This means there is little **linear co-movement** between $X$ and $Y$.

> [!warning] Important
> Zero covariance does **not** necessarily mean that $X$ and $Y$ are completely unrelated.
>
> They can have a nonlinear relationship.

For example:

$$
Y=X^2
$$

is clearly a relationship between $X$ and $Y$, but covariance can be zero for certain symmetric distributions.

So covariance primarily captures **linear dependence / co-movement**.

---

# 14. Concrete covariance example

Consider four students:

| Student | Study Hours $X$ | Score $Y$ |
| ------- | --------------: | --------: |
| A       |               2 |        60 |
| B       |               4 |        70 |
| C       |               6 |        80 |
| D       |               8 |        90 |

The means are:

$$
\mu_X=5
$$

and:

$$
\mu_Y=75
$$

Now calculate the deviations:

| Student | $X-\mu_X$ | $Y-\mu_Y$ | Product |
| ------- | --------: | --------: | ------: |
| A       |        -3 |       -15 |      45 |
| B       |        -1 |        -5 |       5 |
| C       |        +1 |        +5 |       5 |
| D       |        +3 |       +15 |      45 |

Every product is positive.

Therefore:

$$
\operatorname{Cov}(X,Y)
=
\frac{45+5+5+45}{4}
=
25
$$

So:

$$
\boxed{\operatorname{Cov}(X,Y)=25}
$$

The variables have positive covariance because they tend to move in the same direction relative to their means.

---

# 15. Geometric intuition

This is one of the most useful ways to understand covariance.

Suppose each observation is a point:

$$
(x_i,y_i)
$$

in a 2D coordinate system.

The center of the data is:

$$
(\mu_X,\mu_Y)
$$

Now shift the coordinate system so that the mean becomes the origin.

Each observation becomes:

$$
(x_i-\mu_X,\;y_i-\mu_Y)
$$

or, as a vector:

$$
\mathbf v_i=
\begin{bmatrix}
x_i-\mu_X\\
y_i-\mu_Y
\end{bmatrix}
$$

Now consider:

$$
(x_i-\mu_X)(y_i-\mu_Y)
$$

This is simply the product of the two coordinates of the centered vector.

Therefore, covariance is asking:

> **When the data is centered around its mean, do the $X$ and $Y$ coordinates tend to have the same sign or opposite signs?**

---

## Positive covariance geometrically

If the data cloud tends to stretch from:

$$
\text{bottom-left}\rightarrow\text{top-right}
$$

then:

$$
\boxed{
\operatorname{Cov}(X,Y)>0
}
$$

The variables tend to increase together.

---

## Negative covariance geometrically

If the data cloud tends to stretch from:

$$
\text{top-left}\rightarrow\text{bottom-right}
$$

then:

$$
\boxed{
\operatorname{Cov}(X,Y)<0
}
$$

The variables tend to move in opposite directions.

---

## Zero covariance geometrically

If the data cloud has no preferred diagonal direction:

$$
\boxed{
\operatorname{Cov}(X,Y)\approx0
}
$$

there is little linear co-movement.

---

# 16. The deepest connection between variance and covariance

Write variance as:

$$
\operatorname{Var}(X)
=
E[(X-\mu_X)(X-\mu_X)]
$$

Compare this with covariance:

$$
\operatorname{Cov}(X,Y)
=
E[(X-\mu_X)(Y-\mu_Y)]
$$

The only difference is that covariance uses two potentially different variables.

Therefore:

$$
\boxed{
\operatorname{Var}(X)
=
\operatorname{Cov}(X,X)
}
$$

This is one of the most important relationships to remember.

> **Variance is self-covariance.**

Covariance is the more general concept.

---

# 17. Covariance matrix

Suppose we have several random variables:

$$
X_1,X_2,X_3
$$

We can calculate covariance between every pair.

This produces the **Covariance Matrix**:

$$
\boxed{
\Sigma=
\begin{bmatrix}
\operatorname{Var}(X_1)&\operatorname{Cov}(X_1,X_2)&\operatorname{Cov}(X_1,X_3)\\
\operatorname{Cov}(X_2,X_1)&\operatorname{Var}(X_2)&\operatorname{Cov}(X_2,X_3)\\
\operatorname{Cov}(X_3,X_1)&\operatorname{Cov}(X_3,X_2)&\operatorname{Var}(X_3)
\end{bmatrix}
}
$$

Notice the diagonal:

$$
\operatorname{Cov}(X_i,X_i)
=
\operatorname{Var}(X_i)
$$

Therefore:

> **Diagonal = individual variance**

and:

> **Off-diagonal = covariance between different variables**

So the covariance matrix tells us both:

1. How much each variable varies individually.
2. How the variables vary together.

---

# 18. Units of variance and covariance

Suppose $X$ is measured in meters:

$$
[X]=m
$$

Because variance squares the deviation:

$$
[\operatorname{Var}(X)]=m^2
$$

So variance has **squared units**.

For covariance:

$$
\operatorname{Cov}(X,Y)
=
E[(X-\mu_X)(Y-\mu_Y)]
$$

Therefore:

$$
\boxed{
[\operatorname{Cov}(X,Y)]
=
[X][Y]
}
$$

For example, if:

* $X$ = height in meters
* $Y$ = weight in kilograms

then:

$$
[\operatorname{Cov}(X,Y)]
=
m\cdot kg
$$

This dependence on units makes raw covariance difficult to compare across different variables.

---

# 19. Standard deviation

Because variance has squared units, we often take its square root.

The **[[Standard Deviation]]** is:

$$
\boxed{
\sigma_X=\sqrt{\operatorname{Var}(X)}
}
$$

For example, if:

$$
\operatorname{Var}(X)=25
$$

then:

$$
\sigma_X=5
$$

Unlike variance, standard deviation has the same units as the original variable.

If $X$ is measured in meters:

$$
[\sigma_X]=m
$$

---

# 20. Correlation

Covariance tells us the direction of linear co-movement, but its magnitude depends on the scales of the variables.

We can normalize covariance using the standard deviations:

$$
\boxed{
\rho_{X,Y}
=
\frac{\operatorname{Cov}(X,Y)}
{\sigma_X\sigma_Y}
}
$$

This is the **[[Correlation]] coefficient**.

It satisfies:

$$
-1\leq\rho_{X,Y}\leq1
$$

Conceptually:

* $\rho>0$ → positive linear relationship
* $\rho<0$ → negative linear relationship
* $\rho\approx0$ → weak linear relationship

Correlation can therefore be viewed as a **normalized covariance**.

---

# 21. Variance vs. covariance

| Concept                | Question                                                            | Formula                                                 |
| ---------------------- | ------------------------------------------------------------------- | ------------------------------------------------------- |
| **Variance**           | How much does $X$ vary around its mean?                             | $\operatorname{Var}(X)=E[(X-\mu_X)^2]$                  |
| **Covariance**         | How do $X$ and $Y$ vary together?                                   | $\operatorname{Cov}(X,Y)=E[(X-\mu_X)(Y-\mu_Y)]$         |
| **Standard deviation** | What is the typical spread in the original units?                   | $\sigma_X=\sqrt{\operatorname{Var}(X)}$                 |
| **Correlation**        | How strongly do $X$ and $Y$ linearly co-vary, independent of scale? | $\rho=\frac{\operatorname{Cov}(X,Y)}{\sigma_X\sigma_Y}$ |

---

# 22. Final mental model

Think of the **mean** as the center of your data.

### Variance asks:

> **How far does one variable spread away from its center?**

$$
\boxed{
\operatorname{Var}(X)
=
E[(X-\mu_X)^2]
}
$$

So:

$$
\boxed{
\text{Variance}
=
\text{spread of one variable}
}
$$

---

### Covariance asks:

> **When one variable moves away from its center, what does another variable tend to do?**

$$
\boxed{
\operatorname{Cov}(X,Y)
=
E[(X-\mu_X)(Y-\mu_Y)]
}
$$

So:

$$
\boxed{
\text{Covariance}
=
\text{co-movement of two variables}
}
$$

---

# 23. The one relationship to remember

The most important connection is:

$$
\boxed{
\operatorname{Var}(X)
=
\operatorname{Cov}(X,X)
}
$$

So you can think of the entire idea as:

$$
\boxed{
\text{Variance}
=
\text{how a variable varies}
}
$$

$$
\boxed{
\text{Covariance}
=
\text{how two variables vary together}
}
$$

Or even more intuitively:

> **Variance asks "How much do I move?"**
>
> **Covariance asks "When I move, does the other variable move with me or against me?"**
