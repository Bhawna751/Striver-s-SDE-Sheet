## [518. Coin Change II](https://leetcode.com/problems/coin-change-ii/)

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
  
 **Approach :**
- array of size [n][target+1], initialize it as 0.
- Base Cases: for `'ind'` == `0`, if `T % arr[0] == 0`, initialize the dp array to `1` else initialize it to `0`.
- Iterative Computation Using Loops: first row (`ind = 0`) in the base case, so `ind` variable will move from `1` to `n-1`, whereas `target` variable will move from `0` to `T`(target). Initialize two nested for loops to traverse the dp array ,set the value of each cell in the 2D dp array. Instead of recursive calls, use the dp array itself to find the values of intermediate calculations.
- Returning the answer: At last dp[n-1][target] will hold the solution after the completion of whole process, as we are doing the calculations in bottom-up manner.

```cpp
class Solution {
public:
    int change(int amount, vector<int>& coins) {
        int n = coins.size();
        vector<vector<int>> dp(n,vector<int>(amount+1,0));

        for(int i=0;i<=amount;i++){
            if(i % coins[0] == 0) dp[0][i] = 1;
        }

        for(int i = 1; i<n;i++){
            for(int j  = 0;j<=amount;j++){
                int notpick = dp[i-1][j];
                int pick = 0;
                if(coins[i] <= amount) pick = dp[i][j - coins[i]];
                dp[i][j] = pick + notpick;
            }
        }
        return dp[n-1][amount];
    }
};
```
 
</details>
<details>
  <summary>SPACE OPTIMIZATION</summary>
  <br>
 
 **Approach**
-  two arrays `prev` and `cur`. Initialize the `prev` array for the **first element** of the array.
- Fill the `cur` array for present row using nested loops and the same logic discussed in tabulation. If the current element is less than or equal to the target, calculate `take`.
- store the sum of `take` and `not take` in the `cur` array.
- Update `prev` with `cur`, get the minimum number of coins needed for the target sum stored in `prev[Target]`.
```cpp
class Solution {
public:
    int change(int amount, vector<int>& coins) {
        int n = coins.size();
        vector<int> prev(amount+1,0);

        for(int i=0 ; i<=amount ; i++){
            if(i % coins[0] == 0) prev[i] = 1;
        }

        for(int i = 1; i<n;i++){
            vector<int> cur(amount+1,0);
            for(int j  = 0;j<=amount;j++){
                int notpick = prev[j];
                int pick = 0;
                if(coins[i] <= amount) pick = cur[j - coins[i]];
                cur[j] = pick + notpick;
            }
            prev=cur;
        }
        return prev[amount];
    }
}; 
```
</details>
