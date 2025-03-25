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
</details>
