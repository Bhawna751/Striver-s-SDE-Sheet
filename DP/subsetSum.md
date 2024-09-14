## [416. Partition Equal Subset Sum](https://leetcode.com/problems/partition-equal-subset-sum/description/)
Given an integer array `nums`, return `true` if you can partition the array into two subsets such that the sum of the elements in both subsets is equal or `false` otherwise.

Example 1:
```
Input: nums = [1,5,11,5]
Output: true
```
Explanation: The array can be partitioned as [1, 5, 5] and [11].

Example 2:
```
Input: nums = [1,2,3,5]
Output: false
```

**Solution:**
<details>
  <summary>RECURSIVE</summary>
  <br>

  ```cpp
class Solution {
public:
    bool solve(vector<int> &nums, int k, int i){
        if(k==0)return true;
        if(i==0)return nums[i] == k;
        bool notpick = solve(nums,k,i-1);
        bool pick = 0;
        if(nums[i] <= k) pick = solve(nums,k-nums[i],i-1);
        return notpick || pick;
    }
    bool canPartition(vector<int>& nums) {
        int n = nums.size();
        int total=0;
        for(int i=0;i<n;i++){
            total += nums[i];
        }
        if(total%2!=0)return false;
        else{
            int k = total/2;
            return solve(nums,k,n-1);
        }
    }
};
```
  
</details>
<details>
  <summary>MEMOIZATION</summary>
  <br>

  ```cpp
class Solution {
public:
    bool solve(vector<int> &nums, int k, int i,vector<vector<int>> &dp){
        if(k==0)return true;
        if(i==0)return nums[i] == k;
        if(dp[i][k] !=-1) return dp[i][k];
        bool notpick = solve(nums,k,i-1,dp);
        bool pick = 0;
        if(nums[i] <= k) pick = solve(nums,k-nums[i],i-1,dp);
        return dp[i][k]= notpick || pick;
    }
    bool canPartition(vector<int>& nums) {
        int n = nums.size();
        
        int total=0;
        for(int i=0;i<n;i++){
            total += nums[i];
        }
        if(total%2!=0)return false;
        else{
            int k = total/2;
            vector<vector<int>> dp(n,vector<int>(k+1,-1));
            return solve(nums,k,n-1,dp);
        }
    }
};
```
Time Complexity: O(N*target), where target is the total sum of elements of the array divided by 2.

Space Complexity:O(N*target) + O(N)

</details>
<details>
  <summary>TABULATION</summary>
  <br>

  ```cpp
class Solution {
public:
    
    bool canPartition(vector<int>& nums) {
        int n = nums.size();
        
        int total=0;
        for(int i=0;i<n;i++){
            total += nums[i];
        }
        if(total%2!=0)return false;
        else{
            int k = total/2;
            vector<vector<bool>> dp(n,vector<bool>(k+1,false));
            for(int i=0;i<n;i++) dp[i][0]=true;
            if(nums[0] <= k)dp[0][nums[0]] = true;
            for(int i=1;i<n;i++){
                for(int j=1;j<=k;j++){
                    bool notpick = dp[i-1][j];
                    bool pick = false;
                    if(nums[i] <= j) pick = dp[i-1][j-nums[i]];
                    dp[i][j] = notpick || pick;
                }
            }
            return dp[n-1][k];
        }
    }
};
```
Time Complexity: O(N*target), where target is the total sum of elements of the array divided by 2.

Space Complexity:O(N*target) 

</details>
<details>
  <summary>SPACE OPTIMIZATION</summary>
  <br>

  ```cpp
class Solution {
public:
    
    bool canPartition(vector<int>& nums) {
        int n = nums.size();
        
        int total=0;
        for(int i=0;i<n;i++){
            total += nums[i];
        }
        if(total%2!=0)return false;
        else{
            int k = total/2;
            vector<bool> prev(k+1,false);
            prev[0]=true;
            if(nums[0] <= k) prev[nums[0]] = true;
            for(int i=1;i<n;i++){
                vector<bool> cur(k+1, false);
                for(int j=1;j<=k;j++){
                    bool notpick = prev[j];
                    bool pick = false;
                    if(nums[i] <= j) pick = prev[j-nums[i]];
                    cur[j] = notpick || pick;
                }
                prev=cur;
            }
            return prev[k];
        }
    }
};
```
Time Complexity: O(N*target), where target is the total sum of elements of the array divided by 2.

Space Complexity:O(target) 

</details>
