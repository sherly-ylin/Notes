- [Array](#array)
  - [Two-Pointer](#two-pointer)
- [DP](#dp)
  - [LIS-like](#lis-like)
      - [**LIS - O(n^2)**](#lis---on2)
- [2 loops: i:n-\>1; j:1-\>n](#2-loops-in-1-j1-n)
- [Proof](#proof)
      - [Prove optimal and feasible (SCI Greedy)](#prove-optimal-and-feasible-sci-greedy)




# Array
## Two-Pointer
**#905 Array By Parity**
- Input: array A 
- Goal: sort A s.t. even numbers come before odd numbers
```
two pointers i=1, j=n
while i<j:  # 4 cases
    (1) A[i] = even & A[j] = even: i++
    (2) A[i] = even & A[j] = odd: i++, j--
    (3) A[i] = odd & A[j] = even: swap A[i], A[j], i++, j--
    (4) A[i] = odd & A[j] = odd: j--
```
---
**#344 Reverse String**

**#349 Intersection of Two Arrays**

**#977 Squares of a Sorted Array**


# DP

## LIS-like
> either attach to previous, or just be itself alone
#### **LIS - O(n^2)**
- **Input**: array A in n integers
- **Goal**: Find LIS / length of LIS
- **Idea**: either include max(previous LIS), or not -- only A[i] (d[i]=1)
```
OPT[i] = the length of LIS in A[1:i] ending with A[i]
OPT[1] = 1
OPT[i] = 1 + max(OPT[j]), for i≥2, for all j<i s.t. A[j]<A[i]
LIS(A):
  d=[1]*n
  for i = 2,...,n:
    for j = 1,...,i:
      if A[j]<A[i] and d[i]< d[j]+1:
        d[i] = d[j]+1
return max(d)
```
---
**#Leetcode 674 Longest Increasing Subarray - O(n)**
- **Input**: array A of n integers
- **Goal**: find length of LI subarray
- **Idea**: either can include subarray ending w/ A[i-1], or can't
```
OPT[i] = length of LI subarray ending w/ A[i]
OPT[1] = 1
OPT[i] = OPT[i-1]+1, if A[i]>A[i-1]
				 1, otherwise
ALG(A):
  d = [1]*n
  for i = 2,...,n:
    if A[i]>A[i-1]:
      d[i] = d[i-1]+1
return max(d)
```
---
**#53 Max Subarray Sum - O(n)**
- **Input**: array A of n integers
- **Goal**: find the contiguous subarray with the largest sum
- **Idea**: either include prev subarray ending w/ A[i-1], or not include -- be just A[i]
```
OPT[i] = max sum of subarray ending w/ A[i]
OPT[1] = A[1]
OPT[i] = max(A[i], OPT[i-1] + A[i])
```	

**#516 Longest Palindromic Subsequence - O(n^2)**
- **Input**: array A
- **Goal**: find the length of the longest palindromic subsequence in A
- **Idea**: two-pointer A[i:j]: either 
    - (1) include i not j -- A[i:j-1] 
    - (2) include j not i -- A[i+1:j]
    - (3) A[i]=A[j], include both: A[i] + A[i+1:j-1] + A[j]
```
OPT[i][j] = length of  longest palindromic subseq in A[i:j]
OPT[i][i] = 1, OPT[i][j] = 0, for i < j 
OPT[i][j] = if A[i]=A[j]: max(d[i][j-1], d[i+1][j])
            otherwise:  max(d[i][j-1], d[i+1][j], 2+d[i+1][j-1]))
# 2 loops: i:n->1; j:1->n
```
**#LeetCode 1143: Longest Common Subsequence**
- **Input**: String A, B
- **Return**: the length of their longest common subsequence, 0 if none
```
OPT[i][j] = length of LCS in A[1:i] and B[1:j]
	OPT[0][j] = 0 
	OPT[i][0] = 0
OPT[i][j] = OPT[i-1][j-1]+1, if A[i]=B[j]
            max(OPT[i-1][j],OPT[i][j-1]), otherwise
		#include this if A[i]=B[j]
		#otherwise check if can include one of A[i],B[j]
```

**LeetCode 1911: Maximum Alternating Subsequence Sum**
- Input: array of positive
- Goal: max alternating sum
- The **alternating sum** of a 0-indexed array: the sum of the elements at even indices minus the sum of the elements at odd indices.

## Knapsack-like
> Idea: for each item: [pick it] OR [not pick it]

**- 0/1 Knapsack in class (supply: 1) O(n^2)**
- Input: n items w/ (v_i, w_i), capacity B
- Goal: find subset of items s.t. ∑wi ***<=*** B, ∑vi maximized
- Return: Max ∑vi within capacity

```
OPT[i][j] = max ∑v in items[1:i] w/ capacity j
OPT[0][0] = 0
OPT[i][j] = OPT[i-1][j]  if wi>j
            max(OPT[i-1][j], vi+OPT[i-1][j-wi]) otherwise
return OPT[n][B]
```
----
**- Knapsack (supply: infinite)**
- Input: n types of coins w/ values v_i (w_i=v_i), capacity/goal B cents
- Goal: 
  - (1) is it possible to make **exactly** B cents?
  - (2) if so, find the min # of coins needed

```
OPT[i][j] = min # of coins to make j cents using coins[1:i]
OPT[0][0] = 0
OPT[i][j] = OPT[i-1][j]      if A[i]>j
            min(OPT[i-1][j], 1+OPT[i][j-vi]) otherwise
return OPT[n][B]
```
----
**#198 House Robber**
- Input: array A of n items, each with value vi
- Goal: max ∑vi, cannot pick 2 consecutive
```
OPT[i] = max ∑vi through A[1:i]
OPT[0] = 0; OPT[1] = A[1]
OPT[i] = max(OPT[i-1],          # not pick it
            OPT[i-2]+A[i])      # pick it
```
**#213 House Robber 2**
- A[1] & A[n] considered consecutive
  
**#746	Min Cost Climbing Stairs O(n)**
- **Input**: array A of n positive int (cost of landing)
  - Start at A[1] or A[2], can jump 1 or 2 step
- **Goal**: min cost to jump off A 
```
OPT[i] = min cost to land on A[i]
OPT[1] = A[1]; OPT[2] = A[2]
OPT[i] = A[i] + min(OPT[i-1],   # land on A[i-1]
                    OPT[i-2])   # not land on A[i-1]
return min(OPT[n-1], OPT[n])
```
----


**#416 Partition Equal Subset Sum**
- **Input**: array A of n pos integers
- **Goal**: determine if A can be partitioned into two subsets with equal sum.
- **Idea**: 0/1 Knapsack, to make sum(A)/2
```
```

**#674 Longest Increasing Subarray**

---
**#121 Best Time to Buy and Sell Stock**
- **Input**: Array A
- **Goal**: find i < j, s.t. A[j]-A[i] is maximized
- **Idea**: find min(A[1:j-1]), keep track of min_i when iterating j=1-n>
```
OPT[j]= max profit selling on day j: A[j] - min(A[i]), i<j
OPT[j]
d=[0]*n
min_i = A[1]
for j = 2,...,n:
    d[i] = A[j]-min_i
    min_i = max(A[j], min_i)
```
**#1014 Best Sightseeing Pair**
- **Input**: Array A
- **Goal**: find i,j s.t. f(i,j)= A[i]+A[j]+i-j is maximized
- **Idea**: similar to buy/sell stock, keep track of best_i
```
OPT[j] = max(A[i]+A[j]+i-j) with i<j
OPT[j] = A[j]-j + max(A[i]+i) #i<j>


```
  

**-SCI Scheduling Intervals**



**SCI Max Reward II**

## MIS-like
**MIS (2-subproblem) - O(n) -similar to BFS**
> IS: a subset S of V s.t. no pair shares an edge
- **Input**: Tree T (undirected connected G), each vertex u has weight w(u)>0
- **Goal**: find IS S that maximizes weight ∑w(u) u in S
- **Idea**: 
  - use reverse topolgical ordering - calulate child first
  
	- For each vertx u, let T(u) be the subtree rooted in u
```
OPT_in[u] = weight of MIS of T(u) that include u
OPT_out[u] = weight of MIS of T(u) that exlude u
OPT[u] = weight of MIS if T(u) = max(OPT_in[u],OPT_out[u])
- if u is a leaf:
	OPT_in[u]= w(u)
	OPT_out[u] = 0
- if u has children: (C(u) = set of children of u)
	OPT_in[u] = ∑OPT_out[v], v = child of u (in C(u))
	OPT_out[u] = ∑ max(OPT_in[v],OPT_out[v]) for each child v of u
```
**MIS (1-subproblem) - O(n) -similar to BFS**
- **Idea**: this + [sum(children) or sum(grandchildren)]
```
OPT[u] = weight of MIS if T(u)
- if u is a leaf:
	OPT[u]= w(u)
- if u has children:
	OPT[u] = max(∑OPT_out[v], v = child of u (in C(u))
              w(u) + ∑OPT[x]) for each grandchild x of u
```

**SCI Max Reward (MIS) - O(nlogn)**
- **Input**: Array A if n intervals, each with value vi: [[si,ti,vi]..]
- **Goal**: find subset S of compatible intervals w/ max value
- **Idea**: sort ti increasing order(pick earliest)
```
OPT[i] = max ∑val in A[1:i]
OPT[1] = v1
OPT[i] = max(OPT[i-1], vi + OPT[pi])
        #pi = index of previous interval j s.t tj<si & vj maximized
        #binary search p - O(logn)* n interval
```
# Graph
#### **Finding Negative Cycle [KT]**
> DP version of Bellman-Ford
> 

**Idea:** Run Bellman

#### **Detect Negative Cycle**
> Recall: input to **Bellman-Ford** and **Floyd-Warshall** can't have negative cycles

**Using Bellman-Ford:** 
- relax all edges the nth times (instead of n-1):
  - if d[u]+l(u,v) < d[v] for any edge (u,v) #can find a shorter path -- negative cycle exists

**Using Floyd-Warshall:**
```
ALG(G):
  run Floyd-Warshall to get d = n x n matrix (d[_][_][n])
  for all u in V:
    if d[u][u]<0, then neg cycle exists involving u
    # find shortest cycle
    if d[u][u] < min_cycle_length:
      min_cycle_length = d[u][u]
```

**Shortest Cycle**


# Flow

**Bipartite Matching Max Product**
- Input: 2 arrays of n integers X, Y 
- Goal: Find a matching X->Y s.t. maximize ∑xiyi
```
Idea: Add s, t vertices: 
  - (s,xi) w/ c(e)=xi; (X,Y) w/ c(e)=inf; (yi,t) w/ c(e)=yi
```



# Proof

#### Prove optimal and feasible (SCI Greedy)
1. Feasible: show result ALG satisify conditions
2. Optimal:
   1. Suppose for contradiction ALG is not optimal OPT, i.e. ALG(i) ≠ OPT(i) [their i-th decision is different]
   2. Exchange argument:
      1. Create OPT' = OPT - OPT(i) + ALG(i)