Disjoint sets are sets with no elements in common.

Two operation that we usually need in disjoint sets:
- `Find`: Finding the unique set that contains a given element
- `Union`: Uniting two sets

This chapter explores methods for maintaining a data structure that supports these operations.

---
## 19.1 Disjoint-set operations

A disjoint-set data structure maintains a collection $\large  C = \{S_1, S_2, ..., S_k\}$ 

### representative of each set

> To identify each set, we choose a **representative** which is some member of the set.

> It doesn't matter which member is chosen, it matters only that if you ask for the representative of a dynamic set twice without modifying the set between the requests, **you get the same answer both times**.

> Some applications may require prespecified rule for choosing the representative, such as choosing the smallest member in the set (whose elements can be ordered)

### Disjoint-set operations

> each element of a set is actually an object.

##### Operations
- `MAKE-SET(x)`:
   where $\large x$ does not already belong to some other set, creates a new set whose only member (and thus representative) is $\large x$ .
- `UNION(x,y)`: 
  Unites two disjoint dynamic sets that contain $\large x$ and $\large y$ , say $\large S_x$ and $\large S_y$, into a new set that is the union of these two sets. The representative of the resulting set is any member of $\large S_x \cup S_y$ .
  We should destroy the $\large S_x$ and $\large S_y$ from the collection to keep the sets in the collection disjoint.
- `FIND-SET(x)`: 
  Returns a pointer to the representative of the unique set containing $\large x$.


### analyzing the running times of disjoint-set data structures

 We will analyze the running times of disjoint-set data structures in terms of two parameters:
 - $\large n$ : the number of `MAKE-SET` operations.
 - $\large m$ : the total number of `MAKE-SET`, `UNION`, and `FIND-SET` operations.
 
> The first $\large n$ operations are always `MAKE-SET` operations, so that after the first $\large n$ operations, the collection consists of $\large n$ singleton sets.

> Each `UNION` operation reduces the number of sets by 1, so at most $\large n - 1$ `UNION` operations can occur.


### An application of disjoint-set data structures

One of the many applications of disjoint-set data structures arises in determining the connected components of an undirected graph.

we have two procedures:
1. `CONNECTED-COMPONENTS`: 
   It uses the disjoint-set operations to compute the connected components of a graph.
2. `SAME-COMPONENT`:
   After connected-components procedure has preprocessed the graph, this procedure answers queries about whether two vertices belong to the same connected component.
   
![[Data Structures for Disjoint Sets-20240921230842246.webp]]

![[Data Structures for Disjoint Sets-20240921231529745.webp]]

> In an actual implementation an object representing a vertex would contain a pointer to the corresponding disjoint-set object, and vice versa.

> When the edges of the graph are static(not changing over time) depth-first search can compute the connected components faster (See Exercise 20.3-12 edition 4).
> If the connected components usually get updated, the above implementation would be better than running a new depth-first search for each new edge.

---

## 19.2 Linked-list representation of disjoint sets

In this representation each set is represented by it's own linked list.

**Set object attributes** :
- `head`: pointing to the first object in the list
- `tail` : pointing to the last object

**List member object attributes** :
- A pointer to the next object in the list
- A pointer back to the set object
- A set member

> Within each linked list, the objects may appear in any order.

> The representative of each set is the `set member` in the first object in the list.

### disjoint operations in linked list representation

- `MAKE-SET(x)`: 
  Creates a new linked list whose only object is x . $\large O(1)$ 
- `FIND-SET(x)`: 
  Just follow the pointer from $\large x$ back to it's set object and then return the member in the object that head points to.
- `UNION(g,e)`:
  Appends the linked list containing $\large e$ to the linked list containing $\large g$ .(and the set object for $\large e$'s list is destroyed) We will discuss more precisely in the following ...

![[Data Structures for Disjoint Sets-20240922220321220.webp|719]]

### A simple implementation of union

`Union(x,y)`: appends $\large y$'s list onto the end of $\large x$'s list. 
> The **representative** of $\large x$'s list becomes the **representative** of the resulting set.

> To quickly find where to append $\large y$'s list, use the tail pointer for $\large x$'s list.

> The `UNION` operation destroys the set object for $\large y$'s list.

> `UNON` must also update the pointer to the set object for each object originally on $\large y$'s list, which takes **time linear in the length** of $\large y$'s list .


##### analyzing the running time by aggregate analysis

We construct a sequence of $\large m$ operations on $\large n$ objects.

Objects : $\Large x_1,x_2, ... , x_n$

> We will execute the sequence of $\large n$ `MAKE-SET` operations followed by $\large n - 1$ `UNON` operations . So we have :
> $\large m = 2n - 1$

> Then $\large n$ `MAKE-SET` operations take $\large \Theta(n)$ time. 

> Because the $\large i$th `UNION` operation updates $\large i$ objects, the total number of objects updated by all $\large n -1$ `UNION` operations forms an **arithmetic series**

![[Data Structures for Disjoint Sets-20240922234358640.webp]]

> The above condition is in the worst case, so that appending a longer list onto a shorter list is occurred.

$$\Large \sum_{i = 1}^{n - 1} i = \Theta(n^2)$$


> The total number of operations is $\large 2n - 1$, and so each operation on average requires $\large \Theta(n)$  time. So, the amortized time of an operation is $\large \Theta(n)$ .


### A Weighted-union heuristic

