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




<details>
  <summary>4Sum</summary>

  [Link](https://leetcode.com/problems/4sum/description/)

  Brute:
  ------
  - use 4 nested loops

Better:
-----
- 1st loop (0 to n-1), 2nd loop (i+1 to n-1), 3rd loop (j+1 to n-1) , calculate 4th element =target - (arr[i] + arr[j] + arr[k])
- use a hashset, check if 4th element exists in the hashset
- if it exists, sort the four elements, and store it in set
- insert nums[k] in the hashset

<details>
  <summary>Code:</summary>

  ```cpp
class Solution {
public:
    vector<vector<int>> fourSum(vector<int>& nums, int target) {
        int n = nums.size();
        set<vector<int>> st;

        for(int i=0;i<n;i++){
            for(int j=i+1;j<n;j++){
                set<long long>hashset;
                for(int k=j+1;k<n;k++){
                    long long sum = (long long)nums[i]+nums[j]+nums[k];
                    long long fourth = (long long)target - sum;
                    if(hashset.find(fourth)!= hashset.end()){
                        vector<int>temp = {nums[i], nums[j], nums[k], static_cast<int>(fourth)};
                        sort(temp.begin(), temp.end());
                        st.insert(temp);
                    }
                    hashset.insert(nums[k]);
                }
            }
        }
        vector<vector<int>> ans(st.begin(), st.end());
        return ans;
    }
};
```
</details>
Time Complexity: O(N^3 Log(M))

Optimal:
------
- sort and use 4 pointers, i = 0 to n, j = i+1 to n, k = j+1, l=n-1
- skip duplicate vales

<details>
  <summary>Code</summary>

  ```cpp
class Solution {
public:
    vector<vector<int>> fourSum(vector<int>& nums, int target) {
        int n = nums.size();
        sort(nums.begin(), nums.end());
        vector<vector<int>> ans;

        for(int i=0;i<n;i++){
            if(i>0 && nums[i] == nums[i-1] )continue;
            for(int j=i+1;j<n;j++){
                if(j>i+1 && nums[j] == nums[j-1] )continue;
                int k = j+1;
                int l = n-1;
                while(k<l){
                    long long sum =(long long) nums[i] + nums[j] + nums[k] + nums[l];
                    if(target == sum){
                        vector<int> temp = {nums[i], nums[j], nums[k], nums[l]};
                        ans.push_back(temp);
                        k++;
                        l--;
                        while(k<l && nums[k] == nums[k-1])k++;
                        while(k<l && nums[l]==nums[l+1])l--;
                    }
                    else if(sum<target)k++;
                    else l--;
                }
            }
        }
    
        return ans;
    }
};
```
Time complexity: O(N^3)
</details>
</details>
