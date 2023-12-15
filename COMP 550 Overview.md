### Content

- [2. Basic Graph](#2-basic-graph)
	- [2.1 BFS](#21-bfs)
	- [2.2 DFS](#22-dfs)
	- [2.3 MST](#23-mst)
		- [Cut Property](#cut-property)
		- [Cycle Property](#cycle-property)
		- [Prim's](#prims)
		- [Kruskal's](#kruskals)
		- [Reverse-Delete](#reverse-delete)
- [3. Greedy](#3-greedy)
	- [3.1 Compatible Intervals](#31-compatible-intervals)
	- [3.2 Fractional Knapsack](#32-fractional-knapsack)
- [4. Dynamic Programming](#4-dynamic-programming)
	- [4.1 Sum of Array](#41-sum-of-array)
	- [4.2 Longest Increasing Subsequence (LIS)](#42-longest-increasing-subsequence-lis)
	- [4.3 0/1 Knapsack](#43-01-knapsack)
	- [4.4 Edit Distance](#44-edit-distance)
	- [4.5 Max Independent Set in Trees](#45-max-independent-set-in-trees)
- [5. Shortest Paths](#5-shortest-paths)
	- [5.1 DAG SSSP](#51-dag-sssp)
	- [5.2 Dijkstra's](#52-dijkstras)
	- [5.3 Bellman-Ford](#53-bellman-ford)
	- [5.4 Floyd-Warshall (APSP)](#54-floyd-warshall-apsp)
	- [Ch.5 Summary (n ≤ m+1, directed)](#ch5-summary-n--m1-directed)
- [6. Flows and Cuts](#6-flows-and-cuts)
	- [6.1 Ford-Fulkerson](#61-ford-fulkerson)
	- [6.2 Bipartite Matching](#62-bipartite-matching)
	- [6.3 Mininum Vertex Cover](#63-mininum-vertex-cover)
- [8. NP-Hard Problems](#8-np-hard-problems)
	- [8.1 NP Complexity](#81-np-complexity)
	- [8.2 3-SAT ≤ IS](#82-3-sat--is)
	- [8.3 VC ≤ DomSet](#83-vc--domset)
	- [8.32 HamPath ≤ HamCycle](#832-hampath--hamcycle)
- [9. 2-Approximation](#9-2-approximation)
	- [9.1 Vertex Cover](#91-vertex-cover)
	- [9.2 Load Balancing](#92-load-balancing)

# 2. Basic Graph

## 2.1 BFS 


Runtime: O(m+n)

## 2.2 DFS 
Pre- and Post- lists
- Set pre value when first visit the vertex
- Set post value when all its children visited and back to it


Runtime: O(m+n)

## 2.3 MST
> **Minimum Spanning Tree**
> - has exactly n-1 edges(w(e)>0), mininum total weight
> - adding any additional cycle will result in cycle
> - 

### Cut Property
- For any S = subset of V (a cut)
- The lightest edge crossing S is in MST

### Cycle Property
- For any cycle C in G, the heaviest edge in C is not in MST

### Prim's
- Choose any vertex s, let S = {s}, F = ø
- Add the lightest edge crossing S to F (Repeat n-1 times)
### Kruskal's
- Sort edges in **increasing** weight
- for each edge e: add e to F if (V,FU{e}) has no cycle
### Reverse-Delete
- Sort edges in **decreasing** order, let F = E
- for each edge e: remove e if (V,F-{e}) still connected



# 3. Greedy

## 3.1 Compatible Intervals 
**Input**: array of intervals {[s1,t1],...,[sn,tn]}

**Goal**: OPT = max subset of compatible intervals
**Idea**: keep picking the interval with the earliest endtime

	ALG: while not all intervals cross:
		find [si,ti] with smallest ti, select it, then cross it, 
		for all non-crossed intervals: 
			cross all intevals conflict with selected

	RT: O(n^2), brute 
		O(n log n), sort the intervals first

## 3.2 Fractional Knapsack 
	Input: capacity B, a list of items 1..n with values v_i>0, weight w_i>0 (1 available each)
	Goal: Pick 0 ≤ x_i ≤1  s.t. maximize ∑(v_i*x_i) while ∑(w_i*x_i)≤B
	ALG: Sort items s.t v1/w1 ≤ v2/w2 ≤ ... ≤ vn/wn
		 then pick as much of each item as possible(x_i=1) in that order s.t total weight ≤ B
	RT: O(n log n)+O(n)?

# 4. Dynamic Programming
**Stadard Procedure**:
[1] Subproblem: OPT[i] = 
[2] Reccurence: OPT[0] = , OPT[1] = , OPT[i] = 
[3] Pseudocode
[4] Return

## 4.1 Sum of Array 
	Input: array A of n integers
	Goal: sum of A
	[1] OPT[i] = sum of A[1:i]
	[2] OPT[1] = A[1]
		OPT[i] = A[i] + OPT[i-1], i>1
	[3] Sum(A): 
			d = [0]*n
			d[1] = A[1]
			for i = 2,...,n:
				d[i] = A[i] + d[i-1]
	[4]		return d[n]
	RT: O(n)

## 4.2 Longest Increasing Subsequence (LIS) 
	Input: array A in n integers
	Goal: Find LIS / length of LIS
	[1] OPT[i] = the length of LIS in A[1:i] ending with A[i]
	[2] OPT[1] = 1
		OPT[i] = 1 + max(OPT[j]), for i≥2, for all j<i s.t. A[j]<A[i]
	[3] LIS(A):
			d=[1]*n
			for i = 2,...,n:
				for j = 1,...,i:
					if A[j]<A[i] and d[i]< d[j]+1:
						d[i] = d[j]+1
	[4]		return max(d)
	RT: O(n^2)

## 4.3 0/1 Knapsack 

	Input: n items, each with value v_i>0, weight w_i>0, capacity B
	Goal: Find subset of items{1,..,n} s.t
		1. feasible: total weight ∑w_i < B
		2. optimal: maximize total value ∑(v_i)
	[1] OPT[i][j] = optimal value chosen from{1,...,i} with capacity j available
	[2] OPT[0][j] = 0
		OPT[1][j] = v_1
		OPT[i][j] = OPT[i-1][j], if w_i > j
					max(v_i + OPT[i-1][j-w_i], OPT[i-1],[j]), otherwise
	[3] Knapsack(V, W):
			d = (n+1) x B
			for i in range(n+1):
				d[0][i]=0
				d[1][i]= V[1]
			for i = 2,...,n:
				for j = 1,...,B:
					if W[i]>j:
						d[i][j]= d[i-1][j]
					else:
						d[i][j]= max(d[i-1][j], V[i]+OPT[i][j-W[i]])
	[4]		return d[n][B]
	RT: O(nB)

## 4.4 Edit Distance

	Moves: 1. insert a char, 2. delete a char, 3. replace a char with another
	Input: two strings A, B (arrays of characters), |A|=n, |B|=m
	Goal: The mininum moves to convert A to B
	[1] OPT[i][j]= min moves to convert A[1:i] to B[1:j]
	[2] OPT[0][0]= 0
		OPT[1][1]= 0, if A[1] = B[1]; 1, otherwise
		OPT[i][j]= min( 1 + OPT[i][j-1],	# ED(A[i],B[j-1]) + insert B[j]
						1 + OPT[i-1][j],	# delete A[i] + ED(A[i-1],B[j])
						0/1 + OPT[i-1][j-1]) # ED(A[i-1],B[j-1]) + replace A[i] w/ B[j]
	RT: O(mn)

## 4.5 Max Independent Set in Trees 

	Independent set: a subset S of vertices s.t. no pair shares an edge
	Input: Tree T (undirected connected G), each vertex u has weight w(u)>0
	Goal: find IS S that maximizes weight ∑w(u) u in S
	- For each vertx u, let T(u) be the subtree rooted in u

```
	[1] OPT_in[u] = weight of MIS of T(u) that include u
		OPT_out[u] = weight of MIS of T(u) that exlude u
		OPT[u] = weight of MIS if T(u)
	[2] - if u is a leaf:
			OPT_in[u]= w(u)
			OPT_out[u] = 0
		- if u has children: (C(u) = set of children of u)
			OPT_in[u] = ∑OPT_out[v], v = child of u (in C(u))
			OPT_out[u] = ∑ max(OPT_in[v],OPT_out[v]) for each child v of u
	# Reverse Topological Ordering (w/DFS) -> we need to process children before parents
	[3]Peudocode:
		ALG(T):
			d_in[u] = w(u) for all u in V
			d_out[u] = [0]*n
			R = reverse topological ordering of T
			for u in R:
				for each child v of u:
					d_in[u]+= d_out[v]
					d_out[u]+= max(OPT_in[v],OPT_out[v])
			root = R[n]
	[4]		return max(OPT_in[root],OPT_out[root])
```
	RT: (similar to BFS)
		  O(m+n) - topological sort w/DFS
		+ O(m+n) - O(∑out-deg(u)) for each u in V
		= O(n) (T is a tree -> m = n-1)
------------------------------------------------------------------
# 5. Shortest Paths

## 5.1 DAG SSSP 

	Input: directed acyclic graph G, starting vertex s
	Goal: find the shortest paths from s to v for all other vertices 
			(this ALG returns the distance)
```
>DP version:
	[1] OPT[v] = dist from s to v
	[2] OPT[s] = 0
		OPT[v] = min(OPT[v], OPT[u]+l(u,v)), (u,v) is an edge, ie, u is in-neighbor
	[3]Pesudocode:
		ALG(G,s):
			d = [inf]*n, #p=[]*n
			d[s] = 0
			for each vertex v:
				for each edge entering v (u,v): 
					d[u]= min(d[v], d[u]+l(u,v))	# relaxing the edge(u,v)
					#with parent pointer
					#if d[u]+l(u,v) < d[v]:
					#	d[v] = d[u]+l(u,v)
					#	p[v] = u
	[4]		return d, p

	RT: ≈ BFS
		∑in-deg(u)= m 	#line 138-139
		O(m+n)=O(m)	#assume s can reach all of V
```
```
	>BFS version:
		ALG(G,s): 
			d=[inf]*n
			d[s]=0
			for each vertex u in topological order:
				for each out-neightbor v of u:
					d[v] = min(d[v], d[u]+l(u,v))
			return d
```

## 5.2 Dijkstra's 
	Input: directed G, starting vertex s, edge length l(u,v)≥0
	Goal: SSSP
	Idea: BFS + Prim's
		- find u with smallest d[u]				#O(n)
		- relax (u,v) for all out-nb v of u   	#O(m)	n≤m+1
		- repeat
	Dijkstra's(G,s):
		d = [inf]*n, d[s]=0
		S = ø, Q = V
		while Q ≠ ø:								# n iterations
			add vertex u with smallest d[u] to S  	# O(n)
			remove u from Q
			for each out-nb v of u:					# O(out-deg(u)) = O(n) - 
				d[v]= min(d[v], d[u]+l(u,v))
		return d
	RT:O(n^2)
	> Dealing with vertex length:
	#
	#

## 5.3 Bellman-Ford 

	Input: directed G, vertex s, negative edge allowed, no negatic cycle
	Goal: SSSP
```
	BF(G,s):
		d = [inf]*n, d[s]=0
		for i = 1,...,n-1:			# n-1 iterations
			for each edge (u,v):	# O(m)
				relax (u,v)			# d[v]= min(d[v]+l(u,v))
		return d
```
	RT: O(mn)
	#Use Bellman-Ford to detect negative cycle:
		- relax all edges one more time(the Nth time):
			- if d[u]+l(u,v)<d[v] for any edge (u,v) -- negative cycle exists

## 5.4 Floyd-Warshall (APSP) 

	Input: same as BF (directed G, s, neg edges ok, no neg cycle)
	Goal: distance from u to v for all u,v in V
	Output: n x n matrix d s.t. d[u][v]= dist(u,v)
	Floyd-Warshall is a DP!!!
	[1] OPT[u][v][r] = dist(u,v) using only vertices 1-r in between u,v
						# u,v = 1~n; r = 0~n
	[2] OPT[u][v][0] = l(u,v), if (u,v) in E
					   inf, otherwise
		OPT[u][v][r] = min(OPT[u][v][r-1],						#not using r
						   OPT[u][r][r-1]+OPT([r][v][r-1]))		#u->r + r->v
```

	[3] FW(G):
			d = n x n x (n+1), all 0's		
			#r=0
			for u in V:
				for v in V:
					if (u,v) in E:
						d[u][v][0] = l(u,v)
					elif u ≠ v: 
						d[u][v][0] = inf
			for r = 1,...,n:
				for u in V:
					for v in V:
						d[u][v][r] = min(d[u][v][r-1], d[u][r][r-1]+d[r][v][r-1])
	[4]		return d[-][-][n]
```
	RT: O(n^3)

## Ch.5 Summary (n ≤ m+1, directed)

|SSSP|  edge length   |        ALG        |  RT  |
|----|------------------|------------------|------|
|    |  all = 1         |       BFS      | O(m) |
|    |  any, no cycle   |      DAG DP    | O(m)
|    |  all >= 0         |   Dijkstra's   | O(n^2)
|    | any, no neg cycle |    Bellman-Ford | O(mn)
|APSP| any, no neg cycle | 	Floyd-Warshall | O(n^3)
|SSSP| with neg cycle   | unlikely in polynomial time


# 6. Flows and Cuts 
**Flow network**: a directed graph G=(V,E), each edge has capacity c(e), with source s, sink t - no edges entering s, no edges leaving t
**Cut S**: any subset of V
**s-t cut**: subset of V contains s but not t
**Flow**: E -> IR (a value)
**Value of f:** f_out(s) = ∑f(e) leaving s = f_in(t)
**Feasible flow**:	
1. flow ≤ capacity: for all e in E, f(e)≤c(E)			
2. flow conservation at u: for all u ≠ s,t: f_in(u) = f_out(u)
   1.  <=> ∑f(e) entering u = ∑f(e) leaving u


## 6.1 Ford-Fulkerson 

**Idea**: Given G, flow f, construct Gf 'residual graph' = 
(allow ALG to undo path decisions )
```
Gf(G,f):
	for each edge e=(u,v) in G:
		if f(e)<c(e):		#forward edge
			add (u,v) to Gf with c(e)-f(e) capacity
		if f(e)>0:			#backword edge
			add (v,u) to Gf with f(e) capacity
	return Gf
```
```
FF(G,s,t):
	f = 0, Gf = G
	while there exist a s-t path in Gf: 	# using DFS
		find ∆P= min/bottleneck capacity of edges in P
		# augment f along P:
		# f += ∆P ?
		for each edge e=(u,v) in P:
			# if e is in original graph
			if e is forward edge: 	
				f(u,v)+=∆P
			else:
				f(v,u)-=P
			Gf = Gf(G,f)
	return f
```
**Runtime**: O(m|f|)

**Lemma**: For all feasible flow f, all s-t cut S,
```
|f| = f_out(S)-f_in(S) = f_out(s) ≤ c(S) 
c(S) = ∑c(e), e leaving S
```


**Minimum cut** = set of vertices reachable from s in last Gf from Ford-Fulkerson
			|f| = c(S), S = minimum cut

**Theorem**: max flow value = min cut capacity (value)

## 6.2 Bipartite Matching
A **matching M** is a subset of edges that don't share any endpoints
**Input**: Bipartite undirected G. 		# G=(V,E), V=(L,R)
**Goal**: find a subset of edges M such that 
1. **feasible**: for all u in V, u in incident to at most 1 edge in M;
				  <=> no edges in M share an endpoint
2. **optimal**: maximize the # of edge in M, |M|

```
ALG(idea):
	1. construct a flow network (G',s,t,c=1)
		- adding s pointing to vertices in L, t pointed by vertices in R
		- undirected edges becomes L pointing to R
		- all edges have capacity 1
	2. Find max s-t flow in G'	(using 6.1 Ford-Fulkerson)
	3. Convert f into solution for original problem
		M = {{u,v}: u in L, v in R, f(u,v)=1}, subset of original E
```

**Corollary**: feasible flow in G' <=> matching in G (1-1 corespondence)

## 6.3 Mininum Vertex Cover 

**Vertex cover**: subset of V that covers all edges in E
**Input**: Bipartite G
**Goal**: find min vertex cover S (subset of V)
1. Feasible: for all e in E, e is insident to at least 1 vertex in S
2. Optimal minimize |S|
```
ALG(G):
	Construct flow network G' (similar to 6.2, but L->R edges capacity inf ♾️)
	Find min s-t cut S in G' (6.1)
	return (L\S)U(R⋂S)

```

**Corollary**: feasible flow in G' <=> matching in G 	#|f| = |M|
6---
residual graph
min s-t cut
max flow
min vertx cover



# 8. NP-Hard Problems

## 8.1 NP Complexity 

## 8.2 3-SAT ≤ IS 

## 8.3 VC ≤ DomSet 

## 8.32 HamPath ≤ HamCycle 


# 9. 2-Approximation

## 9.1 Vertex Cover 

## 9.2 Load Balancing 