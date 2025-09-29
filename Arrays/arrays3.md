<details>
  <summary>Search in a 2D matrix</summary>

  [Link](https://leetcode.com/problems/search-a-2d-matrix/description/)

  Brute:
  -----
  - traverse each cell using nested loops
  - check if the element at current cell is equal to the ‘target’. If yes, return `true`. Otherwise, after completing the traversal, return `false` as it means no matching element is found in the matrix.

Better:
-----
- traverse each row of the matrix using a for loop.
- for every row, check if it contains the target. if(mat[i][0] <= target && mat[i][m-1] >= target) return bs(mat[i], target)
- in bs(), initialize low = 0 and high = m-1
- While (low <= high) mid = (low+high)/2. check if the element at mid is equal to target, if so, return true.
- if(mat[mid] > target) high = mid-1,else low = mid+1

<details>
  <summary>Code:</summary>

  ```cpp
class Solution {
public:
    bool bs(vector<int>&mat, int target){
        int low = 0, high= mat.size();
        while(low<=high){
            int mid=(low+high)/2;
            if(mat[mid]==target)return true;
            else if(mat[mid] > target) high = mid-1;
            else low = mid+1;
        }
        return false;
    }
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int n = matrix.size(), m = matrix[0].size();
        for(int i=0;i<n;i++){
           if(matrix[i][0] <= target && matrix[i][m-1] >= target) 
           return bs(matrix[i], target);
        }
        return false;
    }
};
```
Time Complexity: O(N + log M)
</details>


Optimal:
-----
- flatten the 2d array into 1d array and apply binary search

<details>
  <summary>Code:</summary>

```cpp
class Solution {
public:
    
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int n = matrix.size(), m = matrix[0].size();
        int l=0, r=n*m-1;
        while(l<=r){
            int mid=(l+r)/2;
            int row = mid/m;
            int col = mid%m;
            if(matrix[row][col]==target)return true;
            else if(matrix[row][col] > target) r = mid-1;
            else l = mid+1;
        }
        return false;
    }
};
```
Time Complexity: O(Log (N*M))
</details>
</details>


<details>
  <summary>Implement Pow(X,N)</summary>

  [Link](https://leetcode.com/problems/powx-n/)

  Brute:
  -----
- ans =1, Check if (n<0) x = 1/x and make n positive by setting n to -n. 
- Use a loop to iterate from 0 to n , multiply ans by x.

<details>
  <summary>Code:</summary>

  ```cpp

class Solution {
public:
    double myPow(double x, int n) {
        double ans=1;
        if(n<0) {
            x = 1/x;
            n = -n;
        }
        for(int i=0;i<n;i++){
            ans *= x;

        }
        return ans;
    }
};
```
Time Complexity: O(N)
</details>


Optimal:
-----
- recursive function:
   - Base case: If (n==0) return 1
   - Base case: If (n==1) return x
   - if(n%2==0) pow(x*x, n/2);
   - return x* pow(x,n-1);

<details>
  <summary>Code:</summary>

```cpp
class Solution {
public:
    double power(double x, long long n){
        if(n==0)return 1.0;
        if(n==1)return x;
        if(n%2==0) return power(x*x, n/2);
        return x*power(x, n-1);
    }
    double myPow(double x, int n) {
        long long num=n;
        if(num<0){
            return (1.0/power(x,-num));
        }
        return power(x,num);
    }
};
```
Time Complexity: O(Log N)
</details>
</details>


<details>
  <summary>Majority Element</summary>

  [Link](https://leetcode.com/problems/majority-element/)

  Brute:
  -----
- Iterate over each element in the array one by one.
- for each element, run another loop and count its occurrence in the given array.
- If any element occurs more than the floor of (N/2), simply return it.
<details>
  <summary>Code:</summary>

```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int n=nums.size();
        for(int i=0;i<n;i++){
            int cnt =0;
            for(int j=0;j<n;j++){
                if(nums[i]==nums[j])cnt++;
            }
            if(cnt > n/2)return nums[i];
        }
        return -1;
    }
};
```
</details>

Better:
-----
- use a hashmap
<details>
  <summary>Code:</summary>

```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int n=nums.size();
        unordered_map<int,int>mpp;
        for(int i=0;i<n;i++){
            mpp[nums[i]]++;
        }
        for(auto it:mpp){
            if(it.second > n/2)return it.first;
        }
        return -1;
    }
};
```
</details>
Time Complexity: O(N)

Optimal:
-----
- `cnt` for tracking the count of elements and `ele` for keeping a track of the element we are counting.
- Traverse through the given array. If (cnt==0) then ele=nums[i] .
- If (nums[i]==ele)cnt++, else cnt--
- return ele
<details>
  <summary>Code:</summary>

```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int n=nums.size();
        int cnt=0, ele;
        for(int i=0;i<n;i++){
            if(cnt==0){
                ele=nums[i];
                cnt=1;
            }
            else if(nums[i]==ele){
                cnt++;
            }
            else cnt--;

        }
        
        return ele;
    }
};
```
Time Complexity:O(N)
</details>
</details>


<details>
  <summary>Majority Element II</summary>

  [Link](https://leetcode.com/problems/majority-element-ii/description/)

  Brute:
  -----
- Iterate over the array, for each unique element, run another loop and count its occurrence in the given array. If any element occurs more than the floor of (N/3), include it in our answer.
- While traversing if any element that is already included in our answer is found, just skip it.
- When the answer array size is already 2, break out of loop, as there cant be more than 2 elements.
<details>
  <summary>Code:</summary>
  
```cpp
class Solution {
public:
    vector<int> majorityElement(vector<int>& nums) {
        vector<int>ans;
        int n=nums.size();
        for(int i=0;i<n;i++){
            if(ans.size()==0 || nums[i]!=ans[0]){
                int cnt=0;
                for(int j=0;j<n;j++){
                    if(nums[j]==nums[i])cnt++;
                }if(cnt > n/3) ans.push_back(nums[i]);
            }
            if(ans.size()==2)break;
        }
        return ans;
    }
};
```
</details>

Better:
-----
- same logic as above but use a frequency hashmap

<details>
  <summary>Code:</summary>

```cpp
class Solution {
public:
    vector<int> majorityElement(vector<int>& nums) {
        vector<int>ans;
        int n=nums.size();
        unordered_map<int,int>mpp;
        for(int i=0;i<n;i++) {
            mpp[nums[i]]++;
            if(mpp[nums[i]] == n/3+1) ans.push_back(nums[i]);
            if(ans.size()==2)break;
        }
        
        return ans;
    }
};
```
Time Complexity: O(N * logN)
</details>

Optimal:
-----
- `cnt1` & `cnt2` for tracking the counts of elements and `el1` & `el2` for storing the majority of elements.
- Traverse through the given array. If (cnt1 == 0 && nums[i] != ele2) ele1 = nums[i] , cnt1++;
- If (cnt2 == 0 && nums[i]!=ele1) ele2=nums[i]. cnt2++;
- If (nums[i]==ele1)cnt1++, if(nums[i]==ele2)cnt2++;
- else cnt1-- cnt2-- 
<details>
  <summary>Code:</summary>

```cpp
class Solution {
public:
    vector<int> majorityElement(vector<int>& nums) {
        int cnt1=0, cnt2=0, ele1=-1e9, ele2=-1e9;
        int n=nums.size();
        
        for(int i=0;i<n;i++) {
            if(nums[i]!=ele1 && cnt2 ==0){
                ele2=nums[i];
                cnt2=1;
            }else if(nums[i]!=ele2 && cnt1==0){
                ele1=nums[i];
                cnt1=1;
            }
            else if(nums[i]==ele1) cnt1++;
            else if(nums[i]==ele2) cnt2++;
            else{
                cnt1--;
                cnt2--;
            }
        }
        vector<int>ans;
        cnt1=0, cnt2=0;
        for(int i=0;i<n;i++){
            if(nums[i] == ele1)cnt1++;
            else if(nums[i]==ele2)cnt2++;
        }
        if(cnt1>=n/3+1)ans.push_back(ele1);
        if(cnt2>=n/3+1)ans.push_back(ele2);
        return ans;
    }
};
```
Time Complexity: O(N)
</details>
</details>


<details>
  <summary>Unique Paths</summary>

  Recursive:
  -----
  - try all possible ways

```cpp
class Solution {
public:
    int helper(int i, int j){
        if(i==0 && j==0)return 1;
        if(i<0 || j<0)return 0;
        int up = helper(i-1, j);
        int left = helper(i, j-1);
        return up+left;
    }
    int uniquePaths(int m, int n) {
        return helper(m-1,n-1);
    }
};
```
Memoization:
-----
- declare a dp (m,n), dp[i][j] represents no.of ways to reach 0,0 from i,j cell.
- if(dp[i][j]!=-1) return dp[i][j]
- else store the value of the subproblem
  <details>
    <summary>Code:</summary>

```cpp
    class Solution {
public:
    int solve(int i, int j, vector<vector<int>>&dp){
        if(i==0 && j==0)return 1;
        if(i<0 || j<0)return 0;
        if(dp[i][j]!=-1)return dp[i][j];
        int up = solve(i-1, j,dp);
        int left = solve(i, j-1,dp);
        return dp[i][j] = up+left;
    }
    int uniquePaths(int m, int n) {
        vector<vector<int>> dp(m, vector<int>(n,-1));
        return solve(m-1,n-1,dp);
    }
};
```
</details>

Tabulation:
------
- decalre a dp(m,n) and if(i==0 && j==0) dp[0][0] = 1; continue
- if(i>0) up = dp[i-1][j], if(j>0) left = dp[i][j-1]
- return dp[m-1][n-1]

<details>
  <summary>Code:</summary>

```cpp
class Solution {
public:
    int solve(int m, int n, vector<vector<int>>&dp){
        
        for(int i  = 0;i<m;i++){
            for(int j=0;j<n;j++){
                if(i==0 && j==0){
                    dp[i][j]=1;
                    continue;
                }
                int up = 0, left =0;
                if(i>0)up = dp[i-1][j];
                if(j>0) left = dp[i][j-1];
                dp[i][j] = up+left;
            }
        }
        return dp[m-1][n-1];

    }
    int uniquePaths(int m, int n) {
        vector<vector<int>> dp(m, vector<int>(n,-1));
        
        return solve(m,n,dp);
    }
};
```
</details>

Space Optimization:
-----
```cpp
class Solution {
public:
    
    int uniquePaths(int m, int n) {
        vector<int>prev(n,0);
        for(int i  = 0;i<m;i++){
            vector<int>cur(n,0);
            for(int j=0;j<n;j++){
                if(i==0 && j==0){
                    cur[j]=1;
                    continue;
                }
                int up = 0, left =0;
                if(i>0)up = prev[j];
                if(j>0) left = cur[j-1];
                cur[j] = up+left;
            }
            prev = cur;
        }
        return prev[n-1];
    }
};
```
</details>
</details>



<details>
  <summary>Reverse Pairs</summary>

  [Link](https://leetcode.com/problems/reverse-pairs/)

  Brute:
  -----
  - traverse the array, i = 0 to n, and j = i+1 to n
  - if(arr[i] > 2*arr[j])cnt++

<details>
  <summary>Code:</summary>

```cpp
class Solution {
public:
    int reversePairs(vector<int>& nums) {
        int n=nums.size();
        int ans=0;
        for(int i=0;i<n;i++){
            for(int j=i+1;j<n;j++){
                if(nums[i] > 2*nums[j]) ans++;
            }
        }
        return ans;
    }
};
```
</details>

Optimal:
-----
- use modified mergeSort

```cpp
class Solution {
public:
    int mergeSort(vector<int>&nums, int l, int r){
        if(l>=r)return 0;
        int mid = (l+r)/2;
        int cnt=0;
        cnt += mergeSort(nums,l,mid);
        cnt += mergeSort(nums,mid+1,r);
        cnt += countPairs(nums,l,mid,r);
        merge(nums,l,mid,r);
        return cnt;
    }
    void merge(vector<int>&nums, int l, int mid, int r){
        vector<int>temp;
        int left = l, right = mid+1;
        while(left <= mid && right <=r){
            if(nums[left]<=nums[right])temp.push_back(nums[left++]);
            else temp.push_back(nums[right++]);
        }
        while(left<=mid)temp.push_back(nums[left++]);
        while(right<=r)temp.push_back(nums[right++]);
        for(int i=l;i<=r;i++) nums[i]=temp[i-l];
    }
    int reversePairs(vector<int>& nums) {
        return mergeSort(nums,0,nums.size()-1);
    }
    int countPairs(vector<int>&nums, int low, int mid, int high){
        int r = mid+1;
        int cnt=0;
        for(int i=low;i<=mid;i++){
            while(r <= high && (long long)nums[i] > 2LL * nums[r]){
                r++;
            }
            cnt += (r-(mid+1));
        }
        return cnt;
    }
};
```
</details>
