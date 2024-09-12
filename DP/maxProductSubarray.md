## [152. Maximum Product Subarray](https://leetcode.com/problems/maximum-product-subarray/description/)

Given an integer array` nums`, find a `subarray` that has the largest product, and return the product.

The test cases are generated so that the answer will fit in a 32-bit integer.

Example 1:
```
Input: nums = [2,3,-2,4]
Output: 6
```
Explanation: [2,3] has the largest product 6.

Example 2:
```
Input: nums = [-2,0,-1]
Output: 0
```
Explanation: The result cannot be 2, because [-2,-1] is not a subarray.

Solution:
```cpp
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        int n = nums.size();
        int mini = 1, maxi = 1;
        int ans = -1e9;
        for (int j = 0; j < n; j++) {
            if(nums[j] < 0){
                swap(maxi,mini);
            }
            maxi = max(maxi*nums[j], nums[j]);
            mini = min(mini*nums[j], nums[j]);
            ans = max(ans, maxi);
        }

        return ans;
    }
};
```
