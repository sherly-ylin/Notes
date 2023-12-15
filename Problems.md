- [DP](#dp)
  - [LIS类](#lis类)
  - [Knapsack类](#knapsack类)
- [Array](#array)
  - [Two-Pointer](#two-pointer)
- [Graph](#graph)
- [Flow](#flow)



# Array
Two-Pointer
---
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

## LIS类
#516 Longest Palindromic Subsequence

## Knapsack类
> Idea: for each item: [pick it] OR [not pick it]

**- 0/1 Knapsack in class (supply: 1)**
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

**#746	Min Cost Climbing Stairs**
- Input: array A of n positive int (cost of landing)
  - Start at A[1] or A[2], can jump 1 or 2 step
- Goal: min cost to jump off A 
```
OPT[i] = min cost to land on A[i]
OPT[1] = A[1]; OPT[2] = A[2]
OPT[i] = A[i] + min(OPT[i-1],   # land on A[i-1]
                    OPT[i-2])   # not land on A[i-1]
return min(OPT[n-1], OPT[n])
```
----
**#53 Max Subarray**


**#416 Partition Equal Subset Sum**

**#674 Longest Increasing Subarray**

---
**#121 Best Time to Buy and Sell Stock**
- Input: Array A
- Goal: find i < j, s.t. A[j]-A[i] is maximized
```
d=[0]*n
min_i = A[1]
for j = 2,...,n:
    d[i] = A[j]-min_i
    min_i = max(A[j], min_i)
```
**#1014 Best Sightseeing Pair**
- Input: Array A
- Goal: find i,j s.t. f(i,j)= A[i]+A[j]+i-j is maximized
  

**-SCI Scheduling Intervals**

**SCI Max Reward (MIS)**

**SCI Max Reward II**







# Graph
**Finding Negative Cycle [KT]**
> DP version of Bellman-Ford
> 

**Idea:** Run Bellman

**Detect Negative Cycle**
> Recall: input to **Bellman-Ford** and **Floyd-Warshall** can't have negative cycles

**Using Bellman-Ford:** 
- relax all edges the nth times (instead of n-1):
  - if d[u]+l(u,v) < d[v] for any edge (u,v) #can find a shorter path -- negative cycle exists

**Using Floyd-Warshall:**


**Shortest Cycle**


# Flow

**Bipartite Matching Max Product**
- Input: 2 arrays of n integers X, Y 
- Goal: Find a matching X->Y s.t. maximize ∑xiyi
```
Idea: Add s, t vertices: 
  - (s,xi) w/ c(e)=xi; (X,Y) w/ c(e)=inf; (yi,t) w/ c(e)=yi
```


