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
In this implementation we do care about the length of lists, and we append the shorter list to the longer one (in UNION procedure) .

##### Theorem 19.1
Using the linked-list representation of disjoint sets and the weighted-union heuristic, a sequence of $\large m$ `MAKE-SET`, `UNION`, and `FIND-SET` operations, $\large n$ of which are `MAKE-SET` operations, takes $\large O(m + n\space \lg n)$ time.

##### Proof
Because each `UNION` operation unites two disjoint sets, at most $\large n - 1$ `UNION` operations occur over all.

We have to bound the total time taken by `UNION` operations.

We start by determining, for each object, an upper bound on the number of times the object's pointer back to it's set object is updated, So :

**Consider $\large x$ as an object**
Each time $\large x$'s pointer is updated, $\large x$ must have started in the smaller set.
In the $\large i$th $\large x$'s pointer update, the resulting set must have at least $\large 2^i$ members, So we have: $$\large 2^i \leq n \implies i \leq \lg{n} \implies i = \lfloor\lg{n}\rfloor$$
So each object's pointer is updated at most $\large \lfloor\lg{n}\rfloor$ times over all the `UNION` operations.

> Thus the total time spent updating objects pointers over all `UNION` operations is $\large O(n\lg{n})$ .

> Updating the tail pointers and the list lengths, takes $\large \Theta(1)$ time per `UNION` operation.

> Each `MAKE-SET` and `FIND-SET` operation takes $\large O(1)$ time, and there are $\large O(m)$ of them.

So the total time for the entire sequence is thus $\large O(m + n\lg{n})$ .

---

## 19.3 Disjoint-set forests

A **faster** implementation of disjoint sets represent sets by **rooted trees**.
So we have all the sets as some trees in a **disjoint-set forest**.

### Rooted trees
Each tree represents one set and each node represent one member.

- `Root`: The root of each tree contains the representative of each set  
- `node`: each node has a pointer that points to it's parent (**each root is it's own parent**)

![[Data Structures for Disjoint Sets-20240927182703777.webp]]

### Implementation of operations
`MAKE-SET`: Simply creates a tree with just one node.
`FIND-SET`: Follows parent pointers until it reaches the root of the tree.
`UNION`: It' simply causes the root of one tree to point to the root of the other.

> A sequence of $\large n - 1$ `UNION` operations could create a tree that is just a linear chain of $\large n$ nodes. By using two heuristics, however, we can achieve a running time that is almost linear in the total number of $\large m$ operations. **(Which is also better than the linked-list representation)**

##### Heuristics to improve the running time

- `union by rank`:
  For each node of the tree, we maintain a **rank** which is  an **upper bound on the height of the node**.
  Union by rank makes the root with smaller rank point to the root with larger rank during a `UNION` operation .

- `path compression`:
  This heuristic is also quite simple and highly effective.
  `FIND-SET` operations use it to make each node on the find path point directly to the root .
  **(Path compression does not change any ranks)**

![[Data Structures for Disjoint Sets-20240927191637839.webp]]


##### Pseudocode for disjoint-set forests

![[Data Structures for Disjoint Sets-20240927191759864.webp]]

> Each `FIND-SET` operation leaves all ranks unchanged.

> The `FIND-SET` procedure is a **two-pass method**, as it recurses, it makes one pass up the find-path to find the root, and as the recursion unwinds, it makes a second path back down the find-path to update each node to point directly to the root.

### Effect of the heuristic on the running time
Combining union by rank and path compression gives a worst-case running time of $\large O(m\alpha(n))$, where $\large \alpha(n)$ is a very slowly growing function (defined in section 4).

In any conceivable application of a disjoint-set data structure, $\large \alpha(n) \leq 4$, and thus, it's running time is as good as linear in $\large m$ for all practical purposes.

---

## 19.4 Analysis of union by rank with path compression *
