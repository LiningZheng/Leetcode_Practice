Description:
Given a 01 matrix M, find the longest line of consecutive one in the matrix. The line could be horizontal, vertical, diagonal or anti-diagonal.

### 1 DFS
traverse the matrix.
for each element, use dfs to check the max length of the lines the element lies in.

Time: O(N^2)
Space: O(N)

### 2 DP
use a 2D*4 matrix to store the length of the lines until a point, in 4 directions.
Time: O(N^2)
Space: O(N^2)
