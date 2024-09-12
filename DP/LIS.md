## Longest Increasing Subsequence

Given an integer array nums, return the length of the longest strictly increasing 
subsequence.

Example 1:
```
Input: nums = [10,9,2,5,3,7,101,18]
Output: 4
```
Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4.

Example 2:
```
Input: nums = [0,1,0,3,2,3]
Output: 4
```
Solution (**memoization**)
```cpp
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
        int n = nums.size();
        vector<vector<int>> dp(n,vector<int> (n+1,-1));
        return solve(nums,dp,0,-1);
    }
    int solve(vector<int> &nums, vector<vector<int>> &dp, int i, int prev){
        if( i>= nums.size()) return 0;
        if(dp[i][prev+1]!=-1)return dp[i][prev+1];
        int pick = 0;
        int notpick = solve(nums,dp,i+1, prev);
        if(prev == -1 || nums[i] > nums[prev]) pick = 1+solve(nums,dp,i+1,i);
        return dp[i][prev+1] = max(pick,notpick); 
    }
};
```
Time Complexity : O(N^2)

Space Complexity : O(N^2)

Solution: **Space optimized**
```cpp
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
        int n = nums.size();
        vector<int> dp(n,1);
        int ans = 1;//ans = 2
        for(int i=0;i<n;i++){
            for(int j= 0 ;j<i;j++){
                if(nums[i] > nums[j]){
                    dp[i] = max(dp[i],dp[j] + 1);
                    ans = max(ans,dp[i]);
                }
            }
        }
        return ans;
    }
};
```
Time Complexity : O(N^2)

Space Complexity : O(N)


