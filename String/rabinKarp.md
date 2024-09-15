## [686. Repeated String Match](https://leetcode.com/problems/repeated-string-match/description/)
Given two strings `a` and `b`, return the minimum number of times you should repeat string `a` so that string `b` is a substring of it. If it is impossible for `b`​​​​​​ to be a substring of `a` after repeating it, return `-1`.

Notice: string `"abc"` repeated `0` times is `""`, repeated `1` time is `"abc"` and repeated `2` times is `"abcabc"`.

Example 1:
```
Input: a = "abcd", b = "cdabcdab"
Output: 3
```
Explanation: We return 3 because by repeating a three times "abcdabcdabcd", b is a substring of it.

Example 2:
```
Input: a = "a", b = "aa"
Output: 2
```
<details>
  <summary>Using NPOS</summary>
  <br>

```cpp
class Solution {
public:
    int repeatedStringMatch(string a, string b) {
        string ans = "";
        int cnt=0;
        while(ans.size() < b.size()){
            ans += a;
            cnt++;
        }
        if(ans.find(b) != string::npos) return cnt;
        ans+=a;
        cnt++;
        if(ans.find(b) != string::npos) return cnt;
        return -1;
    }
};
```
</details>
<details>
  <summary> Rabin Karp</summary>
  
**Intuition For Rabin Karp:**
The hash value is calculated using a rolling hash function, which allows you to update the hash value for a new substring by efficiently removing the contribution of the old character and adding the 
contribution of the new character. This makes it possible to slide the pattern over the text and calculate the hash value for each substring without recalculating the entire hash from scratch.

**Algorithm for Rabin Karp:**
- Initially calculate the hash value of the pattern.
- Start iterating from the starting of the string:
    - Calculate the hash value of the current substring having length `m`.
    - If the hash value of the current substring and the pattern are same check if the substring is same as the pattern.
    - If they are same, store the starting index as a valid answer. Otherwise, continue for the next substrings.
- Return the starting indices as the required answer.
  
