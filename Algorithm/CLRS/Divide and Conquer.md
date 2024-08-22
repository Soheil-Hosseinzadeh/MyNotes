## Chapter 4

The divide-and-conquer method is a powerful strategy for designing asymptotically efficient algorithms.

> Merge sort is an example of divide and conquer algorithms

In Divide and conquer, you solve a given problem (instance) recursively. If the problem is small enough`(the base case)` you just solve it directly without recursing. Otherwise `(the recursive case)` you perform three characteristic steps:
1. `Divide`: divide the main problem into subproblems.
2. `Conquer`: conquer the subproblems by solving them recursively.
3. `Combine`: combine the subproblem solutions to form a solution to the main problem.
> The recursion in **Conquer** state bottoms out when it reaches a base case and the subproblem is small enough to solve directly.


## Recurrences
recurrence is an equation that describes a function in terms of its value on other, typically smaller, arguments.

> The recurrence is **WELL DEFINED** if there is at least one function that satisfies it, and **ILL DEFINED** otherwise.


## Algorithmic recurrences

![[Algorithmic Recurrences.png]]

first property means there exist constants c1, c2 so that:

$$
0 \lt c_1 \leq T(n) \leq c_2
$$
 for: $$n\lt n_0$$
 > The running time of the algorithm may not be defined for some values of n if there are no legal inputs of that size, but it must be defined for at least one, or else the algorithm doesn't solve any problem.


## Conventions for recurrences

> Whenever a recurrence is stated without and explicit base case, we assume that the recurrence is algorithmic.

## Solving Recurrences in chapter 4
1. **Substitution method** : guessing the form of a bound and using mathematical induction to prove the guess.
2. **Recursion-tree method**
3. **Master method**
4. **Akra-Bazzi method**
---
## 4.1 : Multiplying square matrices

$$
\Large C = A\cdot B
$$
so that : 
$$
\Large c_{ij} = \sum_{k=1}^{n} a_{ik}\times b_{kj}
$$
**two types of matrices :**
1. `dense`: A dense matrix is one where most of its elements are non-zero. In other words, it has a high density of non-zero elements relative to its total size.

> Dense matrices typically require storage for every element, even if it's zero, and operations on dense matrices involve iterating over all elements.

2. `sparse`: A sparse matrix is one where most of its elements are zero. It has a low density of non-zero elements relative to its total size.

>Sparse matrices are advantageous in terms of storage efficiency because they only store the non-zero elements and their positions.

#### regular multiply algorithm

![[matrix Multiply.png]]

> To store  $\large A \cdot B$  in C we have to initialize matrix C first, it takes an additional $\large \Theta (n^2)$ time.
> The above code takes $\large \Theta (n^3)$ time.

#### A simple divide and conquer algorithm

Lets assume that we have A,B and C matrices:
$$ \large A =\begin{pmatrix} A_{11} & A_{12} \\ A_{21} & A_{22} \end{pmatrix}
\quad
B =\begin{pmatrix} B_{11} & B_{12} \\ B_{21} & B_{22} \end{pmatrix}
\quad
C =\begin{pmatrix} C_{11} & C_{12} \\ C_{21} & C_{22} \end{pmatrix}
$$
so that:

![[matrices.png]]

> The equations in the picture above would be correct even if the matrices elements would have been some other $\large n/2\times n/2$ matrices, so we can create a recursive divide and conquer algorithm.

In this algorithm we want to do the $\large C = A\cdot B$.
We have to divide each $\large n\times n$ matrix into four $\large n/2\times n/2$ submatrices.
our base case is when n is equal to 1.

> we have assumed that n is a power of 2.

###### We have two ways for implementing the matrix partitioning:
1. Allocating temporary storage to hold A's, B's and C's submatrices and copying each element in A and B to it's corresponding location in the appropriate submatrix.
   After the recursive conquer step, copy the elements in each of C's four submatrices to their corresponding locations in C. This approach takes $\large \Theta (n^2)$ time, since $\large 3n^2$ elements are copied.
2. using index calculations which is faster and more practical.
   A submatrix can be specified within a matrix by indicating where within the matrix the submatrix lies without touching any matrix elements.
   Changes to the submatrix elements update the original matrix.
   partitioning by index calculations can be performed in $\large \Theta (1)$ time.

>Both of the above ways make no difference to the overall asymptotic running time of matrix multiplication.

![[Pasted image 20240803172255.png]]

the recurrence would be :
$$
\large T(n) = 8T(\frac n 2) + \Theta (1) \quad => \quad T(n) = \Theta(n^3)
$$
my code in Golang: (works for any number not just powers of 2, works with any matrices not just the square ones)

```go
package main

  

import "fmt"

  

func extractSubMatrix(startRow, numOfRows, startCol, numOfCols int, matrix [][]int) [][]int {

var result [][]int

if (startRow == 0 && startRow == numOfRows) || (startCol == 0 && startCol == numOfCols) {

return [][]int{{0}}

}

for i := startRow; i < startRow+numOfRows; i++ {

result = append(result, matrix[i][startCol:startCol+numOfCols])

}

return result

}

  

func matrixMultiply(A, B, C [][]int) {

if len(A) == 1 && len(A[0]) == 1 && len(B) == 1 && len(B[0]) == 1 && len(C) == 1 && len(C[0]) == 1 {

C[0][0] += A[0][0] * B[0][0]

return

}

a11 := extractSubMatrix(0, len(A)/2, 0, len(A[0])/2, A)

a12 := extractSubMatrix(0, len(A)/2, len(A[0])/2, len(A[0])-len(A[0])/2, A)

a21 := extractSubMatrix(len(A)/2, len(A)-len(A)/2, 0, len(A[0])/2, A)

a22 := extractSubMatrix(len(A)/2, len(A)-len(A)/2, len(A[0])/2, len(A[0])-len(A[0])/2, A)

  

b11 := extractSubMatrix(0, len(B)/2, 0, len(B[0])/2, B)

b12 := extractSubMatrix(0, len(B)/2, len(B[0])/2, len(B[0])-len(B[0])/2, B)

b21 := extractSubMatrix(len(B)/2, len(B)-len(B)/2, 0, len(B[0])/2, B)

b22 := extractSubMatrix(len(B)/2, len(B)-len(B)/2, len(B[0])/2, len(B[0])-len(B[0])/2, B)

  

c11 := extractSubMatrix(0, len(C)/2, 0, len(C[0])/2, C)

c12 := extractSubMatrix(0, len(C)/2, len(C[0])/2, len(C[0])-len(C[0])/2, C)

c21 := extractSubMatrix(len(C)/2, len(C)-len(C)/2, 0, len(C[0])/2, C)

c22 := extractSubMatrix(len(C)/2, len(C)-len(C)/2, len(C[0])/2, len(C[0])-len(C[0])/2, C)

  

matrixMultiply(a11, b11, c11)

matrixMultiply(a12, b21, c11)

matrixMultiply(a11, b12, c12)

matrixMultiply(a12, b22, c12)

matrixMultiply(a21, b11, c21)

matrixMultiply(a22, b21, c21)

matrixMultiply(a21, b12, c22)

matrixMultiply(a22, b22, c22)

}

func main() {

a := [][]int{{3, 2}, {2, 9}}

b := [][]int{{4, 5}, {9, 2}}

c := [][]int{{0, 0}, {0, 0}}

matrixMultiply(a, b, c)

fmt.Printf("c: %v\n", c)

}
```

![[Pasted image 20240803220110.png]]

![[Pasted image 20240803220638.png]]

