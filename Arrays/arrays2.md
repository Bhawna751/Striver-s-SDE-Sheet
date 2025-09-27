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

<details>
  <summary>Find the Repeated Number</summary>

  [Link](https://leetcode.com/problems/find-the-duplicate-number/)

  Brute:
  ----
  - sort the array
  - check if(arr[i+1] == arr[i)

  <details>
    <summary>Code:</summary>

  ```cpp
  class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        int ans;
        for(int i=0;i<nums.size();i++){
            if(nums[i]==nums[i+1]){
                ans = nums[i];
                break;
            }
        }
        return ans;
    }
};
  ```
  </details>
  
  Optimal:
  ----

  - use a frequency array

  <details>
    <summary>code:</summary>

  ```cpp
  class Solution {
    public:
    int findDuplicate(vector<int>& nums) {
        int n=nums.size();
        int ans;
        vector<int>freq(n+1,0);
        for(int it:nums){
            freq[it]++;
        }
        for(int i=0;i<=n;i++){
            if(freq[i]>1){
                ans=i;
                break;
            }
        }
        return ans;
    }
};
   ```
Time complexity : O(n)
Space Complexity: O(n)
  </details>

Optimal 2:
-----
- using tortoise and hare method in linked list
- if a cycle is detected it means a duplicate number is found
- return slow

<details>
  <summary>Code:</summary>

```cpp
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        int slow = nums[0];//slow = 1
        int fast = nums[0];//fast =1
        do{
            slow = nums[slow];//slow = 2
            fast = nums[nums[fast]];//fast = 4

        }while(slow!=fast);
        fast = nums[0];//fast = 1
        while(slow!=fast){
            slow = nums[slow];
            fast = nums[fast];
        }
        return slow;
    }
};
```
</details>

</details>



<details>
  <summary>Find the Repeated & Missing Number</summary>


  Brute:
  ----
  - Iterate in array from 1 to N & for each integer, i, count its occurrence in the given array using linear search.
  - Store those two elements that have the occurrence of 2 and 0. Finally, return the elements.


  <details>
    <summary>Code:</summary>

  ```cpp
  class Solution {
public:
    vector<int> findMissingRepeatingNumbers(vector<int> nums) {
        int n=nums.size();
        int repeating = -1, missing =-1;
        for(int i=1;i<=n;i++){
            int cnt =0;
            for(int j=0;j<n;j++){
                if(nums[j] == i) cnt++;
            }
            if(cnt==2) repeating = i;
            else if(cnt == 0)missing = i;
            if(repeating!=-1 && missing!=-1)break;
        }
        return {repeating,missing};
    }
};
  ```
  </details>
  
  Better:
  ----

  - use a frequency array

  <details>
    <summary>code:</summary>

  ```cpp
  class Solution {
public:
    vector<int> findMissingRepeatingNumbers(vector<int> nums) {
        int n=nums.size();
        vector<int> freq(n+1,0);
        for(int it:nums){
            freq[it]++;
        }
        int repeating=-1, missing=-1;
        for(int i=1;i<=n;i++){
            if(freq[i]==2){
                repeating=i;
            }
            else if(freq[i]==0) missing=i;
            if(repeating!=-1 && missing!=-1)break;
        }
        return {repeating,missing};
    }
};
   ```
Time complexity : O(n)
Space Complexity: O(n)
  </details>

Optimal 2:
-----
- use math, sum of n integers `SN` = (n*(n+1))/2, sum of squares `S2N`= ((n)(n+1)(2n+1))/6
- val1 = `S` - `SN`, val2 = `S2` - `S2N` ---> val2 = val2/val1
- repeating = (val1+val2)/2, missing = repeating - val1

<details>
  <summary>Code:</summary>

```cpp
class Solution {
public:
    vector<int> findMissingRepeatingNumbers(vector<int> nums) {
        long long n = nums.size();
        long long sn = (n*(n+1))/2;
        long long s2n = (n*(n+1)*(2*n+1))/6;
        long long s = 0, s2 = 0;
        for(int i=0;i<n;i++){
            s += nums[i];
            s2 += (long long)nums[i] * (long long)nums[i];
        }
        long long val1 = s-sn;
        long long val2 = s2 - s2n;
        val2 = val2/val1;
        long long x = (val1 + val2)/2;
        long long y = x - val1;
        return {(int)x, (int)y};
    }
};
```
</details>

</details>

