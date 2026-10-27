This is the link of the course: [link](https://www.youtube.com/playlist?list=PLE7DDD91010BC51F8)
This course has been taught by the esteemed Professor Gilbert Strang.
![[MIT 18.06 Linear Algebra-20261018153404404.webp]]

## 1. The Geometry of Linear Equations

We can have different pictures while looking at linear equations.
1. Matrix picture
   ![[MIT 18.06 Linear Algebra-20261018152527202.webp]]
2. Row picture
   ![[MIT 18.06 Linear Algebra-20261018152615786.webp]]

3. Column picture: This is the important useful one, in this picture we have a linear combination of vectors.
   ![[MIT 18.06 Linear Algebra-20261018152756078.webp]]

>One Important question: Do the linear combinations of the columns fill 3-D space?

## 2. Elimination with Matrices
By elimination we can find the asnwer of linear equations.
![[MIT 18.06 Linear Algebra-20261018154934639.webp]]

We write the relative matrix:
![[MIT 18.06 Linear Algebra-20261018155102534.webp]]

In elimination, we start from first row, try to find a number and multiply it by the pivot to eliminate x from other rows by subtracting it, then we do the say for y from the second row and consider the row2 col2 cell as the second pivot.

![[MIT 18.06 Linear Algebra-20261018155244070.webp]]

The whole purpose is to get from matrix A to an upper triangle matrix U.

>The pivots can't be zero.

The elimination can also get to failure!
 Some time the pivot get zero, but we can exchange below rows and use below as some none zero pivot, but if that wasn't possible then we will get to failure in elimination. (failure means there are no possible answers for the equation)

We also do the same forward elimination for right handside numbers of the equation too:
![[MIT 18.06 Linear Algebra-20261018162421939.webp]]

#### Back Substitution
In back substitution we solve the equations from below to top by substituting the variables.
![[MIT 18.06 Linear Algebra-20261018162608685.webp]]


#### Matrices
We can multiply matrices like these two ways:
![[MIT 18.06 Linear Algebra-20261018170507465.webp]]

![[MIT 18.06 Linear Algebra-20261018170539154.webp]]


Now we can consider each step of elimination as a matrix multiplication:
Step for $\large E_{21}$
![[MIT 18.06 Linear Algebra-20261018170639334.webp]]

Step for $\large E_{32}$
![[MIT 18.06 Linear Algebra-20261018173319882.webp]]

We can have all these steps of elimination in one matrix:
![[MIT 18.06 Linear Algebra-20261018173457966.webp]]

#### Permutation matrix
We can use them to exchange rows
![[MIT 18.06 Linear Algebra-20261018173747449.webp]]

>What if we want to exchange columns?

Well then we do it like this:
![[MIT 18.06 Linear Algebra-20261018174441461.webp]]

>For column exchange we multiply the matrix on the **right**, but for rows exchanges we do the multiplication to the **left** of the matrix.

#### Inverses
![[MIT 18.06 Linear Algebra-20261018175226345.webp]]