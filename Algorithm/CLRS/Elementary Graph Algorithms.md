## chapter 20

In this chapter we will learn:
- ##### methods for representation a graph
- ##### searching a graph
> Techniques for searching a graph lie at the heart of the field of graph algorithms.

---
## 20.1  Representation of graphs

We have two methods for representing graphs (directed and undirected ones):
1.  **Adjacency list**
2. **Adjacency matrix**

Two types of graphs:
- **Sparse** : graphs with $\large|E|$  much less than $\large|V|^2$ 
- **Dense** : graphs with $\large|E|$  close to $\large|V|^2$

> Sparse graphs are usually represented by `Adjacency list` method, because it provides a compact way for representing sparse graphs.

> `Adjacency matrix` method is used when we are dealing with a dense graph or when we need to be able to tell quickly whether there is an edge connecting two given vertices.

![[Pasted image 20240807135858.png]]

### Adjacency list representation
consider a graph $G = (V, E)$ :

> If $G$ is a directed graph, the sum of the lenghts of all the adjacency lists is $|E|$

> If $G$ is an undirected graph, the sum of the lengths of all the adjacency lists is $2\space|E|$

> For both directed and undirected graphs, the adjacency list representation requires $\large \Theta ( V + E)$ memory, finding each node in the graph also takes $\large \Theta ( V + E)$ .
> If $|E| = \Omega(V)$ , we can say that finding each edge takes $\large \Theta(E)$ time.

##### Adjacency list disadvantage
> A potential disadvantage of the adjacency-list representation is that it doesn't provide a quick way to determine whether a given edge is present in the graph, we actually have to search for $\large v$ in the adjacency list $\large Adj[u]$ .

##### How to fix it?
- According to Exercise 20.1-8 we can use hash maps instead of adjacency lists, in this way the expected lookup time is $\large O(1)$, but in the worst case it could take $\large O(v)$ .

- We can also sort vertices in each adjacency list at first then we could perform a binary search to find an edge, in this way the worst case lookup time is $\large O(lg V)$ .

- Another way is using `adjacency matrix representation`:
### Adjacency matrix representation

> The adjacency matrix of a graph requires $\large \Theta(V^2)$ memory.

> Since in an undirected graph, $(u,v)$ and $(v,u)$ represent the same edge, the adjacency matrix $A$ of an undirected graph is it's own transpose: $A = A^T$ .

> In some applications, it pays to store only the entries above the diagonal of the adjacency matrix, thereby cutting the memory needed to store the graph almost in half.

examples:
![[Pasted image 20240812233259.png]]

![[Pasted image 20240812233313.png]]

![[Pasted image 20240813160838.png]]

---
## 20.2   Breadth-first search

Breadth-first search is one of the simplest algorithms for searching a graph.
Given a graph $\large G=(V, E)$ and a distinguished source vertex S.
breadth first search explores the edges of G to discover every vertex that is reachable from S. It computes the distance from s to each reachable vertex, where the distance to a vertex v equals the smallest number of edges needed to go from S to V.

> Breadth-first search also produces a breadth-first tree with root S, that contains all reachable vertices.

> For any vertex v reachable from s , the simple path in the breadth-first tree from s to v corresponds to a shortest path from s to v in G, that is a path containing the smallest number of edges.

> **BFS works on both directed or undirected graphs**.

>Breadth-first search is so named because we can think of it as discovering vertices in waves emanating from the source vertex.
>That is, starting from s , the algorithm first discovers all neighbors of s , which have distance 1. Then it discovers all vertices with distance 2, then all vertices with distance 3, and ... , until it has discovered every vertex reachable from S.

> In order to keep track of the waves of vertices, breadth first search uses a single first-in, first-out queue, containing some vertices at a distance k, possibly followed by some vertices at distance $k + 1$ .

### How does it work ?
We define three colors for vertices:
- White : vertices are initially white by default
- gray : A vertex that is reachable from s is discovered the first time it is encountered during the search, at which time it becomes gray
- black : Once all of a vertex’s edges have been explored, the vertex is behind the frontier of the search, and it goes from gray to black.

for each vertex we have:
- v.color
- v.d (distance from the source vertex s to v)
- v.$\large \pi$ is v's predecessor in breadth-first tree 

> Breadth-first search constructs a breadth-first tree, initially containing only it's root, which is source vertex S. Whenever a white vertex v is discovered (in the course of scanning the adjacency list of a gray vertex u) the vertex v and the edge (u, v) are added to the tree. We call u `predecessor` or `parent` of v.


![[Pasted image 20240813232609.png]]

> This while loop maintains the following invariant :
> **The queue Q consists of the set of gray vertices**

![[Pasted image 20240813233703.png]]
![[Pasted image 20240814131348.png]]
### Analyzing running time

>The operations of enqueuing and dequeuing take O(1) time, and so the total time devoted to queue operations is O(V).

>Because the procedure scans the adjacency list of each vertex only when the vertex is dequeued, it scans each adjacency list at most once. Since the sum of the lengths of all $|V|$ adjacency lists is $\large \Theta(E)$, the total time spent in scanning adjacency lists is $\large O(V + E)$. The overhead for initialization is $\large O(V)$, and thus the total running time of the BFS procedure is $\large O(V + E)$.

So we can say:


> Breadth-first search runs in time linear in the size of the adjacency-list representation of $G$ .

![[Pasted image 20240903202215.png]]

### Shortest Paths
- **Shortest-path distance** $\large \delta(s,v)$ : 
	  The minimum number of edges in any path from vertex s to vertex v.
- **Shortest path** :
	  A path of length $\large \delta(s,v)$ from s to v.

##### Lemma 20.1
Let $G = (V,E)$ be a directed or undirected graph, and let $\large s \in V$ be an arbitrary vertex. Then for any edge $\large(u,v)\in E$ : $$\large \delta(s,v) \leq \delta(s,u) + 1$$
##### Proof
We have two cases:
1. $\large u$ is reachable from $\large s$
	  We absolutely have a path from s to v, so we can say the length of this path is greater equal than $\large \delta(s, v)$ . So the inequality holds. 

2. $\large u$ isn't reachable from $\large s$
	  In this case $\large \delta(s, u) = \infty$ and again the inequality holds.



##### Lemma 20.2
Let $\large G = (V, E)$ be a directed or undirected graph, and suppose that BFS is run on $G$ from a given source vertex $\large s \in V$. Then, for each vertex $\large v \in V$, the value $\large v.d$ computed by BFS satisfies $\large v.d \ge \delta(s, v)$ at all times, including at termination.
##### Proof
The proof is by induction on the number of `ENQUEUE` operations. 
The inductive hypothesis is that $\large v.d \geq \delta(s, v)$ for all $\large v \in V$ .
**Induction**: 
- Base case
  The base of the induction is the situation immediately after enqueuing $S$ in line 9 of BFS. The inductive hypothesis holds here because $\large s.d = 0 = \delta(s,s)$ and $\large v.d = \infty \geq \delta(s,v)$ for all $\large v \in V - \{s\}$ .
- inductive step
  For the inductive step, consider a white vertex v that is discovered during the search from a vertex u. The inductive hypothesis implies that $\large u.d \geq \delta(s,u)$ . So according to the line 15 of BFS code and Lemma 20.1 we can say: $$
	  \begin{align} 
	  \large v.d &= \large u.d + 1 \quad
	  \geq \quad \delta(s,u) + 1  \quad
	  \geq \quad \delta(s,v)
	  \end{align}$$
![[Drawing 2024-09-03 20.04.03.excalidraw.svg|650]]

So, we proved that $\large v.d \geq \delta(s,v)$ .
Vertex $\large v$ is only enqueued once and i't won't be again, thus the value of $\large v.d$ never changes again and the inductive hypothesis is maintained.


> All times the d values of vertices in the queue either are all the same or form a sequence $\large <k, k, \dots, k, k+1, k+1, \dots, k+1>$ for some integer $\large k \geq 0$ . (It's our next Lemma 20.3)

##### Lemma 20.3
Suppose that during the execution of BFS on a graph $\large G = (V, E)$, the queue Q contains the vertices $\large <v_1, v_2, \dots, v_r>$, where $\large v_1$ is the head of Q and $\large v_r$ is the tail.
then we have $\quad \large v_r.d \leq v_1.d + 1 \quad and \quad v_i.d \leq v_{i+1}.d \quad for \quad i = 1,2,\ldots, r - 1$ .     
##### Proof
The proof is by induction on the number of queue operations.
- Base case
  Initially when the queue contains only $\large s$ the lemma trivially holds.
  
- Inductive step
  We must prove that the lemma holds after both dequeuing and enqueuing a vertex.
  So We assume that the inductive hypothesis is held, and have to prove, it would be held after an enqueuing or dequeuing.
  
  `Dequeuing`:
  When the head $\large v_1$ of the queue is dequeued we have two cases:
  First if the queue becomes empty, then the lemma holds.
  Second $\large v_2$ becomes the new head, we know by the inductive hypothesis, $\large v_1.d \leq v_2.d$ . 
  we know that $\quad \large v_r.d \leq v_1.d + 1 \quad$  
  then we can say : $\quad \large v_r.d \leq v_2.d + 1 \quad$  since $\quad \large v_1.d \leq v_2.d$ .
  The remaining inequalities are unaffected.
  
  `Enqueuing`:
  When a vertex $\large v$ is enqueued onto a queue $\large <v_1, v_2, \dots , v_r>$ the enqueued vertex becomes $\large v_{r+1}$ . again we have two cases:
  First if the queue was empty before enqueuing $\large v$ , then after that the lemma trivially holds.
  Second the queue was not empty. In this case the procedure has most recently removed vertex $\large u$ , whose adjacency list is currently being scanned, from the queue $\large Q$ .
  Before removing $\large u$ we know that :
  $\large u = v_1 \quad u.d \leq v_2.d \quad v_r.d \leq u.d + 1$
  After u is removed the vertex $\large v_2$ becomes the new head $\large v_1$ of the queue,
  
  So for proving $\large v_{r+1}.d = v.d \leq v_1.d + 1$  we have :	  
  $\large u.d \leq v_1.d \quad$ (add $+1$ to each side) 
  so we can say:
  $\large u.d + 1 \leq v_1.d + 1 \quad \implies \quad v_{r+1}.d = v.d \leq v_1.d + 1$ 

  For proving $\large v_r.d \leq v_{r+1}.d$ we can say:
  $\large v_r.d \leq u.d + 1 \quad and \quad u.d + 1 = v.d \quad so \quad v_r.d \leq v.d = v_{r+1}.d$ 
  
  The remaining inequalities are unaffected.

##### Corollary 20.4
Suppose that vertices $\large v_i$ and $\large v_j$ are enqueued during the execution of BFS, and that $\large v_i$ is enqueued before $\large v_j$ . Then $\large v_i.d \leq v_j.d$ at the time that $\large v_j$ is enqueued.

##### Proof
From Lemma 20.3 .

### Theorem 20.5 (correctness of breadth-first search)
Let $\large G = (V, E)$ be a directed or undirected graph, and suppose that BFS is run on G from a given source vertex $\large s \in V$ . Then during it's execution, BFS discovers every vertex $\large v \in V$ that is reachable from the source $\large s$, and upon termination, $\large v.d = \delta(s,v)$ for all $\large v \in V$. 

>Moreover, for any vertex $\large v \neq s$ that is reachable from $\large s$, one of the shortest paths from $\large s$ to $\large v$ is a shortest path from $\large s$ to $\large v.\pi$ followed by the edge $\large (v.\pi, v)$ .

##### Proof (By contradiction)
We want to prove : $$
\large \forall v\in V : v.d = \delta(s,v)$$
So the contradiction hypothesis would be:$$
\large \exists v \in V : v.d \neq \delta(s,v)$$

Assume for the purpose of contradiction we have some vertex like $\large v$ so that $\large v.d \neq \delta(s,v)$ .
about vertex $\large v$ we have:
- According to Lemma 20.2 $$\large v.d \geq \delta(s,v) \implies v.d > \delta(s,v)$$
  So $\large v$ **must be reachable** from $\large s$, for otherwise we would have : $$\large \delta(s,v) = \infty \geq v.d$$
- We cannot have $\large v = s$, because $\large s.d = 0 \quad and \quad \delta(s,s) = 0$

Let $\large u$ be the vertex immediately preceding $\large v$  (since $\quad \large v \neq s \quad u$ must exist) on some shortest path from $\large s$ to $\large v$, so that :       $$\large \delta(s,v) = \delta(s,u) + 1 \qquad u.d=\delta(s,u)$$       
putting these properties together gives: $$\large v.d > \delta(s,v) = \delta(s,u) + 1 = u.d + 1$$
Now consider the time when BFS dequeues vertex $\large u$ from $\large Q$, at this time we have three cases for $\large v$ that all of them lead to a contradiction of  the above inequality.

![[Drawing 2024-09-04 00.24.39.excalidraw.svg]]

Thus we conclude that : $$
\large \forall v \in V : v.d = \delta(s,v)$$
Now we can say : $$
\large v.\pi = u \implies v.d = u.d + 1   $$
and, shortest path from $\large s$ to $\large v$, is shortest path from $\large s$ to $\large v.\pi$ + edge $\large (v.\pi, v)$ 

### Breadth-first trees

The blue edges show the breadth-first tree built by the BFS procedure as it searches the graph.

> The tree corresponds to the $\large \pi$ attributes.

![[Pasted image 20240813233703.png]]

We define the **predecessor sub-graph** of $\large G$ as $\large G_\pi = (V_\pi,E_\pi)$, where $$\large V_\pi = \{v \in V : v.\pi \neq NIL\} \space \cup \space \{s\}$$ and $$\large E_\pi = \{(v.\pi,v): v \in V_\pi - \{s\}\}$$
$\large G_\pi$ is a breadth-first tree so that 
$\large V_\pi$ : Consists of the vertices reachable from $\large s$
$\large E_\pi$ : Consists of the tree edges

> For all $\large v \in V_\pi$, contains a unique simple path from $\large s$ to $\large v$ that is also shortest path.

> In a breadth-first tree we have : $\large |E_\pi| = |V_\pi| - 1$ 

##### Lemma 20.6
When applied to a directed or undirected graph $\large G = (V,E)$, procedure BFS constructs $\large \pi$ so that the predecessor subgraph $\large G_\pi = (V_\pi, E_\pi)$ is a breadth-first tree.

##### Proof
Line 16 of BFS sets $\large v.\pi = u$ if and only if $\large (u,v) \in E$ and $\large \delta(s,v) < \infty$ and thus $\large V_\pi$ consists of the vertices in $\large V$ reachable from $\large s$ .
Since the predecessor subgraph forms a tree, be Theorem B.2, it contains a unique simple path from $\large s$ to each vertex in $\large V_\pi$ .
Applying Theorem 20.5 inductively yields that every such path is a shortest path in $\large G$ .


![[Pasted image 20240911211110.png]]

> This procedure runs in time linear in the number of vertices in the path printed.

---
## 20.3   Depth-first search

Depth-first search is another algorithm for searching a graph.
Depth-first search searches "deeper" in the graph whenever possible.

### How does it work?
Let's consider vertex $\large v$ as the most recently discovered vertex.
DFS would deeply explore all the edges of vertex $\large v$ (It also explores all the edges of the connected vertices to vertex $\large v$ until there would be no edge left at the end, and then starts to backtrack) .
Once all of $\large v$ 's edges have been explored, the search **backtracks** to explore edges leaving the vertex from which $\large v$ was discovered.
This process continues until all vertices that are reachable from the original source have been discovered.

> If any undiscovered vertices remain, then depth-first search selects one of them as a new source, and repeats the search process from that new source.

> The algorithm repeats this entire process until it has discovered every vertex.

> Unlike breadth-first search, whose predecessor subgraph forms a tree, DFS search produces a predecessor subgraph that might contain several trees, because the search may repeat from multiple sources.

##### Predecessor subgraph of a DFS search
- It always includes all vertices
- It accounts for multiple sources
- It forms a **depth-first forest** comprising several **depth-first trees**
- The predecessor subgraph is $\large G_\pi = (V, E_\pi)$ where : $$\large E_\pi = \{(v.\pi,v) : v\in V \quad and \quad v.\pi \neq NIL \space \}$$
- The edges in $\large E_\pi$ are tree edges.

> Like BFS search, DFS search colors vertices during the search to indicate their state.

`White` : Default initial color
`gray`: When a vertex is discovered it becomes gray
`black`: When a vertex's adjacency list has been examined completely

> This coloring technique guarantees that each vertex ends up in exactly on depth-first tree, so that these trees are disjoint.

##### vertex timestamps
Depth-first search also **timestamps** each vertex. 
Each vertex like $\large v$ has two timestamps:
1. `first timestamp` $\large v.d$ : recorded when $\large v$ is first discovered and grayed.
2. `second timestamp` $\large v.f$ : recorded when the search finishes examining $\large v$ 's adjacency list and blackens $\large v$ .

> The value of timestamps are integers in range: $$\large 1 \leq timestamp \leq 2|V|$$
> and we always have: $$\large u.d < u.f$$

> **DFS works on both directed or undirected graphs**.

### Depth-first search code

![[Pasted image 20240915022950.png]]

> Lines 5-7 of DFS check each vertex in $\large V$, when a white vertex such as $\large v$ is found, visit it by calling DFS-VISIT.

> Upon every call of DFS-Visit$(G, u)$ in line 7, vertex $\large v$ becomes the root of a new tree in the depth-first forest.

> When DFS returns, every vertex $\large u$ has been assigned a **discovery time** $\large u.d$ and a **finish time** $\large u.f$ .

> In each call DFS-VISIT$(G, u)$:
> - `Lines 1-3`: increment time value, record discovery time of $\large u$ , paint $\large u$ gray
> - `Lines 4-7`: examine each vertex $\large v$ adjacent to $\large u$ and recursively visit $\large v$ if it is white
> - `Lines 8-10`: finally after every edge leaving $\large u$ has been explored, increment time, record finish time $\large u.f$ , and paint u black.

> The results of DFS may depend upon the order of examined vertices in line 5 of DFS and line 4 of DFS-VISIT.
> These different visitation orders won't cause problems in practice.


### Depth-first search running time

>The loops on line 1-3 and lines 5-7 of DFS take $\large \Theta (V)$ time, exclusive of the time to execute the calls to DFS - VISIT .

> To calculate the running time of DFS - VISIT, it is better to see how many times it is called, and then we can calculate the whole running time of all calls to DFS - VISIT .

> The procedure DFS - VISIT is called exactly once for each vertex $\large v \in V$ .

![[Drawing 2024-09-19 20.02.18.excalidraw.svg]]

![[Pasted image 20240920014246.png]]
