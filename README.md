Assignment-03 
Khushi Srivastava
35113302723
CSE-5A

SECTION A – Short Theory 

Q1. List the three ingredients of Dynamic Programming (DP) and write one-line purpose of each.
Ans:
1. Optimal Substructure:  Ensures that the optimal solution to a problem can be constructed from optimal solutions of its subproblems.
2. Overlapping Subproblems: Indicates that the problem’s subproblems repeat, allowing reuse of previously computed solutions.
3. Memoization or Tabulation (Storage of Subproblem Results): Saves the results of subproblems to avoid redundant computation and achieve efficient time complexity.
Pseudo code:
for each subproblem s:
    solve s using smaller subproblems
    store result[s]
return result[main_problem]

Q2. State two differences between DP and Divide & Conquer focusing on subproblem overlap and reuse; give one example for each.
Ans:
Difference 1:  DP solves overlapping subproblems; D&C solves independent ones.
Difference 2:  DP reuses results from previous computations, D&C recalculates.

Example DP:  Fibonacci using memoization.
Example D&C:  Merge Sort or Quick Sort.
Pseudo code:
def fib(n):
    if n<=1: return n
    if n not in memo:
        memo[n] = fib(n-1)+fib(n-2)
    return memo[n]

Q3. Define the Principle of Optimality in one sentence and name one problem satisfying it.
Ans:
A problem satisfies the principle of optimality if its optimal solution contains optimal solutions to all of its subproblems. 
Example: Shortest Path Problem (e.g., Dijkstra’s algorithm).
Pseudo code:

for each vertex v:
    dist[v] = min(dist[u] + weight(u,v))

Q4. Define memoization and contrast it with tabulation in one line each.
Ans:
Memoization: It is a top-down DP approach where results of solved subproblems are stored to avoid re-computation.
Tabulation: It is a bottom-up DP approach where all subproblems are solved iteratively and stored in a table before reaching the final answer.
Pseudo code:
# Memoization
if state not solved:
    solve recursively and store

# Tabulation
for state in order:
    compute using previous states

Q5. Define Branch and Bound (BnB) and explain the role of bounding in pruning in two lines.
Ans:
Branch and Bound systematically explores a search tree using bounds to cut off paths that can’t lead to better solutions.
Bounding helps skip unpromising nodes by calculating upper/lower limits.

Pseudo code:
queue = [root]
while queue not empty:
    node = queue.pop()
    if bound(node) > best:
        branch(node)

SECTION B – Algorithms & Recurrences 

Q6. Matrix Chain Multiplication (A₁:5×4, A₂:4×6, A₃:6×2, A₄:2×7)
a) Recurrence & base:
m[i,i] = 0
m[i,j] = min_{i≤k<j} ( m[i,k] + m[k+1,j] + p[i-1]*p[k]*p[j] )

b) Minimum scalar multiplications: 158
Pseudo code:

for l = 2 to n:
    for i = 1 to n-l+1:
        j = i+l-1
        m[i][j] = min(m[i][k] + m[k+1][j] + p[i-1]*p[k]*p[j])

Q7. Longest Common Subsequence (X='ABCDGH', Y='AEDFHR')
a) Recurrence & base:

LCS(i,0)=0; LCS(0,j)=0
if X[i]==Y[j]: LCS(i,j)=LCS(i-1,j-1)+1
else: LCS(i,j)=max(LCS(i-1,j),LCS(i,j-1))

b) LCS length: 3
Pseudo code:

for i in 1..m:
    for j in 1..n:
        if X[i]==Y[j]: dp[i][j]=dp[i-1][j-1]+1
        else: dp[i][j]=max(dp[i-1][j],dp[i][j-1])

Q8. Optimal Binary Search Tree (keys:10,20,30; p:0.4,0.3,0.3; assume q=0)
a) DP Formulation:

w[i,i-1]=0; e[i,i-1]=0
w[i,j]=w[i,j-1]+p[j]
e[i,j]=min_{r=i..j}(e[i,r-1]+e[r+1,j]+w[i,j])

b) Minimum expected cost: 1.6
Pseudo code:
for l=1..n:
    for i=1..n-l+1:
        j=i+l-1
        e[i][j]=min(e[i][r-1]+e[r+1][j]+w[i][j])
Q9. 0/1 Knapsack – Branch & Bound (W=5; w={2,3,4,5}, p={3,4,5,6})
a) Fractional upper bound formula:

ub(node) = v_curr + Σ [p_k × min(1, (W - w_curr)/w_k)]

(Items sorted by profit/weight ratio.)

b) Nodes:
Level-0: (0,0,7.0)
Level-1 Include item₁: (3,2,7.0)
Level-1 Exclude item₁: (0,0,6.5)
Pseudo code:
while not empty(Q):
    node = Q.pop()
    if node.ub > best:
        expand(node)

Q10. TSP – Dynamic Programming (Held–Karp; 4 cities)
a) Recurrence & final:

C[S,j] = min_{i∈S\{j}} ( C[S\{j},i] + d[i,j] )
Answer = min_{j≠1} ( C[{2..n},j] + d[j,1] )

b) Base entries:

C[{2},2]=d[1,2]; C[{3},3]=d[1,3]; C[{4},4]=d[1,4]
Pseudo code:

for S in subsets({2..n}):
    for j in S:
        C[S][j] = min(C[S-{j}][i]+d[i][j])
final=min(C[{2..n}][j]+d[j][1])
