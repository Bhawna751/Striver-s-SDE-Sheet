## [139. Word Break](https://leetcode.com/problems/word-break/description/)
Given a string `s` and a dictionary of strings `wordDict`, return `true` if s can be segmented into a space-separated sequence of one or more dictionary words.

Note that the same word in the dictionary may be reused multiple times in the segmentation.

Example 1:
```
Input: s = "leetcode", wordDict = ["leet","code"]
Output: true
```
Explanation: Return true because "leetcode" can be segmented as "leet code".

Example 2:
```
Input: s = "applepenapple", wordDict = ["apple","pen"]
Output: true
```
Explanation: Return true because "applepenapple" can be segmented as "apple pen apple".
Note that you are allowed to reuse a dictionary word.

Example 3:
```
Input: s = "catsandog", wordDict = ["cats","dog","sand","and","cat"]
Output: false
```
### Solution:

<details>
  <summary>RECURSIVE</summary>
  <br>

  **Approach :**
  try breaking the string from different points and checks whether each substring is present in the dictionary
```cpp
class Solution {
public:
    bool solve(string s, unordered_set<string> &st, int ind){
        if(ind == s.size()) return true; //successfully segmented
        for(int i= ind+1;i<=s.size();i++){
            if(st.find(s.substr(ind,i-ind)) != st.end() && solve(s,st,i)){
                return true;
            }
        }
        return false;
    }
    bool wordBreak(string s, vector<string>& wordDict) {
        unordered_set<string>st(wordDict.begin(), wordDict.end());//"leet" "code"
        return solve(s, st, 0);
    }
};
```
Time Complexity: O(2^n) in the worst case, since every character can either start or not start a new word.

Space complexity: O(n) 

</details>
<details>
  <summary>MEMOIZATION</summary>
  <br>

  **Approach :**
- store intermediate results in a memoization table to avoid redundant calculations.
```cpp
class Solution {
public:
    bool solve(string s, unordered_set<string> &st, int ind, unordered_map<int,bool> &dp){
        if(ind == s.size()) return true; //successfully segmented
        if(dp.find(ind) != dp.end()) return dp[ind];
        for(int i= ind+1;i<=s.size();i++){
            if(st.find(s.substr(ind,i-ind)) != st.end() && solve(s,st,i,dp)){
                return dp[ind]=true;
            }
        }
        return dp[ind]= false;
    }
    bool wordBreak(string s, vector<string>& wordDict) {
        unordered_set<string>st(wordDict.begin(), wordDict.end());//"leet" "code"
        unordered_map<int,bool>dp;
        return solve(s, st, 0,dp);
    }
};
```
Time Complexity: O(n^2) due to the memoization of overlapping subproblems.

Space complexity: O(n)

</details>
<details>
  <summary>BOTTOM-UP</summary>
  <br>

  **Approach :**
- store intermediate results in a memoization table to avoid redundant calculations.
```cpp
class Solution {
public:
    bool wordBreak(string s, vector<string>& wordDict) {
        unordered_set<string>st(wordDict.begin(), wordDict.end());//"leet" "code"
        vector<bool>dp(s.length()+1,false);
        dp[0]=true; // An empty string can always be segmented
        for(int i=1;i<=s.length();i++){
            for(int j=0;j<i;j++){
                if(dp[j] && st.find(s.substr(j,i-j)) != st.end()){
                    dp[i]=true;
                    break;
                }
            }
        }
        return dp[s.length()];
    }
};
```
Time Complexity: O(n^2) due to the memoization of overlapping subproblems.

Space complexity: O(n)

</details>
