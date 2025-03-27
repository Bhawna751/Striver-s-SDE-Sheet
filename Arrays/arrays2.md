<details>
  <summary>Rotate Image</summary>

  [Link](https://leetcode.com/problems/rotate-image/description/)

  ----
  **Brute:**
  - Take another dummy matrix of n*n, and then take the first row of the matrix and put it in the last column of the dummy matrix,
  - take the second row of the matrix, and put it in the second last column of the matrix and so on.
  
  ----
  **Optimal:**

  - Transpose the matrix. (transposing means changing columns to rows and rows to columns)
  - Reverse each row of the matrix.

  <details>
    <summary>code:</summary>

  ```cpp
          void rotate(vector<vector<int>>& matrix) {
        int n=matrix.size();
        for(int i=0;i<n;i++){
            for(int j=0;j<i;j++){
                swap(matrix[i][j], matrix[j][i]);
            }
        }
        for(int r = 0;r<n;r++){
            reverse(matrix[r].begin(), matrix[r].end());
        }
    }
   ```
Time complexity : O(n*n) + O(n*n)
Space Complexity: O(1)
  </details>
</details>
