## 518. Coin Change II

You are given an integer array `coins` representing coins of different denominations and an integer `amount` representing a total amount of money.

Return the number of combinations that make up that amount. If that amount of money cannot be made up by any combination of the coins, return `0`.

You may assume that you have an *infinite number* of each kind of coin.

The answer is guaranteed to fit into a **signed 32-bit integer**.

 

Example 1:
```
Input: amount = 5, coins = [1,2,5]
Output: 4
```
Explanation: there are four ways to make up the amount:
- 5=5
- 5=2+2+1
- 5=2+1+1+1
- 5=1+1+1+1+1

<details>
  <summary>MEMOIZATION</summary>
  <br>
  
**Approach:**
- Declare a dp array of size `[n][target+1]`: As there are two changing parameters in the recursive solution, `'ind'` and `'target'`. The maximum value `'ind'` can attain is `(n)`, where n is the size of array and for `'target'` only values between `0` to `target`. 
- The dp array stores the **calculations of subproblems**. Initialize dp array with -1, to indicate that no subproblem has been solved yet.

While encountering an overlapping subproblem: When we come across a subproblem, for which the dp array has value other than -1, it means we have found a subproblem which has been solved before hence it is an overlapping subproblem. No need to calculate it's value again just retrieve the value from dp array and return it.
Store the value of subproblem: Whenever, a subproblem is enocountered and it is not solved yet(the value at this index will be -1 in the dp array), store the calculated value of subproblem in the array.
```cpp
  class Solution {
public:
    int solve(int amount, vector<int>& coins, int i,vector<vector<int>> &dp){
        if(i==0) return (amount % coins[i] == 0);
        if(dp[i][amount]!=-1)return dp[i][amount];
        int notpick = solve(amount,coins,i-1,dp);
        int pick = 0;
        if(coins[i]<= amount)pick= solve(amount - coins[i], coins, i,dp);
        return dp[i][amount] = pick + notpick;
    }
    int change(int amount, vector<int>& coins) {
        int n = coins.size();
        vector<vector<int>> dp(n,vector<int>(amount+1,-1));
        return solve(amount,coins,n-1,dp);
    }
};
```

Time Complexity:O(N*Target)

Space Complexity: O(N*Target)

</details>
<details>
  <summary>TABULATION</summary>
  <br>
  
</details>
<details>
  <summary>SPACE OPTIMIZATION</summary>
  <br>
  
</details>
