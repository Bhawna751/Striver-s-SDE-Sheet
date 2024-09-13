## [64. Minimum Path Sum](https://leetcode.com/problems/minimum-path-sum/description/)

Given a `m x n` grid filled with non-negative numbers, find a path from top left to bottom right, which minimizes the sum of all numbers along its path.

Note: You can only move either `down` or `right` at any point in time.

Example 1:
```
Input: grid = [[1,3,1],[1,5,1],[4,2,1]]
Output: 7
```
Explanation: Because the path 1 → 3 → 1 → 1 → 1 minimizes the sum.

Solution:
<details>
  <summary>MEMOIZATION</summary>
  <br>
  
```cpp
class Solution{
public:
    int solve(vector<vector<int>> dp,vector<vector<int>>& grid, int i, int j){
        if(i==0 && j==0) return grid[i][j];
        if(i<0 || j<0) return 1e9;
        if(dp[i][j] != -1) return dp[i][j];
        int up = grid[i][j] + solve(dp,grid,i-1,j);
        int left = grid[i][j] + solve(dp,grid,i,j-1);
        return dp[i][j] = min(left,up);
    }
    int minPathSum(vector<vector<int>>& grid){
        int n = grid.size(), m = grid[0].size();
        vector<vector<int>> dp (n, vector<int>(m,-1));
        return solve(dp,grid,n-1,m-1);
    }
}
```
Time Complexity: O(M*N)

Space Complexity:O((N-1)+(M-1)) + O(M*N)
</details>

Solution:
<details>
  <summary>TABULATION</summary>
  <br>
  
```cpp
class Solution{
public:
    int minPathSum(vector<vector<int>>& grid){
        int n = grid.size(), m = grid[0].size();
        vector<vector<int>> dp (n, vector<int>(m,0));
        dp[0][0] = grid[0][0];
        for(int i=1;i<m;i++){
            dp[0][i] = grid[0][i] + dp[0][i-1];
        }
        for(int i = 1;i<n;i++) dp[i][0] = grid[i][0] + dp[i-1][0];
        for(int i=1;i<n;i++){
            for(int j=1;j<m;j++){
                dp[i][j] = grid[i][j] + min(dp[i-1][j], dp[i][j-1]);
            }
        }
        return dp[n-1][m-1];
    }
}
```
Time Complexity: O(M*N)

Space Complexity:O(M*N)
</details>
