## Span and linear combinations
We call the set of every possible combination of $\Large a \vec{u} + b\vec{v}$ the span of the $\Large \vec{u}$ and $\Large \vec{v}$.

We call such a combination $\Large a\vec{u} + b\vec{v}$ a linear combination of those two vectors.

#### Linear dependent
Imagine we have 3 vectors: $\Large \vec{u}\quad\vec{v}\quad \vec{w}$
if we can have $\Large \vec{w}=a\vec{u} + b\vec{v}$ for some arbitrary $\Large a,b$ values, then we say that these vectors are linearly dependent, because one of them can be defined as a linear combination of the others.
More accurate definition:
![[3Blue1Brown Course-20261015202515082.webp]]

>A better visual interpretation is to say that, one of the vectors sit on the span space of the others and doesn't add anything new to the span space at all.

![[3Blue1Brown Course-20261015130143504.webp]]

#### Linear independent
A set of vectors is said to be linearly independent if there exists no vector in the set that is equal to a linear combination of the other vectors in the set.

More accurate definition:
![[3Blue1Brown Course-20261015203416602.webp]]

## Linear Transformation
When we linearly transform a vector to some other one, we just need to know the transformed of basis vectors (like $\large \hat{i}, \hat{j}, \dots$) in order to get to the transformation of any $\large \vec{v} = \left(\begin{matrix}x\\y\end{matrix}\right)$:
![[3Blue1Brown Course-20261015161155128.webp]]

![[3Blue1Brown Course-20261015161324692.webp|605]]

![[3Blue1Brown Course-20261015172943846.webp]]

![[3Blue1Brown Course-20261015173018060.webp]]

So for example any linear transformation is only defined my the transformations of basis vectors.
![[3Blue1Brown Course-20261015161524775.webp]]

![[3Blue1Brown Course-20261015161556238.webp]]

![[3Blue1Brown Course-20261015161705337.webp]]

In linear transformations the grid lines remain parallel and evenly spaced while the origin remains fixed.
![[3Blue1Brown Course-20261015162051260.webp]]

## Matrix multiplication
![[3Blue1Brown Course-20261015173507879.webp]]

![[3Blue1Brown Course-20261015173529165.webp]]

>Matrix multiplication shows applying one transformation after another!

## The determinant
What does the determinant of a matrix show?
>We know that a matrix is actually a transformer. A determinant of a matrix actaully shows how much are areas scaled through this transformation.

![[3Blue1Brown Course-20261015201317455.webp]]

For example take a look at the below example:
![[3Blue1Brown Course-20261015201406426.webp]]

![[3Blue1Brown Course-20261015201429907.webp]]

One important example: When the determinant of a transformation is zero, it means that the area of any region will become zero. In this case vectors of the matrix are linearly dependent, so we will see the dimensions of span space get decreased.
![[3Blue1Brown Course-20261015201721890.webp]]

So how does the determinant value of a matrix get negative?
The negative has a meaning:
>In 2d space it means that the orientation has been changed, like flipping the 2d space.
>In 3d space it can be sensed by the right hand rule on 3 basis vectors.

![[3Blue1Brown Course-20261015213657708.webp]]

![[3Blue1Brown Course-20261015213718849.webp]]

>In 3d space the determinant of the matrix shows the volume.

![[3Blue1Brown Course-20261015213752992.webp]]

![[3Blue1Brown Course-20261015213813206.webp]]

![[3Blue1Brown Course-20261015213840735.webp]]

![[3Blue1Brown Course-20261015220606076.webp]]


A zero determinant value in 3d space means that the whole span space has been squished onto something with 0 volume, meaning a flat plane, a line or even a single point.

#### zero determinant
When the determinant value of the transformation matrix is zero, it means that the transformed space or volume has become zero after transformation, so it means that the basis vectors of the matrix aren't linearly independent and has caused a reduction in the dimension of the span space.

![[3Blue1Brown Course-20261015220515390.webp]]

**A useful conclusion**
If we consider a matrix $\Large A_{n\times n}=\left(\begin{matrix}\vec{a_{1}}, \ \vec{a_{2}},\ \dots,\ \vec{a_{d}}\end{matrix}\right)$ and a vector $\Large \vec{v}= \left( \begin{matrix}v_{1}\\v_{2}\\\dots\\v_{n}\end{matrix} \right)$ then the transformed vector of $\Large \vec{v}$ (let's call it $\large \vec{w}$) by matrix $\Large A$ will be: $\Large A.\vec{v}=v_{1}\vec{a_{1}}+v_{2}\vec{a_{2}}+\dots+v_{d}\vec{a_{d}}$
If we want $\Large \vec{w}$ to be zero, there are only two possibilities:
1. The vectors of matrix $\Large A$ are linearly independent and don't cause reduction in the span space dimension. So we for sure know $\Large \det(A) \neq 0$
   In this case the only way for $\Large \vec{w}$ to be zero is that $\Large \vec{v}$ has to be zero itself. Otherwise the considered linear combination can not be zero because the column vectors of $\Large A$ are linearly independent.
2. The vectors of matrix $\Large A$ are linearly dependent and the $\Large \det(A) = 0$
   In this case the $\Large \vec{w}$ will be zero with out any need of $\Large \vec{v}$ being zero.

#### Determinant computation

**Intuition**:
![[3Blue1Brown Course-20261015220702245.webp]]

![[3Blue1Brown Course-20261015220720200.webp]]

![[3Blue1Brown Course-20261015221045560.webp]]

For $\large 3 \times 3$ matrices:
![[3Blue1Brown Course-20261015221146256.webp]]

>The pattern is the same for higher dimensions.

Another interesting point:
![[3Blue1Brown Course-20261015221301164.webp]]

