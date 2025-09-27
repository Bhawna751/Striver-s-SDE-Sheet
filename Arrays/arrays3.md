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
