<details>
  <summary>Set Matrix Zeroes</summary>

  [Link](https://leetcode.com/problems/set-matrix-zeroes/description/)

----
  **Brute:**
  
   - visit every cell, for each cell with 0, call setrow() and setcol()
   - set the values in the row and cols as `-1`.
   - now for all the values marked as -1, turn them as 0.

  Time Complexity: O(n*m) * O(n+m) + O(n*m)
  
----
**Better:**
  - intialize two arrays `row` and `col` with -1 values.
  - visit each cell, and for each 0 encountered in `i,j` , set the `row[i]` and `col[j]` as 0.
  - traverse the entire matrix and we will put 0 into all the cells (i, j) for which either row[i] or col[j] is marked as 0.
    <details>
      <summary>code: </summary>

      ```cpp
        class Solution {
          public:
              void setZeroes(vector<vector<int>>& matrix) {
                int n =matrix.size(), m = matrix[0].size();
                vector<int> row(n,-1), col(m,-1);
                for(int i=0;i<n;i++){
                for(int j=0;j<m;j++){
                  if(matrix[i][j] == 0){
                    row[i]=0;
                    col[j]=0;
                  }
                }
              }
        for(int i=0;i<n;i++){
            for(int j=0;j<m;j++){
                if(row[i]==0||col[j]==0){
                    matrix[i][j] = 0;
                }
            }
          }
      }
    };
      ```
    </details>
    Time Complexity: O(n*m) + O(n*m)
    Space Complexity: O(n+m)

    -----
    **Optimal:**

    - traverse each `cell[i][j]` and for each `i` and `j`, mark the cells in first row and col as `0`.
      ```cpp
        for(int i = 0;i<n;i++){
            for(int j=0;j<m;j++){
                if(matrix[i][j] == 0){
                    matrix[i][0] = 0;
                
                    if(j!=0)matrix[0][j]=0;//if j was equal to 0 then it would have tried to set the 0th col as 0 which
                                              //would have already been set as 0
                    else col0 = 0;//for the 0th column
                }
            }
        }
      ```
    - mark the rest of the cells apart from first row and col respectively.
      ```cpp
      for(int i = 1;i<n;i++){
            for(int j=1;j<m;j++){
                if(matrix[i][j] != 0){
                    if(matrix[i][0]==0 || matrix[0][j] == 0) matrix[i][j]=0;
                }
            }
        }
      ```
    - check for the first cell if its 0 or not.
     ```cpp
      if(matrix[0][0] == 0){
            for(int j=0;j<m;j++){
                matrix[0][j] = 0; 
            }
        }
     ```
    - for the 0th col, set vealues in each row as 0.
      ```cpp
        if(col0 == 0){
            for(int i=0;i<n;i++){
                matrix[i][0] = 0;
            }
        }
      ```
      Time Complexity: O(2*(n*m))
      Space Complexity: O(1) 
</details>


<details>
  <summary>Pascal's Triangle</summary>

  [Link](https://leetcode.com/problems/pascals-triangle/)
  
  **Optimal:**

  - solve using nCr
  - create rows for each index till `n`.
  - call generateRows() for each row.
  - in generateRows(), push the first value always as 1
  - from col `1` to `n-1` perform the following operations:
     
      ```cpp
        for(int i=1;i<ind;i++){
            sum *= (ind - i);
            sum /= i;

            row.push_back(sum);
        }
      ```
      Time Complexity: O(n*n)
      Space Complexity: O(1) 
</details>


<details>
  <summary>Next Permutation</summary>

  [Link](https://leetcode.com/problems/next-permutation/)
  
  **Optimal:**

  - find out the breakpoint from the right side (n-2 to 0)
  - the breakpoint will be the first point of decreasing numbers.
    ```cpp
      for(int i=n-2;i>=0;i--){
            if(nums[i+1]>nums[i]){
                breakpoint = i;
                break;
            }
        }
    ```
  - if no breakpoint was found then simply reverse the enitre array and return.
  - start traversing from the right again till breakpoint found and find the next greater element.
  - swap the breakpoint value with the next greater element found.
  - reverse the right half of breakpoint
    ```cpp
      reverse(nums.begin()+breakpoint+1,nums.end());
    ```
      Time Complexity: O(3N)
      Space Complexity: O(1) 
</details>



<details>
  <summary>Maximum Subarray</summary>

  [Link](https://leetcode.com/problems/maximum-subarray/description/)
  
  **Optimal:**

  - traverse the array, and sum all the values respectively.
  - keep track of the maximum sum value
  - if the current sum ever goes belows 0 then reset sum to 0.
    ```cpp
      int maxSubArray(vector<int>& nums) {
        int maxi=-1e9, n=nums.size(),sum=0;
        for(int i=0;i<n;i++){
            sum += nums[i];
            if(sum > maxi) maxi = sum;
            if(sum < 0) sum=0;
        }
        return maxi;
    }
    ```
      Time Complexity: O(N)
      Space Complexity: O(1) 
</details>


<details>
  <summary>Sort Colors</summary>

  [Link](https://leetcode.com/problems/sort-colors/)
  
  **Optimal:**

  - traverse the array, and keep count of all number of 0's, 1's and 2's.
  - assign all the values starting from 0 to 2 to the amount of count observed. 
    ```cpp
      void sortColors(vector<int>& nums) {
        int cnt0=0, cnt1=0, cnt2=0;
        for(int i = 0;i<nums.size();i++){
            if(nums[i] == 0) cnt0++;
            else if(nums[i] == 1) cnt1++;
            else cnt2++;
        }
        //cout<<cnt0<<" "<<cnt1<<" "<<cnt2<<" ";
        for(int i=0 ; i<cnt0 ; i++)nums[i] = 0;
        for(int i=cnt0 ; i<cnt1+cnt0 ; i++)nums[i] = 1;
        for(int i=cnt1+cnt0 ; i<nums.size() ; i++)nums[i] = 2;
    }
    ```
      Time Complexity: O(2N)
      Space Complexity: O(1) 
</details>
