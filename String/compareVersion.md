## [165. Compare Version Numbers](https://leetcode.com/problems/compare-version-numbers/description/)
Given two version strings, `version1` and `version2`, compare them. A version string consists of revisions separated by dots `.`. The value of the revision is its integer conversion ignoring leading zeros.

To compare version strings, compare their revision values in left-to-right order. If one of the version strings has fewer revisions, treat the missing revision values as 0.

Return the following:
- If `version1` < `version2`, return -1.
- If `version1` > `version2`, return 1.
- Otherwise, return 0.

**Solution:**

Two pointer:

- All the given revisions in version1 and version2 can be stored in a 32-bit integer.
- ginving us a clue that for comparing some numbers we have open option.
- Question asks us to compare versions of two different strings by traversing left to right. And versions are present between dots of strings.
- start generating every possible number present in between dots of both the strings and simply compare those two numbers and on the basis of that comparison we will return our answer.
- For doing this we will use our two pointer approach.
```cpp
class Solution {
public:
    int compareVersion(string version1, string version2) {
        int i=0, j=0, n1=version1.size(), n2=version2.size(), num1=0, num2=0;
        while(i<n1 || j<n2){
            while(i<n1 && version1[i]!='.'){
                num1 = num1 * 10 + (version1[i]-'0');
                i++;
            }
            while(j<n2 && version2[j]!='.'){
                num2 = num2 * 10 + (version2[j]-'0');
                j++;
            }
            if(num1 > num2) return 1;
            if(num1 < num2) return -1;
            i++; j++;
            num1 = 0; num2 =0;
        }
        return 0;
    }
};
```
