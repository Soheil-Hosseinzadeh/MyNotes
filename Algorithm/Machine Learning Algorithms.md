 >**CLRS-Chapter 33 edition 4**

## Machine Learning overview
**Different forms of machine learning:**
- Supervised learning
- unsupervised learning
- reinforcement learning

![[Machine Learning Algorithms-20260502014627848.webp]]


## 33.1 Clustering
 
Let S denote the given set of $n$ points in $\large R^d$
>**Goal:** Creating $k$ clusters $\large <S^{(1)}, S^{(2)}, \dots, S^{(k)}>$ of $\large S$ with $k$ centers $\large <c^{(1)}, c^{(2)}, \dots, c^{(k)}>$ so that minimize the sum of squared distance from each point to its nearest center.
>
![[Machine Learning Algorithms-20260502021909877.webp|268]]
![[Machine Learning Algorithms-20260502021250803.webp|517]]

Unfortunately this problem is **NP-hard**. So we can not find a global minimum but we can find a **local minimum**!

A local minimum of *f(S, C)* has two properties:
1. Optimal Center for each cluster (centroids as centers)
2. Assigning each point to the cluster with nearest center

#### Optimal center for each cluster
![[Machine Learning Algorithms-20260502032027794.webp]]

#### Cluster with nearest center for each point
![[Machine Learning Algorithms-20260502032600152.webp]]
![[Machine Learning Algorithms-20260502164955808.webp]]

#### Lloyd's procedure
![[Machine Learning Algorithms-20260502165030273.webp]]

>Note: each iteration of Lloyd's procedure (except the last iteration), strictly decrease *f(S,C)*.
>(iteration: 4. Recompute centers as centroids => 2. Assign points to clusters)

>We know for sure that the Lloyd's procedure will terminate. It has to iterate at most $\large k^n$ times.
##### Running time
- Theoretically $\large O(k^n)$
- Practically consider a threshold for the decrease percentage in *f(S, C)*
  **$\large T$** : number of iterations => $\large O(T\ d\ k\ n)$

#### Examples
##### Clustering 1D points into 2 clusters
![[Machine Learning Algorithms-20260502165247678.webp]]

parameters: $\Large c_{1}, c_{2}$

**$\Large F(S, C):$**
![[Machine Learning Algorithms-20260502164416812.webp]]
![[Machine Learning Algorithms-20260502164721433.webp]]

**Lloyd's Procedure on this example:**
**Iterations of Lloyd's procedure in $\large F(S, C)$ function:**
- starting $\large C: \ c_{1} = 47 \ \ c_{2}=40$
![[Machine Learning Algorithms-20260502193833904.webp]]
![[Machine Learning Algorithms-20260502210851387.webp]]


**Iterations of Lloyd's procedure:**

![[Machine Learning Algorithms-20260502215206852.webp]]

![[Machine Learning Algorithms-20260502215155563.webp]]

![[Machine Learning Algorithms-20260502215217226.webp]]

![[Machine Learning Algorithms-20260502215223375.webp]]

![[Machine Learning Algorithms-20260502215229275.webp]]

##### Clustering the capitals of cities
![[Machine Learning Algorithms-20260502230109087.webp]]

##### Compressing a photograph
The goal here is to reduce the number of distinct colors required to represent a photograph.
Each photograph has some pixels and each pixel is an **RGB** vector represented by 24 bits.
$$\Large \text{pixel} =
\begin{pmatrix}
R (8\ bit) \\
G (8\ bit) \\
B (8\ bit)
\end{pmatrix}
$$
We choose k as the number of distinct colors (cluster centers).
K is usually a power of 2, for example if $\large k=16$ we can encode each pixel with $\large \lg(k) = 4$ bits.

There is an auxiliary table called **palette** which is used for decompression and maps each pixel value to its 24-bit cluster center.

![[Machine Learning Algorithms-20260502231843623.webp]]
![[Machine Learning Algorithms-20260502231906633.webp]]

---
## 33.2 Multiplicative-weights algorithms

You have to make a sequence of decisions, but some of the information needed to make the $i$th decision appears only after you have already made the $(i-1)$st decision.

>So in this section we are going to observe **online** machine learning algorithm.

#### Problem
We have:
- n pre-trained models (also called Experts): $\large E_{1}, E_{2}, \dots, E_{n}$
- We have $\large T$ events, each with an outcome of either 0 or 1
- $\large o^{(t)}$ denotes the outcome of the $t$th event.
- Before event t, each expert $\large E^{(i)}$ makes a prediction $\large q^{(t)}_{i} \in \{0, 1\}$

We have to produce a prediction $\large p^{(t)}$ By using $n$ experts for each event.
Our prediction base is only on the predictions of the experts and anything we have learned about the experts from their previous predictions.

total number of mistakes: $\large m$
$$\large
m = \sum^{T}_{t=1} |p^{(t)} - o^{(t)}|
$$
$\large m^*$ denotes the number of mistakes made by the best expert:
$$\large m^*=min\{m_{i}: 1 \leq i\leq n\}$$
we define *regret* as $\large m-m^*$

>The goal is to minimize the total number m of mistakes, so that to limit the number of our mistakes to be close to the number of mistakes of the best expert.
>In other words we tend to design an algorithm with low regret. (Regret can be negative, although it typically isn’t, since it is rare that you do better than the best expert.)


#### Majority Vote
What happens if we consider the majority vote of experts predictions and delete experts with wrong predictions at each event?

![[Machine Learning Algorithms-20260503001155190.webp]]

**Generalized algorithm without any perfect expert**
We do the same approach like the above *Lemma* although we may get to empy $\large S$, if that happens we will reset $\large S$ and fill it with all the experts and continue.
>In this way the algorithm is going to make at most $\large m^*\lceil \lg{n} \rceil$ mistakes.

There is a better approach: **learn about experts by their previous predictions**
#### Weighted-Majority
- In this approach we assign weights to experts which show how much we trust each expert.
- At each event decrease the weight of experts with wrong prediction via multiplying their weights.

**Definitions:**
- ($0 < \large w^{(i)}_{i}\leq 1$) denotes the weight of $\large i$th expert for $\large t$th event. 
- ($\large 0<\gamma \le \frac{1}{2}$) the parameter that get multiplied with weights and controls the weight decrease.
- $\large upweight^{(t)}$ : The sum of the weights of the experts who predict 1 for event $t$.
- $\large downweight^{(t)}$ : The sum of the weights of the experts who predict 0 for event $t$.

![[Machine Learning Algorithms-20260503011204078.webp]]

#### Analyzing total mistakes with respect to the best expert

- $\large m^{(t)}$ : number of mistakes made by the procedure through event $t$ .
- $\large m^{(t)}_{i}$ number of mistakes made by expert $\large E_{i}$ through event $t$ .
![[Machine Learning Algorithms-20260503013240091.webp]]
![[Machine Learning Algorithms-20260503014557955.webp]]
![[Machine Learning Algorithms-20260503014718649.webp]]
![[Machine Learning Algorithms-20260503015400311.webp]]

**Reminding Taylor series around $\large a$** :
$$\large f(x) = \sum_{n=0}^{\infty} \frac{f^{(n)}(a)}{n!}(x-a)^n $$
**finding lower bound: $\large \ln(1-x) \geq -x -x^2 \quad\text{for} \quad0<x\leq \frac{1}{2}$**
$$\large
\begin{align}
\ln(1-x) &= -x -\frac{x^2}{2}-\frac{x^3}{3}- \dots \\
&= -x-\frac{x^2}{2}\left( 1+\frac{2x}{3}+\frac{2x^2}{4}+\frac{2x^3}{5}+\dots \right) \\
&\geq -x-\frac{x^2}{2}(1+x+x^2+x^3+\dots) \\
&=-x-\frac{x^2}{2}\left( \frac{1}{1-x} \right),\quad   \text{for}\ |x|<1:\frac{1}{1-x} \leq2\\
&\geq-x-\frac{x^2}{2} \cdot2 \\
&=-x-x^2
\end{align}
$$
![[Machine Learning Algorithms-20260503025342075.webp]]
![[Machine Learning Algorithms-20260503025730736.webp]]
![[Machine Learning Algorithms-20260503035352035.webp]]

---
## 33.3 Gradient descent

Gradient descent is general method for finding a local minimum of a function for which $\large f(x)\leq f(x')$ for all $\large x'$ that are near x.

>When the function is convex, it can find a point near the **global minimizer**.

#### Gradient
Given a function $\large f: R^n\to R$ its gradient $\large \nabla f$ is a function $\large \nabla f: R^n\to R^n$ comprising $\large n$ partial derivatives: $\large (\nabla f)(x)=\left( \frac{\partial f}{\partial x_{1}} , \frac{\partial f}{\partial x_{2}} , \dots, \frac{\partial f}{\partial x_{n}}\right)$.

>The gradient can be viewed as direction in which the function value locally increases the fastest.


#### Unconstrained gradient descent
>**Gradient descent idea:** Move in the direction opposite to the gradient, by a distance influenced by the magnitude of the gradient.

![[Machine Learning Algorithms-20260508183145155.webp]]

> According to the above picture we can see that **initial point** and **step size** are important in gradient descent.

![[Machine Learning Algorithms-20260509031530786.webp]]

![[Machine Learning Algorithms-20260509063943684.webp]]

Gradient does not always work! We are going to see when it works and quantify the number of iterations needed.

#### Analysis of unconstrained gradient descent

>Our analysis focuses on convex functions.

##### What is a convex function?
$$
\large
\begin{align}
&f:R^n\to R \quad \text{for all }x, y \in R^n \quad\text{and for all }0\leq \lambda\leq 1, \ \text{we have:} \\ \\
&\qquad f(\lambda x+(1-\lambda)y) \leq \lambda f(x) + (1-\lambda)f(y)
\end{align}
$$
![[Machine Learning Algorithms-20260509041036701.webp]]

>In unconstrained gradient descent we also assume that our convex function is **<mark style="background: #ADCCFFA6;">closed</mark>** and **<mark style="background: #ADCCFFA6;">differentiable</mark>**.

##### What is a closed function?

At first we need to know what is a closed set: 
>$\large (x_{n})$ is considered a sequence dependent to $n$.
$$
\Large C \text{ is closed} \equiv (\ \forall(x_{n})\subseteq C,\ x_{n}\to x \implies x\in C\ )
$$

>A set $\large C$ is closed if whenever every convergent sequence in $\large C$ converges to a point in $\large C$.

examples of closed sets:
$$\large
\begin{align}
& [0, 1] \\
&(-\infty, 5] \\
& \mathbb{R} \\
\end{align}
$$

Now we consider $\large f:\mathbb{R}^n \to \mathbb{R}$ as a closed function so that:
$$\large
\begin{align}
\forall \alpha \in \mathbb{R} \quad \text{the set } \{x \in dom(f): f(x) \leq \alpha\}\ \text{is closed}
\end{align}
$$
Actually the function is closed if all regions have no missing boundary points.

For example the below function is not a closed one and has missing boundary points:
![[Machine Learning Algorithms-20260509063649805.webp]]


We can prove that in a convex function, any local minimum is also a global minimum:
![[Machine Learning Algorithms-20260509064112908.webp]]
by letting $\lambda = 1$ we get to contradiction.

##### Properties of Convex functions
**1- A convex function always lies above its tangent hyperplane**
$$\large
\begin{align}
&\text{for any convex differentiable function }f: \mathbb{R}^n \to \mathbb{R}\ ,\quad \forall x,y\in \mathbb{R}^n \quad \text{we have:} \\ \\

&\qquad \qquad \qquad \qquad f(x) \geq f(y) + \langle\nabla f(x),\ y-x\rangle
\end{align}
$$

![[Machine Learning Algorithms-20260509223118185.webp]]

![[Machine Learning Algorithms-20260509230230087.webp]]

**2- The function value at the average point is at most the average of the function values**:
$$\large
\begin{align}
&f:\mathbb{R}^n\to\mathbb{R},\ \text{for any integer } T\ge 1,\ \text{and for all }x^{(0)}, \dots,x^{(T-1)}\in\mathbb{R}^n, \text{we have:} \\ \\
&\qquad \qquad \qquad \qquad f\left( \frac{x^{(0)}+\dots+x^{(T-1)}}{T}\right) \leq \frac{f(x^{(0)})+\dots+f(x^{(T-1)})}{T}
\end{align}
$$

##### Analysis of gradient descent
Consider the `gradient descent` procedure that we saw earlier.

- Gradient descent doesn't return the exact global minimizer $\large x^{*}$.
- We consider $\large \epsilon$ as an error bound so that $\large f(\text{x-avg})-f(x^{*})\leq \epsilon$ at termination.

The value of $\large \epsilon$ depends on three things:
1. number $\large T$ of iterations
2. $\large R=||x^{(0)}-x^{*}||$ : It will be better to start close to the global minimizer
3. $\large ||\nabla f(x)|| \leq L$ : An upper bound on the magnitude of the gradient

In the following of this section we are going to analyze the error bound.
![[Machine Learning Algorithms-20260510023450505.webp]]
![[Machine Learning Algorithms-20260510023515235.webp]]
![[Machine Learning Algorithms-20260510030548908.webp]]
![[Machine Learning Algorithms-20260510031053308.webp]]
![[Machine Learning Algorithms-20260510031203250.webp]]
**proof**:
$$\large
\begin{align}
||a+b||^2-||a||^2&=(a_{1}+b_{1})^2+(a_{2}+b_{2})^2+\dots+(a_{n}+b_{n})^2-(a_{1}^2+a_{2}^2+\dots+a_{n}^2) \\
&= b_{1}^2+b_{2}^2+\dots+b_{n}^2+2(a_{1}b_{1}+a_{2}b_{2}+\dots+a_{n}b_{n}) \\
&=||b||^2 + 2<a,\ b>
\end{align}
$$
![[Machine Learning Algorithms-20260510031816570.webp]]
![[Machine Learning Algorithms-20260510032009187.webp]]
We can do this about the left dot product:
according to the tangent hyperplane property of the convex functions we know that:
$$\large
\begin{align} \\
&\forall x, y \in \mathbb{R^n} \quad \text{and} \quad f:\mathbb{R}^n\to\mathbb{R} \\ \\
&f(x)\geq f(y) + \langle\nabla f(y),\ x-y\rangle \implies -(f(y)-f(x))\geq- \langle\nabla f(y),\ y-x \rangle
\end{align}
$$

So now we continue the equation like below:
![[Machine Learning Algorithms-20260510033448668.webp]]

![[Machine Learning Algorithms-20260510035244031.webp]]
![[Machine Learning Algorithms-20260510035301969.webp]]


>So now according to the error bound $\large \epsilon =RL/\sqrt{ T }$ we are able to <mark style="background: #ADCCFFA6;">get close to the global minimum as much as we desire</mark> by <mark style="background: #FF5582A6;">increasing</mark> the number of iterations $\large T$.
>
>Actually we can interpret the analysis of gradient descent as a proof that there is some step size $\large \gamma=R/(L\sqrt{ T })$ for which the procedure makes progress toward the minimum.

**Practical problem**
Practically we usually don't really know $\large R$ and $\large L$ . What should we do then?
In each iteration we can search for a step size via a **binary-search-routine** that achieves a large decrease in $\large f(x^{(t+1)})-f(x^{(t)})$. This method is called <mark style="background: #ADCCFFA6;">line search</mark>.

**line search**:
$$\large
\begin{align}
&g(x^{(t)},s)=f\left(x^{(t)}-s\nabla f(x^{(t)})\right) \\
\end{align}
$$
At first we start with a small step size $\large s$ for which $\large g(x^{(t)}, s)\leq f(x^{(t)})$, then repeatedly double $\large s$ and compute $\large g$ function, until we get to step sizes $\large s,\ 2s$ by which $\large g(x^{(t)}, 2s) \geq g(x^{(t)}, s)$.
Then we perform a binary search in the interval $\large [s, 2s]$ to find the step size that achieves sufficient decrease. (the more decrease the better)


#### Constrained gradient descent
In this kind of gradient descent we have some limitations.

At first let's see some required definitions:
**body:**
We call $\large K \subseteq \mathbb{R}^n$ a body. For example a simple 2d area in x-y plane.

**Convex Body:**
A body is denoted as a convex body when  for all $\large x, y \in K$ we have:
$$\large
\lambda x + (1-\lambda)y \in K \quad \text{for all }\  0\leq\lambda\leq1
$$
![[Machine Learning Algorithms-20260514022449840.webp]]

>A **closed convex body** contains its limit points.

**Projection**:
We define projection $\large\prod_{K}(x)$ of a point $\large x$ in $\large n$ dimensions onto a convex body $\large K$ as the point $\large y\in K$ such that:
$$\large
||x-y|| = min\{||x-z||: z\in K\}
$$
If we have $\large x \in K$ then $\large\prod_{K}(x) = x$ .

Now we can say what **<mark style="background: #ADCCFFA6;">Constrained gradient descent</mark>** is:
We want to minimize a closed convex function $\large f(x)$, subject to the additional requirement that $\large x \in K$, where $\large K$ is a closed convex body.

We run the same gradient descent algorithm but:
- In each iteration we check whether the current $\large x^{(t)}$ is still within the convex $\large K$ or not.
- If it is not, we move it to the closest point in $\large K$ which is its projection on $\large K$.
>We assume that $\large \ x^{(0)} \in K$ .

![[Machine Learning Algorithms-20260514024346436.webp]]

![[Machine Learning Algorithms-20260514025522246.webp]]

![[Machine Learning Algorithms-20260514025052167.webp]]![[Machine Learning Algorithms-20260514025811274.webp]]![[Machine Learning Algorithms-20260514025825338.webp]]
![[Machine Learning Algorithms-20260514025840585.webp]]

##### Analysis of constrained gradient descent
![[Machine Learning Algorithms-20260514032138828.webp]]

In this part we tend to calculate the error bound $\large f(\text{x-avg})-f(x^*)\leq \epsilon$ .
Fortunately We can do the same steps as we did in unconstrained gradient descent.
Only there is one different step in calculating an upper bound for the $\large \Phi(t-1)-\Phi(t)$:
![[Machine Learning Algorithms-20260514033005422.webp]]
With this same upper bound on the change in the potential function as in unconstrained gradient descent, the entire proof can proceed as before.

##### Applications of gradient descent
Gradient descent is widely used in **optimization** and **machine learning**.

###### **<mark style="background: #ADCCFFA6;">Solving linear equations</mark>**

**Prerequisites:**
- <mark style="background: #BBFABBA6;">Gradient of $\large X^TAX$</mark>
Consider $\large A$ as an $\large n \times n$ matrix and $\large X$ as an $\large n \times 1$ vector.
Then we have: $\large \nabla (\mathbf{x}^TA\mathbf{x}) = 2A\mathbf{x}$ if and only if $\large A$ is a symmetric matrix.

- <mark style="background: #BBFABBA6;">Positive-semidefinite matrix</mark>
An $\large n \times n$ matrix $\large A$ is **positive-semidefinite** if $\large \mathbf{x}^TA\mathbf{x}\geq0$ for all n-dimensional vectors $\large \mathbf{x}$.

- <mark style="background: #BBFABBA6;">Multidimensional convex function</mark>
A 1-dimensional function is convex when its second derivative is positive.
The equivalent definition for a multidimensional function is that it is convex when its **Hessian matrix** $\large \nabla^2f(x)$ is positive-semidefinite.

**Hessian matrix**:
![[Machine Learning Algorithms-20260514055841052.webp]]

**Proof**:
Assume a function $\large f(x)$ and $\large x, v \in \mathbb{R}^n$ and $\large t \in \mathbb{R}$.
Now let's consider $\large f(x+tv)$, we can interpret $\large f(x+tv)$ as moving toward direction $\large v$ from point $\large x$ so that we can change the sign and the magnitude of our move by $\large t$.

According to this interpretation we can say:
$$\large
f(x) \text{ is a convex function} \iff \forall x,v\in \mathbb{R}^n, \forall t\in\mathbb{R}: \  \frac{d^2}{dt}f(x+tv)\geq0
$$
$$\large
\begin{align} \\
&f(x)=f(x_{1}, x_{2},\dots,x_{n}) \\
&\frac{df}{dt}= \frac{\partial f}{\partial x_{1}}\ \frac{dx_{1}}{dt}+\frac{\partial f}{\partial x_{2}}\ \frac{dx_{2}}{dt} + \dots+\frac{\partial f}{\partial x_{n}}\ \frac{dx_{n}}{dt} = \nabla f(x)^T\left(\begin{matrix}
\frac{dx_{1}}{dt} \\
\frac{dx_{2}}{dt} \\
\dots \\
\frac{dx_{n}}{dt}
\end{matrix}\right) \\
&\frac{d}{dt}f(x+tv)= \nabla f(x+tv)^T \left(\begin{matrix}
v_{1} \\
v_{2} \\
\dots \\
v_{n}
\end{matrix}\right)= \nabla f(x+tv)^Tv
\end{align}
$$
Now we take the second derivation:
$$\large
\begin{align}
&\frac{d^2}{dt}f(x+tv)=\frac{d}{dt}(\nabla f(x+tv)^T)v \\
&=\left(\frac{d}{dt}\frac{\partial f}{\partial x_{1}}(x+tv),\frac{d}{dt}\frac{\partial f}{\partial x_{2}}(x+tv),\dots, \frac{d}{dt}\frac{\partial f}{\partial x_{n}}(x+tv)\right).v \\ \\
&=\left(\nabla\left(\frac{\partial f}{\partial x_{1}}(x+tv)\right)^T.v,\ \nabla\left(\frac{\partial f}{\partial x_{2}}(x+tv)\right)^T.v, \dots,\ \nabla\left(\frac{\partial f}{\partial x_{n}}(x+tv)\right)^T.v\right).v \\
&=\left(v^T.\nabla\left(\frac{\partial f}{\partial x_{1}}(x+tv)\right), \ v^T.\nabla\left(\frac{\partial f}{\partial x_{2}}(x+tv)\right), \dots,\ v^T.\nabla\left(\frac{\partial f}{\partial x_{n}}(x+tv)\right)\right).v \\ \\
&=v^T.
\left(\begin{matrix}
\frac{\partial^2f}{\partial x_{1}\partial x_{1}}(x+tv),& \frac{\partial^2f}{\partial x_{1}\partial x_{2}}(x+tv),&\dots&,\frac{\partial^2f}{\partial x_{1}\partial x_{n}}(x+tv) \\
\frac{\partial^2f}{\partial x_{2}\partial x_{1}}(x+tv),& \frac{\partial^2f}{\partial x_{2}\partial x_{2}}(x+tv),&\dots&,\frac{\partial^2f}{\partial x_{2}\partial x_{n}}(x+tv) \\
\dots&\dots&\dots&\dots\\
\dots&\dots&\dots&\dots \\
\frac{\partial^2f}{\partial x_{n}\partial x_{1}}(x+tv),& \frac{\partial^2f}{\partial x_{n}\partial x_{2}}(x+tv),&\dots&,\frac{\partial^2f}{\partial x_{n}\partial x_{n}}(x+tv)
\end{matrix}\right).v \\ \\
&=v^TH(x+tv)v \\
\end{align}
$$
So in order for $\large f(x)$ to be a convex function we should have:
$$\large
\forall x, v \in \mathbb{R}^n, \forall t\in \mathbb{R}:\ \  v^TH(x+tv)v\geq0
$$
Since we are free in choosing $\large x, v, t$ we can make the formula more simple:
$$\large
\forall x, y \in \mathbb{R}^n:\ \  y^TH(x)y\geq0
$$
which means $\large \forall x\in \mathbb{R}^n$ the Hessian matrix $\large H(x) \text{ or } \nabla^2f(x)$ of $\large f$ should be positive-semidefinite.


**Solving $\large A\mathbf{x}=\mathbf{b}$**:
![[Machine Learning Algorithms-20260514035553115.webp|476]]
![[Machine Learning Algorithms-20260514035603625.webp|478]]

We can use gradient descent to solve $\large A\mathbf{x} = \mathbf{b}$ equation and find $\large \mathbf{x}$ by considering $\large A\mathbf{x}-\mathbf{b}$ as a gradient vector of some function.

We can use gradient descent on $\large f(\mathbf{x})=\frac{1}{2}\mathbf{x}^TA\mathbf{x}-\mathbf{b}^T\mathbf{x}$ to find a point $\large \mathbf{x}$ where $\large A\mathbf{x} \approx \mathbf{b}$ When:
- $\large A$ is a symmetric matrix ($\large A_{ij}=A_{ji}$)
>Because if $\large A$ is symmetric then the gradient of $\large f(x)$ will be $\large AX-B$.
- $\large A$ is a positive-semidefinite matrix.
>Because we need $\large f(x)$ to be a convex function so its Hessian matrix $\large \nabla^2f(x)$ which is $\large A$ has to be positive-semidefinite.

So we can use gradient descent to solve $\large A\mathbf{x}=\mathbf{b}$ equation where $\large A$ is a symmetric positive-semidefinite matrix.

###### **<mark style="background: #ADCCFFA6;">Linear regression problems</mark>**

We use gradient descent and all different forms of it in almost every problem in machine learning.
One of the problems where we use gradient descent in machine learning is **linear regression**.

**Linear regression**:
- Linear regression is one of the supervised learning problems.
- We have a set of $\large m$ samples. each sample $\large (\mathbf{x}^{(i)}, \mathbf{y}^{(i)})$ has its features vector $\large \mathbf{x}^{(i)}=\left(\begin{matrix}\mathbf{x}^{(i)}_{1}\\\mathbf{x}^{(i)}_{2}\\\dots\\\mathbf{x}^{(i)}_{n}\end{matrix}\right)$ and its label $\large \mathbf{y}^{(i)}$.

The goal is to compute the best linear relationship between the $\large \mathbf{x}^{(i)}$ values and $\large \mathbf{y}^{(i)}$:
$$\large
f: \mathbb{R}^n\to \mathbb{R} \qquad f(x) = w_{0}+ \sum^{n}_{j=1}w_{j}x_{j} \qquad f(\mathbf{x}^{(i)})\approx \mathbf{y}^{(i)}
$$
To find the best model we have to define a cost function $\large J(\mathbf{w},w_{0})$  and run gradient descent on it to find the best weights $\large \mathbf{w}=\left(\begin{matrix}w_{1}\\w_{2}\\\dots\\w_{n}\end{matrix}\right)$and $\large w_{0}$ that minimize the $\large J(\mathbf{w},w_{0})$.
>SSE (sum of squared errors) cost function:
$$\large
\begin{align}
J(\mathbf{w},w_{0})=\sum^{m}_{i=1}(e^{(i)})^2&=\sum^{m}_{i=1}(f(\mathbf{x}^{(i)})-\mathbf{y}^{(i)})^2 \\ \\
&=\sum^{m}_{i=1}(w_{0}+ \sum^{n}_{j=1}w_{j}x^{(i)}_{j} -\mathbf{y}^{(i)})^2
\end{align}
$$

You can check the below images of the cost function and the model itself as an example of solving linear regression problems by gradient descent.

![[Machine Learning Algorithms-20260628165851422.webp]]

![[Machine Learning Algorithms-20260628165956783.webp]]

![[Machine Learning Algorithms-20260628170002561.webp]]

What is the gradient of SSE cost function?
$$\large
\begin{align}
\nabla \mathbf{J}(\mathbf{w},w_{0})&=\nabla\left(\sum^{m}_{i=1}(w_{0}+ \sum^{n}_{j=1}w_{j}x^{(i)}_{j} -\mathbf{y}^{(i)})^2\right) \\ \\
&= \sum^{m}_{i=1}\nabla\left((w_{0}+\sum^{n}_{j=1}w_{j}x^{(i)}_{j} -\mathbf{y}^{(i)})^2\right) \\\\
&=\sum^{m}_{i=1} \left(\begin{matrix}
2(w_{0}+\sum^{n}_{j=1}w_{j}x^{(i)}_{j} -\mathbf{y}^{(i)})\times1 \\
2(w_{0}+\sum^{n}_{j=1}w_{j}x^{(i)}_{j} -\mathbf{y}^{(i)})\times x^{(i)}_{1} \\
2(w_{0}+\sum^{n}_{j=1}w_{j}x^{(i)}_{j} -\mathbf{y}^{(i)})\times x^{(i)}_{2} \\
. \\
. \\
2(w_{0}+\sum^{n}_{j=1}w_{j}x^{(i)}_{j} -\mathbf{y}^{(i)})\times x^{(i)}_{n}
\end{matrix}\right) \\ \\
&=\sum^{m}_{i=1}2(w_{0}+\sum^{n}_{j=1}w_{j}x^{(i)}_{j} -\mathbf{y}^{(i)})\left(\begin{matrix}
1\\x^{(i)}_{1}\\x^{(i)}_{1}\\\dots \\x^{(i)}_{n}
\end{matrix}\right)
\end{align}
$$

>According to the $\large \nabla J(\mathbf{w}, w_{0})$ that we calculated, it takes $\large O(mn)$ to compute the gradient which is linear in the input size.

##### Regularization
Sometimes the model (hypothesis) may be so complicated by having more parameters, being polynomial instead of linear and etc, these all cause the model to overfit (memorizing) the training data, instead of learning it.
Regularization involves some techniques inorder to avoid overfitting the training data.
It often involves <mark style="background: #FFF3A3A6;">adding a term to the cost function</mark>, or adding a <mark style="background: #FFF3A3A6;">constraint to the parameter points</mark>.

>Adding constraint to the parameter points is exactly what we saw in unconstrained gradient descent.

>Adding this constraint controls the complexity of the model, as the number of values $\large w_{j}$ that can have large absolute value is now limited.

Let's see an example of that:
- consider the constrained gradient descent
- Assume we add the constraint $\large ||\mathbf{w}||\leq B$
- Projection function: $\large \prod_{k}(\mathbf{w}')=\mathbf{w}'B/||\mathbf{w}'|| =\mathbf{w}$

- With this constraint we can say that $\large L=||\nabla J(\mathbf{w})||=O(B)$ and also $\large R=O(B)$:
for simplicity let's consider $\large \mathbf{w}=\left(\begin{matrix}w_{0}\\w_{1}\\\dots\\w_{n}\end{matrix}\right), \quad \mathbf{x}^{(i)}=\left(\begin{matrix}1\\x^{(i)}_{1}\\x^{(i)}_{2}\\\dots \\x^{(i)}_{n}\end{matrix}\right)$
proof of $\large L=O(B)$:
$$\large
\begin{align}
||\nabla J(\mathbf{w})||&= ||\sum^{m}_{i=1}(\mathbf{w}^T\mathbf{x}^{(i)}-y^{(i)})\mathbf{x}^{(i)}|| \\
&\leq \sum^{m}_{i=1}\left(||\mathbf{w}||.||\mathbf{x}^{(i)}||+||y^{(i)}||\right).||\mathbf{x}^{(i)}|| \\
&\leq\sum^{m}_{i=1}\left(B.||\mathbf{x}^{(i)}||^2+||y^{(i)}||.||\mathbf{x}^{(i)}||\right) \\
&=B\sum^{m}_{i=1}||\mathbf{x}^{(i)}||^2+\sum^{m}_{i=1}||y^{(i)}||.||\mathbf{x}^{(i)}|| \\
&=Bc_{1} + c_{2}=O(B)
\end{align}
$$
proof of $\large R=O(B)$:
$$\large
||\mathbf{w}^{(0)}||\leq B,\ ||\mathbf{w}^{*}||\leq B \implies R= ||\mathbf{w}^{(0)}-\mathbf{w}^{*}|| \leq2B
$$

- The error bound $\large RL/\sqrt{ T }$ also becomes $\large O(B^2/\sqrt{ T })$.