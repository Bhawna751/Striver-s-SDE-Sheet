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
