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


<details>
  <summary>Merge Intervals</summary>

  [Link](https://leetcode.com/problems/merge-intervals/description/)

BRUTE :

- Check if the list has zero or one interval; if so, return it as is.
- Set a flag indicating that merging may be possible.
- While merging is possible:
   -  Reset the flag at the start of each pass.
   -  Compare each interval with all subsequent intervals.
   -  If an overlap is detected:
       - Merge the two intervals into one combined interval.
       - Remove the second interval from the list.
       - Mark that a merge happened and restart the scanning process.
- When a complete pass finds no overlaps, return the final list of merged intervals.

 <details>
    <summary>code:</summary>

  ```cpp
          class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        
        int n = intervals.size();
        if(n == 0 || n == 1)return intervals;
        bool flag=true;
        while(flag){
            flag=false;
            for(int i=0;i<intervals.size() && !flag;i++){
                for(int j=i+1;j<intervals.size();j++){
                    int a1 = intervals[i][0];
                    int b1= intervals[i][1];
                    int a2 = intervals[j][0];
                    int b2 = intervals[j][1];
                    if(!(b1 < a2 || b2 < a1)){
                        int newStart = min(a1,a2);
                        int newEnd = max(b1,b2);
                        intervals[i][0] = newStart;
                        intervals[i][1] = newEnd;
                        intervals.erase(intervals.begin()+j);
                        break;
                    }
                }
            }
        }
        return intervals;
    }
};
   ```
Time complexity : O(n*n) 
Space Complexity: O(n*n)

</details>

OPTIMAL:

- Sorting: First, sort the intervals based on the starting time.
- Iterating and Merging: Iterate through the sorted intervals, merging any overlapping intervals.
- Result: After all intervals are processed, the result array will contain the merged intervals.

<details>
  <summary>Code:</summary>

```cpp
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        int n = intervals.size();
        if(n<=1) return intervals;
        vector<vector<int>> ans;
        sort(intervals.begin(), intervals.end());
        ans.push_back(intervals[0]);
        for(int i=1;i<intervals.size();i++){
            if(intervals[i][0]<=ans.back()[1]){
                ans.back()[1] = max(ans.back()[1], intervals[i][1]);
            }else ans.push_back(intervals[i]);
        }
        return ans;
    }
};
```
Time Complexity:O(n log n)
Space Complexity:O(n)
</details>
</details>



<details>
  <summary>Merge Two sorted Arrays</summary>

BRUTE:
-----
- declare a third array and two pointers, l and r, l pointing to first index of arr1 and r pointing to first index of arr2.
- if(arr1[l] < arr2[r] ) arr3.push_back(arr1[l]), l++;
- if(arr2[r] > arr1[l] ) arr3.push_back(arr2[r]), r++;
- then for remaining indexes of nums1 or nums2, push the value in arr3
- copy arr3 to nums1

<details>
    <summary>Code:</summary>

  ```cpp
    class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        vector<int>merged(m+n);
        int l=0, r=0, ind=0;
        while(l<m && r<n){
            if(nums1[l]<=nums2[r]) merged[ind++] = nums1[l++];
            else merged[ind++] = nums2[r++];
        }
        while(l<m) merged[ind++]=nums1[l++];
        while(r<n) merged[ind++] = nums2[r++];
        for(int i=0;i<m+n;i++){
            nums1[i] = merged[i];
        }
    }
};
```
Time Complexity: O(min(N, M)) + O(N logN) + O(M logM)
</details>

OPTIMAL 1:
----
- Start comparing elements from the end of both arrays.
- Pick the larger element and place it at the current last available position in the first array.
- Move the pointer of the array from which the element was taken one step back.
- Repeat this process until all elements from the second array are placed.

<details>
  <summary>Code:</summary>

```cpp
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        int i=m-1, j=n-1;
        int ind = m+n-1;
        while(j>=0){
            if(i>=0 && nums1[i]>=nums2[j]){
                nums1[ind]=nums1[i];
                i--;
                ind--;
            }
            else {
                nums1[ind]=nums2[j];
                j--;
                ind--;
            }
        }
    }
};
```
</details>
Time Complexity: O(N+M)
</details>
