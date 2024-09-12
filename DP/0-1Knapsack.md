## 0 1 Knapsack

A thief is robbing a store and can carry a maximum weight of `W` into his knapsack. There are `N` items available in the store and the weight and value of each item is known to the thief. 
Considering the constraints of the maximum weight that a knapsack can carry, you have to find the maximum profit that a thief can generate by stealing items.

Note: The thief is not allowed to break the items.

For example, `N = 4`, `W = 10` and `weights` = [6, 1, 5, 3] and `values` = [3, 6, 1, 4]. Then the best way to fill the knapsack is to choose items with weight 6, 1 and 3. 
The total value of knapsack = 3 + 6 + 4 = 13.

Solution:
```cpp
//Memoization:
int knapsackUtil(vector<int>& wt, vector<int>& val, int ind, int W, vector<vector<int>>& dp) {
    // Base case: If there are no items left or the knapsack has no capacity, return 0
    if (ind == 0 || W == 0) {
        return 0;
    }
    // If the result for this state is already calculated, return it
    if (dp[ind][W] != -1) {
        return dp[ind][W];
    }
    // Calculate the maximum value by either excluding the current item or including it
    int notTaken = knapsackUtil(wt, val, ind - 1, W, dp);
    int taken = 0;
    // Check if the current item can be included without exceeding the knapsack's capacity
    if (wt[ind] <= W) {
        taken = val[ind] + knapsackUtil(wt, val, ind - 1, W - wt[ind], dp);
    }
    // Store the result in the DP table and return
    return dp[ind][W] = max(notTaken, taken);
}

// Function to solve the 0/1 Knapsack problem
int knapsack(vector<int>& wt, vector<int>& val, int n, int W) {
    vector<vector<int>> dp(n, vector<int>(W + 1, -1));
    return knapsackUtil(wt, val, n - 1, W, dp);
}

//Time Complexity: O(N*W)
//Reason: There are N*W states therefore at max ‘N*W’ new problems will be solved.
//Space Complexity: O(N*W) + O(N)
//Reason: We are using a recursion stack space(O(N)) and a 2D array ( O(N*W))


//TABULATION:
int maxProfit(vector<int> &values, vector<int> &weights, int n, int w)
{
	// Write your code here
	vector<vector<int>> dp(n,vector<int>(w+1,0));
	for(int i=weights[0];i<=w;i++){
		dp[0][i] = values[0];
	}
	for(int i=1;i<n;i++){
		for(int j=0;j<=w;j++){
			int notpick = dp[i-1][j];
			int pick = -1e9;
			if(weights[i]<=j) pick = dp[i-1][j-weights[i]] + values[i];
			dp[i][j] = max(pick,notpick);
		}
	}
	return dp[n-1][w];
}

//Time Complexity: O(N*W)
//Reason: There are two nested loops
//Space Complexity: O(N*W)

//Sapce optimization:
int maxProfit(vector<int> &values, vector<int> &weights, int n, int w)
{
	vector<int> prev(w+1,0);//
	for(int i=weights[0];i<=w;i++){
		prev[i] = values[0];//
	}
	for(int i=1;i<n;i++){
		for(int j = w;j>=0;j--){
			int notpick = prev[j];
			int pick = -1e9;
			if(weights[i] <= w)pick = values[i] + prev[j-weights[i]];
			prev[j]= max(pick,notpick);
		}
	}
	return prev[w];
}

//Time Complexity: O(N*W)
//Reason: There are two nested loops.
//Space Complexity: O(W)
//Reason: We are using an external array of size ‘W+1’ to store only one row.
```
