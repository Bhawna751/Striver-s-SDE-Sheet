## [14. Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix/description/)
Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string "".

Example 1:
```
Input: strs = ["flower","flow","flight"]
Output: "fl"
```
Example 2:
````
Input: strs = ["dog","racecar","car"]
Output: ""
````
Explanation: There is no common prefix among the input strings.

**Solution:**
```cpp
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        string ans="";
        sort(strs.begin(), strs.end());
        string start = strs[0], end = strs[strs.size()-1];
        for(int i=0;i< min(start.length(),end.length()) ; i++){
            if(start[i] != end[i])break;
            ans += start[i];
        }
        return ans;
    }
};
```
Time Complexity: O(N * log N)
