
Our main source for learning NumPy is it's official website: [numpy.org](https://numpy.org/learn/)

# Why using Numpy?
[Why using Numpy](https://numpy.org/doc/stable/user/whatisnumpy.html)

Numpy is a library with the `ndarray` core object. This library helps us to do our job with the same speed as C code and easy coding by python interface.

>It uses optimized **pre-compiled C code** for it's calculations.
>So we are able to code in python easy interface and still benefit the speed of C language.

#### What are Vectorization and Broadcasting?

**Vectorization** describes the absence of any explicit looping, indexing, etc., in the code - these things are taking place, of course, just “behind the scenes” in optimized, pre-compiled C code.

**Broadcasting** is the term used to describe the implicit element-by-element behavior of operations; generally speaking, in NumPy all operations, not just arithmetic operations, but logical, bit-wise, functional, etc., behave in this implicit element-by-element fashion, i.e., they broadcast.

# Numpy quick start

you can see the full tutorial from the official website: [numpy quickstart](https://numpy.org/doc/stable/user/quickstart.html)
## The Basics

We can see some important `ndarray` object attributes right below:
```python
import numpy as np
a = np.arange(15).reshape(3, 5)
print(a)
print(a.shape)
print(a.ndim)
print(a.dtype.name)
print(a.itemsize)
print(a.size)
print(type(a))
b = np.array([6, 7, 8])
print(b)
print(type(b))
```

#### Array Creation
Some example of array creation:
```python
print(np.zeros((3, 4)))
print(np.ones((2,3,4), dtype=np.int16))
```

To create sequences of numbers, NumPy provides the `arange` function which is analogous to the Python built-in `range`, but returns an array.
```python
print(np.arange(2,10,2))
print("---------")
print(np.arange(12).reshape(3,4))
```

>To disable the brief print behaviour and force NumPy to print the entire array, you can change the printing options using `set_printoptions`.

```python
np.set_printoptions(threshold=sys.maxsize)  # sys module should be imported
```

#### Basic operations
Arithmetic operators on arrays apply _elementwise_. A new array is created and filled with the result.
```python
import numpy as np
a = np.array([20, 30, 40, 50])
b = np.arange(4)
c = a-b
print(c)
print(b**2)
print(10 * np.sin(a))
print(np.sin(np.pi/2))
print (a < 35)
```

Unlike in many matrix languages, the product operator `*` operates elementwise in NumPy arrays. The matrix product can be performed using the `@` operator (in python >=3.5) or the `dot` function or method:
```python
import numpy as np
a = np.array([[4, 5],[8, 23]])
b = np.arange(4, 16, 3).reshape(2,2)
print(f"a:\n{a}\nb:\n{b}\n\n")
print(f"a*b = \n{a*b}\n------------\na@b:\n{a@b}")
```

> Some operations, such as `+=` and `*=`, act in place to modify an existing array rather than create a new one.

The `ndarray` class has got some methods, let's see some of them:
```python
# let's see some stuff about random
a = np.random.rand(3,4)
print(a)
print("-------------")
a = np.random.randint(20 ,size=(3,4))
print(a)

# some built-in ndarray methods:
print(a.sum())
print(a.min())
print(a.max())
```

By default, these operations apply to the array as though it were a list of numbers, regardless of its shape. However, by specifying the `axis` parameter you can apply an operation along the specified axis of an array:
```python
b = np.arange(12).reshape(3,4)
print(b)
print("b sum axis=0:")
print(b.sum(axis=0))
print("b.min axis=1:")
print(b.sum(axis=1))
print("b.cumsum axis=1")
print(b.cumsum(axis=1))
```

#### Universal functions
NumPy provides familiar mathematical functions such as sin, cos, and exp. In NumPy, these are called “universal functions” (`ufunc`). Within NumPy, these functions operate elementwise on an array, producing an array as output.

```python
b = np.arange(4)
print(np.exp(b))
print(np.sqrt(b))
```

#### Indexing, slicing and iterating
We can access elements by slicing like what we used to do in regular python lists.
```python
import numpy as np
a = np.arange(5, 50, 2)
print(a)
print(a[2:20:2]) # third index: step
print(a[::-1]) # reverse printing
```

We can have slicing in multidimentions too.
notice the `fromfunction` ufunc. This function is used to make an ndarray in the desired shape with an input function that creates elements according to their coordinate.
```python
b = np.fromfunction(lambda x,y: 2*x + y, (5, 4), dtype=int)
print(b)
print(b[:, 1])

c = np.arange(100).reshape(2,25,2)
print(c[1, ...]) # the same as c[1, :, :] or c[1]
```

**Iterating** over multidimensional arrays is done with respect to the first axis, however, if one wants to perform an operation on each element in the array, one can use the `flat` attribute which is an iterator over all the elements of the array:
```python
b = np.arange(20).reshape(4, 5)
for row in b:
    print(row)
    
# Using flat:
for element in b.flat:
    print(f"{element}, ", end="")
```

## Shape manipulation
#### Changing the shape of an array
As you see the below methods all return a modified array, but do not change the original array itself. **(Although the returned modified array has the same buffer of data, so if any  element change happens through the modified array, it changes the data of the original array too!)**
```python
rg = np.random
a = np.floor(10 * rg.random((3,4)))

print(a.reshape(2, 6))
print(a.ravel())
print(a.T)
print("the original a")
print(a)
print("-------------")
c = a.reshape(2, 6)
c[0, 0] = 100
print(c)
print(a)
```

>To change the shape of the array itself, use `resize` method, (it returns none)

```python
c = a.resize((2, 6))
print(c)
print(a)
```

>If a dimension is given as `-1` in a reshaping operation, it's size gets set automatically according to the other dimensions.

#### Stacking together different arrays
Several arrays can be stacked together along different axes:
```python
rg = np.random
a = rg.randint(0, 20, (2,2))
b = rg.randint(0, 20, (2,2))
print(f"a: \n{a}")
print(f"b: \n{b}")
print("----------")
print(np.vstack((a, b)))
print(np.hstack((a, b)))
```

Also see what happens with 1d arrays:
```python
a = np.array([1, 3, 4])
b = np.array([6, 2, 65])
print(np.hstack((a, b)))
print(np.vstack((a, b)))
```

>In general, for arrays with more than two dimensions,`hstack` stacks along their second axes, `vstack` stacks along their first axes.

The function `column_stack` stacks 1D arrays as columns into a 2D array. It is equivalent to `hstack` only for 2D arrays:
```python
print(np.column_stack((a, b)))

# similar to:
print(np.hstack((a[:, np.newaxis], b[:, np.newaxis])))
```

>There is some other function called `concatenate` which joins a sequence of arrays along an existing axis.

```python
a = np.random.randint(0, 30, (3, 3))
b = np.random.randint(0, 30, (3, 3))
print(f"a:\n{a}")
print(f"b:\n{b}")
print("---------")
print(np.concatenate((a,b), 1))
```

#### Splitting one array into several smaller ones
Using `hsplit`, you can split an array along its horizontal axis, either by specifying the number of equally shaped arrays to return, or by specifying the columns after which the division should occur:
```python
a = np.random.randint(0, 10, (2, 12))
print(f"a:\n{a}")
# Split `a` into 3
print(np.hsplit(a, 3))
# Split `a` after the third and the fourth column
print(np.hsplit(a, (3, 4)))
```

`vsplit` splits along the vertical axis, and `array_split` allows one to specify along which axis to split.
We can choose to split the array to some number of sections or just specify the columns before which the division should occur by **indices_or_sections** parameter.
```python
print(np.array_split(a, 3, axis=1))
print(np.array_split(a, (2, 3), axis=1))
```


## Copies and Views
>By default, we have no copy at all.
>For example in assignments no copy operation happens.

>Python passes mutable objects as references, so function calls make no copy.

#### View or Shallow copy
Different array objects can share the same data. The `view` method creates a new array object that looks at the same data.
```python
import numpy as np
a = np.random.randint(10, size=(9,))
c = a.view()
print(f"This is a:\n\t{a}\n\nThis is a's view(c):\n\t{c}")
c[0] = 4
print(f"This is a:\n\t{a}\n\nThis is a's view(c):\n\t{c}")
```

>Slicing an array returns a view of it.

#### Deep copy
The `copy` method makes a complete copy of the array and its data.
```python
a = np.array([3,5,2,5,21])
d = a.copy()
d[0] = 324
print(a)
print(d)
```

```python
a = np.arange(int(1e8))
b = a[:100].copy()
del a  # the memory of ``a`` can be released.
```

## Functions and methods overview

#### Basic Linear Algebra
> Cross product of two vectors:
```python
import numpy as np
a = np.array([-1, 2, 3])
b = np.array([1, 2, 7])
print(np.cross(a, b))
```

>Dot product of two vectors:
```python
import numpy as np

print(np.dot(3, 4))

print(np.dot(np.array([2, 3, 4]), np.array([9, 5, 8])))

print(np.dot([2j, 3j], [2j, 3j]))

#When both a and b are 2-D arrays, It acts like matrix multiplication
a = [[1, 0], [0, 1]]
b = [[4, 1], [2, 2]]
print(np.dot(a, b))
```

#### Other functinos
>**linespace**: Return evenly spaced numbers over a specified interval.
```python
print(np.linspace(1, 100, 20, dtype=int))
```

>**zeros_like**: Return an array of zeros with the same shape and type as given array.
```python
a = np.array([[23,32, 1], [3,6, 1]])
print(np.zeros_like(a))
```

## Less basic
#### Broadcasting rules
Broadcasting allows universal functions to deal in a meaningful way with inputs that do not have exactly the same shape.

The first rule of broadcasting is that if all input arrays do not have the same number of dimensions, a “1” will be repeatedly prepended to the shapes of the smaller arrays until all the arrays have the same number of dimensions.

The second rule of broadcasting ensures that arrays with a size of 1 along a particular dimension act as if they had the size of the array with the largest shape along that dimension. The value of the array element is assumed to be the same along that dimension for the “broadcast” array.

##### Example:
```python
import numpy as np

A = np.array([
    [1, 2, 3, 4],
    [5, 6, 7, 8],
    [9,10,11,12]
])  # shape (3,4)

B = np.array([10, 20, 30, 40])  # shape (4,)
```

**Step 1: Add dimension**
B → (1, 4)

**Step 2: Stretch**
B → (3, 4)

So NumPy sees it like:
```python
B = [  
 [10, 20, 30, 40],  
 [10, 20, 30, 40],  
 [10, 20, 30, 40]  
]
```

**Result:**
```python
# A + B =
[[11, 22, 33, 44],  
 [15, 26, 37, 48],  
 [19, 30, 41, 52]]

```

>Think of it like this:
- NumPy aligns shapes **from the right**
- It says:
    - “If one side is 1 → I can stretch it”
    - “If they match → good”
    - “Otherwise → error”

## Advanced indexing and index tricks
NumPy offers more indexing facilities than regular Python sequences. In addition to indexing by integers and slices, as we saw before, arrays can be indexed by arrays of integers and arrays of booleans.

#### Indexing with arrays of indices

>**Indexing by arrays of indices**:
```python
import numpy as np

a = np.arange(21)**2
i = np.array([3, 5, 2, 6])
print(a[i])
print()
i = np.array([[3, 5, 4], [1, 2, 9]])
print(a[i])
```

>When the indexed array `a` is multidimensional, a single array of indices refers to the first dimension of `a`.
```python
a = np.arange(12).reshape(4, 3)
print(f"a:\n{a}\n")
i = np.array([1, 3, 0])
print(f"i: {i}")
print(f"a[i]:\n{a[i]}")
```

We can also give indexes for more than one dimension. The arrays of indices for each dimension must have the same shape.
```python
import numpy as np
a = np.arange(12).reshape(4, 3)
i = np.array([[1, 3], [2, 1]])
j = np.array([[1, 2], [0, 1]])
print(a[i, j])
print()
i = np.array([[0,1], [2, 1]])
print(a[:,i])
```

You can also use indexing with arrays as a target to assign to:
```python
import numpy as np
a = np.arange(5)
print(a)
a[[1, 2, 4]] = 0
print(a)
```

#### Indexing with boolean arrays
When we index arrays with arrays of (integer) indices we are providing the list of indices to pick. With boolean indices the approach is different; we explicitly choose which items in the array we want and which ones we don’t.

The most natural way one can think of for boolean indexing is to use boolean arrays that have _the same shape_ as the original array:
```python
a = np.random.randint(24, size=(4, 4))
b = a > 5
print(f"a:\n{a}\n")
print(f"b:\n{b}\n")
print(a[b])
```

This property can be very useful in assignments:
```python
a[b] = 0
print(a)
# All elements of `a` higher than 5 become 0
```

>The second way of indexing with booleans: For each dimension of the array we give a 1D boolean array selecting the slices we want:
```python
a = np.arange(12).reshape(3, 4)
b1 = np.array([False, True, True])
b2 = np.array([True, False, True, False])

print(f"a:\n{a}\n")
print(a[b1, :])
print()
print(a[b1, b2])
```
>note: `a[b1, b2]` works in element behavior, it doesn't filter the rows and columns:
>b1 => (1, 2)
>b2=> (0, 2)
>`a[b1, b2] => [a[1, 0], a[2, 2]]`

#### The ix_() function
`np.ix_` takes multiple **1D index arrays** and turns them into a form that lets you select a **Cartesian product (all combinations)** of indices across multiple axes.

>This function takes N 1-D sequences and returns N outputs with N dimensions each, such that the shape is 1 in all but one dimension and the dimension with the non-unit shape value cycles through all N dimensions.

It can be used to combine different vectors so as to obtain the result for each indices combination of those vectors.
For example, if you want to compute all the $\large a+b*c$ for all the triplets taken from each of the vectors a, b and c:
```python
a = np.array([4, 3, 1])
b = np.array([8, 2])
c = np.array([6, 3, 22])
ax, bx, cx = np.ix_(a, b, c)
print(f"ax:\n{ax}\n")
print(f"bx:\n{bx}\n")
print(f"cx:\n{cx}\n")
result = ax+bx*cx
print("result:")
print(result)
print(result[0, 1, 2]) 
print(a[0]+b[1]*c[2])
```

**`ix_` can also be used in indexing an array**
Consider 2D array a:
```python
a = np.arange(25).reshape(5, 5)
print(a)
```
To index elements in desired rows(1, 2) and columns(0, 4) we can not do the below, because this kind of indexing works **pairwise**:
```python
print(a[(1, 2), (0, 4)])
```

instead we can use `ix_` to get to a **grid (mesh) of index combinations**:
```python
i = np.array([1, 2])
j = np.array([0, 4])
ix, jx = np.ix_(i, j)
print(a[ix, jx])
```
`ix` and `jx` have (2, 1) and (1, 2) shapes in order. When they are used in `a[ix, jx]` they get broadcasted and turn into (2, 2) arrays like the equivalent below code:
```python
i = np.array([[1, 1], [2, 2]])
j = np.array([[0, 4], [0, 4]])
print(a[i, j])
```

## Extra stuff
#### pseudo-inverse of a matrix
Imagine we have a square matrix $X$.
Let's consider some kind of regression model like this:
$$\large\mathbf{X} \mathbf{w} = \mathbf{y}$$
Since $X$ has got no inverse matrix, we can get to $\mathbf{w}$ like this:
$$\large\mathbf{w} = (\mathbf{X}^T \mathbf{X})^{-1} \mathbf{X}^T \mathbf{y}$$
the chunk of math $(\mathbf{X}^T \mathbf{X})^{-1} \mathbf{X}^T$ does exactly what a regular inverse $\mathbf{X}^{-1}$ does for square matrices—it moves $\mathbf{X}$ to the other side of the equation.

So, they gave this specific chunk of math a name: the **Moore-Penrose Pseudoinverse**, written as $\mathbf{X}^+$.
There is a method in `numpy` library called `pinv` that calculate the $\mathbf{X}^+$ for use.
>In calculation of analytical solution of machine learning problems like polynomial regression, it's better to use `pinv` instead of calculating the inverse of the $(\mathbf{X}^T \mathbf{X})$ regluarly, because `pinv` provides us **Numerical stability**.

In linear algebra, the "condition" of a matrix describes how sensitive it is to those tiny rounding errors.
- A **well-conditioned** matrix is stable. A tiny error in the data only causes a tiny error in the result.
- An **ill-conditioned** matrix is unstable. A tiny error in the data causes a massive, chaotic change in the result.
When dealing with $(\mathbf{X}^T \mathbf{X})$ specially with polynomial regression, the matrix becomes ill-conditioned and using `inv` method results in incorrect weights finally.
That's why we should use `pinv` method in these cases, this method use a different algorithm called **Singular Value Decomposition (SVD)** to calculate the inverse while maintaing numerical stability.
