## [242. Valid Anagram](https://leetcode.com/problems/valid-anagram/description/)
Given two strings `s` and `t`, return `true` if `t` is an anagram of `s`, and `false` otherwise.

Example 1:
```
Input: s = "anagram", t = "nagaram"
Output: true
```
Example 2:
```
Input: s = "rat", t = "car"
Output: false
```
**Solutions:**
<details>
  <summary>Brute Force</summary>
  <br>
  
```cpp
class Solution {
public:
    bool isAnagram(string s, string t) {
        sort(s.begin(), s.end());
        sort(t.begin(), t.end());
        return s==t;
    }
};
```
Time Complexity: O(N log N)

Space Complexity: O(1)
</details>
<details>
  <summary>Hash Table</summary>
  <br>

- Create an unordered map `freq` to store the character frequencies. 
- Iterate over each character `it` in string `s`, increment its frequency in the freq map by using the `freq[it]++` expression.
- Iterate over each character `it` in string `t`, decrement its frequency in the freq map by using the `freq[it]--` expression.
- iterate over each pair `it` in the `freq` map. Check if any frequency (it.second) is non-zero. If any frequency is non-zero, it means there is a character that appears more times in one string than the other, indicating that the strings are not anagrams. In that case, return false.
- If all frequencies in the count map are zero, it means the strings s and t have the same characters in the same frequencies, making them anagrams. In this case, the function returns true.
```cpp
class Solution {
public:
    bool isAnagram(string s, string t) {
        unordered_map<char, int> freq;
        for (char it : s) {
            freq[it]++;
        }
        for(char it: t){
            freq[it]--;
        }
        for(auto it: freq){
            int cnt = it.second;
            if(cnt!=0) return false;
        }
        return true;
    }
};
```
Time Complexity: O(3N)

Space Complexity: O(N)
</details>
