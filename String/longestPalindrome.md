## [5. Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/description/)
Given a string `s`, return the longest palindromic substring in `s`.

Example 1:
```
Input: s = "babad"
Output: "bab"
```
Explanation: "aba" is also a valid answer.

Example 2:
```
Input: s = "cbbd"
Output: "bb"
```
**Solutions:**

<details>
  <summary>Brute Force:</summary>


Algorithm :
- Pick a `starting` index for the `current` substring which is every index from **0 to n-2.**
- Pick the `ending` index for the `current` substring which is every index from **i+1 to n-1.**
- Check if the `substring` from `ith index to jth index` is a palindrome.
- If step 3 is `true` **and** length of substring is greater than maximum length so far, update maximum length and maximum substring.
- Print the maximum substring.
```cpp
class Solution {
private:
    bool isPalin(string str){
        int left=0, right=str.length()-1;
        while(left<right){
            if(str[left] != str[right]) return false;
            left++;
            right--;
        }
        return true;
    }
public:
    string longestPalindrome(string s) {
        if (s.length() <= 1)
            return s;
        int maxLength = 1;
        string maxStr = s.substr(0, 1);
        for (int i = 0; i < s.length(); i++) {
            for (int j = i + maxLength; j <= s.length(); j++) {
                if (j - i > maxLength && isPalin(s.substr(i, j - i))) {
                    maxLength = j - i;
                    maxStr = s.substr(i, j - i);
                }
            }
        }
        return maxStr;
    }
};
```
Time complexity : O(n^3). Assume that n is the length of the input string, there are a total of C(n, 2) = `n(n-1)/2` substrings. Since verifying each substring takes O(n) time, the run time complexity is O(n^3).

Space complexity : O(1).

</details>
<details>
  <summary>DYNAMIC PROGRAMMING</summary>
  <br>

**Intuition :**

To improve over the brute force solution, we first observe how we can avoid unnecessary re-computation while validating palindromes. Consider the case "ababa". If we already knew that "bab" is a palindrome, it is obvious that "ababa" must be a palindrome since the two left and right end letters are the same.
```cpp
class Solution {
public:
    string longestPalindrome(string s) {
        int n=s.length(), maxLen=1, start=0,end=0;
        if(n<=1) return s;
        vector<vector<bool>> dp(n,vector<bool>(n,false));
        dp[0][0] = true;
        for(int i=1;i<n;i++){
            dp[i][i]=true;
            for(int j=0;j<i;j++){
                if(s[i] == s[j] && (i-j<=2 || dp[j+1][i-1])){
                    dp[j][i]=true;
                    if(i-j+1 > maxLen){
                        maxLen = i-j+1;
                        start=j;
                        end=i;
                    }
                }
            }
        }
        return s.substr(start,end-start+1);
    }
};
```
Time complexity : O(n^2). 

Space complexity : O(n^2).

</details>
