## [Egg Dropping Puzzle](https://www.geeksforgeeks.org/problems/egg-dropping-puzzle-1587115620/1)

You are given `N` identical eggs and you have access to a `K-floored` building from `1` to `K`.

There exists a floor `f` where `0 <= f <= K` such that any egg dropped from a floor **higher** than f **will break**, and any egg dropped from or **below** floor f will **not break**.

There are few rules given below:
- An egg that survives a fall can be used again.
- A broken egg must be discarded.
- The effect of a fall is the same for all eggs.
- If the egg doesn't break at a certain floor, it will not break at any floor below.
- If the eggs breaks at a certain floor, it will break at any floor above.
- Return the minimum number of moves that you need to determine with certainty what the value of f is.

Example 1:
```
Input:
N = 1, K = 2
Output: 2
```
Explanation: 
1. Drop the egg from floor 1. If it 
   breaks, we know that f = 0.
2. Otherwise, drop the egg from floor 2.
   If it breaks, we know that f = 1.
3. If it does not break, then we know f = 2.
4. Hence, we need at minimum 2 moves to
   determine with certainty what the value of f is.
   
Example 2:
```
Input:
N = 2, K = 10
Output: 4
```
**Solution :**
<details>
  <summary>RECURSIVE</summary>
  <br>

```cpp
int eggDrop(int n, int k) 
    {
        if(k==0 || k == 1)return k;
        if(n==1) return k;
        
        int moves = 1e9;
        for(int i=1;i<=k;i++){
            int breaks = eggDrop(n-1,i-1);
            int survives = eggDrop(n,k-i);
            int maxi = max(breaks, survives);
            moves = min(maxi + 1,moves);
        }
        return moves;
    }
```
</details>

<details>
  <summary>DP with Binary Search</summary>
  <br>

```cpp
int eggDrop(int n, int k) //n = 2, k=10
    {
       vector<vector<int>> dp(n+1, vector<int> (k+1,0));
       for(int i=1;i<=n;i++){
           dp[i][1] = 1;
           dp[i][0] = 0;
       }
       for(int i = 1;i<=k;i++){
           dp[1][i]=i;
       }
        for(int i=2;i<=n;i++){
            for(int j=2;j<=k;j++){
                int low = 1, high = j, ans = 1e9;
                while(low<=high){
                    int mid= (low+high)/2;
                    int breaks = dp[i-1][mid-1];
                    int survives = dp[i][j-mid];
                    int maxi  = 1 + max(breaks,survives);
                    ans = min(ans,maxi);
                    if(breaks>survives) high = mid-1;
                    else low = mid+1;
                }
                dp[i][j] =ans;
            }
        }
        
        return dp[n][k];
    }

```
Time Complexity: 𝑂(𝑛*𝑘 log k) due to nested loops and the linear search.

Space Complexity: O(n*k), for the DP table.

</details>
