## [1143. Longest Common Subsequence](https://leetcode.com/problems/longest-common-subsequence/description/)

Given two strings `text1` and `text2`, return the length of their longest common subsequence. If there is no common subsequence, return 0.

A subsequence of a string is a new string generated from the original string with some characters (can be none) deleted without changing the relative order of the remaining characters.

For example, `"ace"` is a subsequence of `"abcde"`.
A common subsequence of two strings is a subsequence that is common to both strings.

Example 1:
```
Input: text1 = "abcde", text2 = "ace" 
Output: 3
```
Explanation: The longest common subsequence is "ace" and its length is 3.

Example 2:
```
Input: text1 = "abc", text2 = "abc"
Output: 3
```
Explanation: The longest common subsequence is "abc" and its length is 3.

Solution: 
```cpp
class Solution {
public:
//MEMO: 
    // int solve(string &text1, string &text2, int i,int j,vector<vector<int>> &dp){
    //     if(i<0 || j<0) return 0;
    //     if(dp[i][j]!=-1)return dp[i][j];
    //     if(text1[i] == text2[j]) return dp[i][j] = 1+ solve(text1,text2,i-1,j-1,dp);
    //     else return dp[i][j] = max(solve(text1,text2,i,j-1,dp), solve(text1,text2,i-1,j,dp));
    // }
    // int longestCommonSubsequence(string text1, string text2) {
    //     int n=text1.size(), m=text2.size();
    //     vector<vector<int>> dp(n,vector<int>(m,-1));
    //     return solve(text1,text2,n-1,m-1,dp);
    // }
//Time Complexity: O(N*M)
//Reason: There are N*M states therefore at max ‘N*M’ new problems will be solved.
//Space Complexity: O(N*M) + O(N+M)
//Reason: We are using an auxiliary recursion stack space(O(N+M)) (see the recursive tree, in the worst case, we will go till N+M calls at a time) and a 2D array ( O(N*M)).

//  TABULATION: 
//     int longestCommonSubsequence(string text1, string text2){
//         int n=text1.size(), m=text2.size();
//         vector<vector<int>> dp(n+1,vector<int>(m+1,-1));
//         for(int i=0;i<=n;i++){
//             dp[i][0]=0;
//         }
//         for(int i=0;i<=m;i++){
//             dp[0][i]=0;
//         }
//         for(int i = 1;i<=n;i++){
//             for(int j=1;j<=m;j++){
//                 if(text1[i-1] == text2[j-1]) dp[i][j] = 1+dp[i-1][j-1];
//                 else dp[i][j] = max(dp[i-1][j],dp[i][j-1]);
//             }
//         }
//         return dp[n][m];
//     }
// };
//Time Complexity: O(N*M)
//Reason: There are two nested loops
//Space Complexity: O(N*M)
//Reason: We are using an external array of size ‘N*M)’. Stack Space is eliminated.

    int longestCommonSubsequence(string text1, string text2){
        int n=text1.size(), m=text2.size();
        vector<int> prev(m+1,0), cur(m+1,0);
        for(int i=1;i<=n;i++){
            for(int j=1;j<=m;j++){
                if(text1[i-1] == text2[j-1]) cur[j] = 1 + prev[j-1];
                else cur[j] = max(prev[j],cur[j-1]);
            }
            prev=cur;
        }
        return prev[m];
    }
};
```
Time Complexity: O(N*M)
 - Reason: There are two nested loops.
Space Complexity: O(M)
 - Reason: external array of size ‘M+1’ to store only two rows.
