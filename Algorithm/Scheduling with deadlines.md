There are some jobs that a processor has to do in a limited amount of time .

##### Job :
- Deadline
- value
- Needs a **unit of time** to get done

We have totally **$\large n$ units of time**, our purpose is to schedule the jobs so that at last done jobs would have the **most total possible value** .

**There are two implementations :**
1. By array
2. By disjoint sets

## Implementation By Array

#### Variables

- `j[0..n]`: Schedule Array 
  `j[i]` : Return the number of the job that is done at time `i` .

- `d[1..n]`: Deadlines array, jobs deadlines are stored in it.

- `k`: The numbers of jobs which are already in the schedule.

> Note: The `k` jobs in the array `j` are in order of **increasing deadline**.

> Note: The deadline array in **initially sorted** in the **decreasing order** of jobs **values** .

### Implementation
![[Excalidraw/Drawing 2024-10-12 22.03.37.excalidraw.md#^group=eRmNR_ZWlY7BGEJvV1ylE|700]]

![[Excalidraw/Drawing 2024-10-12 22.03.37.excalidraw.md#^group=30VNLIc-TkzPY5hUxKK81|500]]

---

![[Excalidraw/Drawing 2024-10-12 22.03.37.excalidraw.md#^group=9VgWjIoHLKB4YW4qWUriG|500]]

---
![[Excalidraw/Drawing 2024-10-12 22.03.37.excalidraw.md#^group=l9DYlnHaRTNoqQ5O0lXZd|500]]

---
![[Excalidraw/Drawing 2024-10-12 22.03.37.excalidraw.md#^group=AuvY2oFayN7NAuM98MPFh|500]]

---
![[Excalidraw/Drawing 2024-10-12 22.03.37.excalidraw.md#^group=1iWOUEQLI3AyFm43ZPT_A|600]]

### Code
![[Drawing 2024-10-12 21.46.39.excalidraw.svg]]

### Running Time

To find an upper bound for the algorithm, we have to assume we have the worst case of the input `d[0..n]` :
The worst case is when the jobs are in order of **decreasing deadline** in `d[0..n]`.\

![[Drawing 2024-10-12 21.46.39.excalidraw 1.svg]]

---
## Implementation by Disjoint sets

### Variables

- `disjoint sets`: for each time position we create a disjoint set

![[Scheduling with deadlines-20241012174902711.webp]]

- `j[0..n]`: Schedule Array 
  `j[i]` : Return the number of the job that is done at time `i` .
  
- `F[0..n]`: An array that holds the smallest members of the sets. 
  `F(K)` : Smallest member of the set with `K` representative.

- `d[1..n]`: Deadlines array, jobs deadlines are stored in it.

- `k`: The numbers of jobs which are already in the schedule.


> Note: The deadline array in **initially sorted** in the **decreasing order** of jobs **values** .


### Implementation
![[Excalidraw/Drawing 2024-10-12 18.37.47.excalidraw.md#^group=ywoPuJQABCccd-hWvqAwN|700]]



![[Excalidraw/Drawing 2024-10-12 18.37.47.excalidraw.md#^group=AGh-3xMZsrWghhldwWmal|700]]


![[Excalidraw/Drawing 2024-10-12 18.37.47.excalidraw.md#^group=G2qchSwV2qEI09QZJpqVa|700]]


![[Excalidraw/Drawing 2024-10-12 18.37.47.excalidraw.md#^group=S184jxSe-QKgf0_X7hoX1|700]]


![[Excalidraw/Drawing 2024-10-12 18.37.47.excalidraw.md#^group=-WbOBQ3-CqftW3JvMKcbV|700]]

![[Excalidraw/Drawing 2024-10-12 18.37.47.excalidraw.md#^group=vdlrgYIluJFSlCN8zUkZ4|700]]


![[Excalidraw/Drawing 2024-10-12 18.37.47.excalidraw.md#^group=o4IGbO6PBZALh2E98jFgF|700]]


### Code
![[Drawing 2024-10-06 00.45.34.excalidraw.svg]]
### Running Time
$$\Large\Theta(n) + \Theta(n \log n)\text{(for sorting)} = \Theta(n\log n)$$
