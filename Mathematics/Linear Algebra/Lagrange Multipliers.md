## 1. The Problem

Lagrange multipliers help us find candidate maxima or minima of an objective function subject to a constraint.

For example, optimize \(f(x,y)\) subject to:

$$
\large g(x,y)=c
$$

The constraint restricts us to a curve (or, in higher dimensions, a surface).

## 2. Why Is the Gradient Perpendicular to a Contour?

A contour $(g(x,y)=c)$ contains points where $(g)$ remains constant. If we move a tiny amount along the contour, the change in $(g)$ is zero:

$$
\large dg=\frac{\partial g}{\partial x}dx+\frac{\partial g}{\partial y}dy=0
$$

The gradient is defined as:

$$
\large \nabla g=\left(\frac{\partial g}{\partial x},\frac{\partial g}{\partial y}\right)
$$

Let the infinitesimal displacement be:

$$
\large d\mathbf{r}=(dx,dy)
$$

Using the dot product, we obtain:

$$
\large \nabla g\cdot d\mathbf{r}=0
$$

A zero dot product means the vectors are perpendicular. Therefore, **the gradient \(\nabla g\) is perpendicular to the contour's tangent direction**, provided the contour is smooth and \(\nabla g\neq 0\).

**Intuition:** The gradient points in the direction of the greatest increase of a function. Moving along a contour produces no change in that function.

## 3. Why Does This Lead to Lagrange Multipliers?

At a constrained local optimum, we can only move in directions tangent to the constraint. Since we cannot improve the objective through a sufficiently small feasible movement, the objective's gradient has no component along the constraint's tangent direction.

Thus, at a regular constrained optimum, $(\nabla f)$ is also perpendicular to the constraint. Both gradients are perpendicular to the same tangent direction, so they are parallel:

$$
\large \boxed{\nabla f=\lambda\nabla g}
$$

Here, $(\lambda)$ is the **Lagrange multiplier**, a scalar that makes the two gradients parallel. Some conventions use a minus sign; the method remains unchanged.

For one equality constraint, solve:

$$
\large
\begin{cases}
\nabla f(\mathbf{x})=\lambda\nabla g(\mathbf{x})\\
g(\mathbf{x})=c
\end{cases}
$$

These equations produce candidate points. Compare their objective values and check boundaries or other special cases to determine the actual maximum or minimum.

## 4. Example

Maximize:

$$
\large f(x,y)=xy
$$

subject to:

$$
\large x^2+y^2=1
$$

Define the constraint function:

$$
\large g(x,y)=x^2+y^2
$$

The gradients are:

$$
\large \nabla f=(y,x),\qquad \nabla g=(2x,2y)
$$

Apply the multiplier condition and the constraint:

$$
\large
\begin{cases}
y=2\lambda x\\
x=2\lambda y\\
x^2+y^2=1
\end{cases}
$$

Solving gives two types of candidate points:

$$
\large x=y=\pm\frac{1}{\sqrt{2}}
$$

and

$$
\large x=-y=\pm\frac{1}{\sqrt{2}}
$$

For the maximum:

$$
\large \boxed{f_{\max}=\frac{1}{2}}
$$

For the minimum:

$$
\large \boxed{f_{\min}=-\frac{1}{2}}
$$

## 5. The Lagrangian Formulation

Instead of writing the equations separately, define the Lagrangian:

$$
\large \mathcal{L}(\mathbf{x},\lambda)=f(\mathbf{x})-\lambda\big(g(\mathbf{x})-c\big)
$$

Set its partial derivatives to zero:

$$
\large \nabla_{\mathbf{x}}\mathcal{L}=\nabla f-\lambda\nabla g=0
$$

$$
\large \frac{\partial\mathcal{L}}{\partial\lambda}=-(g(\mathbf{x})-c)=0
$$

The first equation enforces the parallel-gradient condition; the second enforces the original constraint.

The Lagrangian packages both conditions into one system.

## Key Takeaway

**At a constrained optimum, the objective cannot improve along any feasible direction.** This forces its gradient to be normal to the constraint, just like the constraint's own gradient. Therefore:

$$
\large \boxed{\nabla f=\lambda\nabla g}
$$

## Assumptions and Caveats

This argument assumes differentiable functions and a regular constraint, meaning \(\nabla g\neq 0\) at the point.

The equations give necessary conditions, not a guarantee of a maximum or minimum. Candidate points must be checked, and boundaries or singular points must be handled separately.