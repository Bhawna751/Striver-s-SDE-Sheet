## [13. Roman to Integer](https://leetcode.com/problems/roman-to-integer/description/)

Roman numerals are represented by seven different symbols: `I`, `V`, `X`, `L`, `C`, `D` and `M`.

Symbol       Value
I             1
V             5
X             10
L             50
C             100
D             500
M             1000

For example, 2 is written as `II` in Roman numeral, just two ones added together. 12 is written as `XII`, which is simply `X + II`. The number `27` is written as `XXVII`, which is `XX + V + II`.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not IIII. Instead, the number four is written as IV. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as IX. There are six instances where subtraction is used:

I can be placed before V (5) and X (10) to make 4 and 9. 
X can be placed before L (50) and C (100) to make 40 and 90. 
C can be placed before D (500) and M (1000) to make 400 and 900.
Given a roman numeral, convert it to an integer.

 

Example 1:
```
Input: s = "MCMXCIV"
Output: 1994
```
Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.

**Solution:**
 When a smaller value appears before a larger value, it represents subtraction, while when a smaller value appears after or equal to a larger value, it represents addition.
 ```cpp
class Solution {
public:
    int romanToInt(string s) {
        int n=s.size(),ans=0;//MCMXCIV
        unordered_map<char,int>mpp;
        mpp['I']= 1;
        mpp['V'] = 5;
        mpp['X'] = 10;
        mpp['L'] = 50;
        mpp['C'] = 100;
        mpp['D'] = 500;
        mpp['M'] = 1000;
        for(int i=0;i<n;i++){
            if(mpp[s[i]]<mpp[s[i+1]]) ans = ans-mpp[s[i]];
            else ans=ans+mpp[s[i]];// ans  = 1000 - 100 + 1000 - 10 + 100 -1 + 5 = 1994
        }
        return ans;
    }
};
```
