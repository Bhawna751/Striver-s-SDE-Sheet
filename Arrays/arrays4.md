<details>
  <summary>Two Sum</summary>

  [Link](https://leetcode.com/problems/two-sum/description/)

  Brute:
  ------
  - use nested loop

Better:
-----
- use a hashmap
- check if for each element, target-nums[i] element exists in map or not

<details>
  <summary>Code:</summary>

  ```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        int n=nums.size();
        
        unordered_map<int,int> mpp;
        for(int i=0;i<n;i++){
            if(mpp.find(target-nums[i])!= mpp.end()){
                return {mpp[target-nums[i]] , i};
            }
            mpp[nums[i]] = i;
        }
        return {-1,-1};
    }
};
```
</details>

Optimal:
------
- sort and use two pointers, l=0, r=n-1;
- and decrement/increment the pointers according to their sums

<details>
  <summary>Code</summary>

  ```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        int n=nums.size();
        int l=0, r=n-1;

        vector<int>ans;
        vector<vector<int>> index;
        for(int i=0;i<n;i++)index.push_back({nums[i],i});

        sort(index.begin(), index.end(), [](const vector<int>& a, const vector<int>&b){
            return a[0] < b[0];
        });

        while(l<r){
            int sum = index[l][0] + index[r][0];
            if(sum == target){
                ans.push_back(index[l][1]);
                ans.push_back(index[r][1]);
                return ans;
            }else if(sum < target) l++;
            else r--;
        }
        return {-1,-1};
    }
};
```
Time complexity: O(N) + O(n*log n )
</details>
</details>
