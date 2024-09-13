## 72. Edit Distance

Given two strings `word1` and `word2`, return the minimum number of operations required to convert `word1` to `word2`.

You have the following three operations permitted on a word:

- Insert a character
- Delete a character
- Replace a character
 
Example 1:
```
Input: word1 = "horse", word2 = "ros"
Output: 3
```
Explanation: 
- horse -> rorse (replace 'h' with 'r')
- rorse -> rose (remove 'r')
- rose -> ros (remove 'e')
Solution:

<details>
<summary>Memoization</summary>
<br>
(i) When the characters match
  
- if(S1[i]==S2[j]), decrement both i and j by 1.
  
(ii) When the characters don’t match

- if(S1[i] != S2[j]) is true,
  - Case 1: Inserting a character: return 1+ f(i,j-1) as i remains there only after insertion and j decrements by 1
  - Case 2: Deleting a character: j remains at its original index and we decrement i by 1, recursively call 1+f(i-1,j).
  - Case 3: Replacing a character:  decrement both i and j by 1. As the number of operations performed is 1, we will return 1+f(i-1,j-1).

```cpp
class Solution {
public:
// MEMOIZATION:
    int solve(string word1, string word2,int i, int j,vector<vector<int>> &dp){
        if(i<0) return j+1;
        if(j<0) return i+1;
        if(dp[i][j] !=-1)return dp[i][j];
        if(word1[i] == word2[j]) return dp[i][j] = solve(word1,word2,i-1,j-1,dp);
        else{
            return 1 + min(solve(word1,word2,i-1,j-1,dp), 
                        min(solve(word1,word2,i-1,j,dp),
                            solve(word1,word2,i,j-1,dp)
                        ));
        }

    }
    int minDistance(string word1, string word2) {
        int n = word1.size(), m = word2.size();
        vector<vector<int>> dp(n,vector<int> (m,-1));
        return solve(word1,word2,n-1,m-1,dp);
    }
};
```
Time Complexity: O(N*M), N*M states therefore at max ‘N*M’ new problems will be solved.

Space Complexity: O(N*M) + O(N+M), recursion stack space(O(N+M)) and a 2D array ( O(N*M)).

</details>

<details>
<summary>Tabulation</summary>
<br>

 ```cpp
int minDistance(string word1, string word2) {
        int n = word1.size(), m = word2.size();
        vector<vector<int>> dp(n+1,vector<int> (m+1,0));
        for(int i=0;i<=n;i++){
            dp[i][0] = i;
        }
        for(int j = 0;j<=m;j++){
            dp[0][j] = j;
        }
        for(int i=1;i<=n;i++){
            for(int j = 1;j<=m ;j++){
                if(word1[i-1] == word2[j-1]) dp[i][j] = dp[i-1][j-1];
                else dp[i][j] = 1 + min(dp[i-1][j-1], min(dp[i-1][j],dp[i][j-1]));
            }
        }
        return dp[n][m];
    }
```
Time Complexity: O(N*M), two nested loops

Space Complexity: O(N*M), array of size ‘N*M’. 
</details>
