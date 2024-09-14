## [1547. Minimum Cost to Cut a Stick](https://leetcode.com/problems/minimum-cost-to-cut-a-stick/description/)

Given a rod of length `N` inches and an array `price[]` where `price[i]` denotes the value of a piece of rod of length i inches (1-based indexing). 

Determine the maximum value obtainable by cutting up the rod and selling the pieces. Make any number of cuts, or none at all, and sell the resulting pieces.

Example 1
```
Input: price = [1, 6, 8, 9, 10, 19, 7, 20], N = 8

Output: 25

```
Explanation: Cut the rod into lengths of 2 and 6 for a total price of 6 + 19= 25.

### Solution:

<details>
  <summary>RECURSIVE</summary>
  <br>
  
```cpp
class Solution{
  public:
      int solve(int n, vector<int> &price, int ind){
        if(ind == 0)return price[0]*n;
        int notpick = solve(n,price,ind-1);
        int pick = -1e9;
        int len = ind + 1;
        if(len <= n) pick = price[ind] + solve(n-len,price,ind);
        return max(pick,notpick);
    }
    int RodCutting(vector<int>& price, int n) {
        return solve(n,price,n-1);
    }
};
```
- Time Complexity: O(2^N)

- Space Complexity:O(N)

</details>
<details>
  <summary>MEMOIZATION</summary>
  <br>
  
```cpp
class Solution{
  public:
      int solve(int n, vector<int> &price, int ind, vector<vector<int>> &dp){
        if(ind == 0)return price[0]*n;
        if(dp[ind][n]!=-1)return dp[ind][n];
        int notpick = solve(n,price,ind-1,dp);
        int pick = -1e9;
        int len = ind + 1;
        if(len <= n) pick = price[ind] + solve(n-len,price,ind,dp);
        return dp[ind][n] = max(pick,notpick);
    }
    int RodCutting(vector<int>& price, int n) {
      vector<vector<int>> dp(n, vector<int> (n+1,-1));
      return solve(n,price,n-1,dp);
    }
};

```
Time Complexity:O(N*Rod length)

Space Complexity:O(N*rod length) + O(N)

</details>
<details>
  <summary>TABULATION</summary>
  <br>

```cpp
class Solution{
  public:
    int RodCutting(vector<int>& price, int n) {
      vector<vector<int>> dp(n, vector<int> (n+1,0));
      for(int i = 0;i<=n;i++) dp[0][i] = price[0] * i;
      for(int i=1;i<n;i++){
        for(int j=1;j<=n;j++){
          int notpick = dp[i-1][j];
          int pick = -1e9;
          int len = i+1;
          if(len<=j) pick = price[i] + dp[i][j-len];
          dp[i][j] = max(pick,notpick);
        }
      }
      return dp[n-1][n];
    }
};

```
Time Complexity:O(N*(rod length)

Space Complexity:O(N*(rod length))

</details>
<details>
  <summary>SPACE OPTIMIZATION  </summary>
  <br>

```cpp
class Solution{
  public:
    int RodCutting(vector<int>& price, int n) {
      vector<int> prev(n+1,0), cur(n+1,0);
      for(int i = 0;i<=n;i++) prev[i] = price[0] * i;
      for(int i=1;i<n;i++){
        for(int j=1;j<=n;j++){
          int notpick = prev[j];
          int pick = -1e9;
          int len = i+1;
          if(len<=j) pick = price[i] + cur[j-len];
          cur[j] = max(pick,notpick);
        }
        prev=cur;
      }
      return prev[n];
    }
};

```
Time Complexity:O(N*(rod length)

Space Complexity:O(rod length)

</details>
